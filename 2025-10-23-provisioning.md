
<a href="https://awyspr.com/"><img src="https://awyspr.com/assets/images/image07.svg?v=b4a015c2" width="10%" height="10%" align="left"></a>

# Provisioning accounts, users, groups, permissions - an automated approach

2025-10-23

## What's this one all about then ?

One thing we are often asked is how to automate provisioning for new accounts, groups and users, under a partner's Organization.

There are lots of ways to do this, but we've automated it ;-) and here's how.

### The job
Given an existing AWS account within an Organization and with an operational IAM Identity Center instance in the Organization and Region:

- Create a group called `*-workload-admin-group`
- Assign that group to the account with IAM Managed Policy for AdministratorAccess permission set
- Create an admin user called `*-workload-admin`
- Put that admin user into the group

Now to do this you need a few prerequisites like:

* You will need to be able to ``aws login``.
* You need permissions to call ``aws sso-admin``, ie something like Admin Access for the user who is running the script.
* The AWS account needs to be created under the Partner Organization. The script does _not_ create the AWS account.
* IAM Identity Center installed in the region. Users, groups and permissions are managed using IAM Identity Center.
* You need to come up with a customer nickname, or slug.
* You need to know the customer's admin account email address.
* You need to know which region you're working in.
 
## The script

Here's the full script. 

Rename it something like setup-customer-aws.sh and run it with bash (works on Linux or Mac, or even Windows Subsystem for Linux).
Assumes you have ```aws-cli``` installed and can login with the appropriate permissions

Run it with:

``bash setup-customer-aws.sh --slug SLUG --awsacct 1234567890 --email name@customer.com --region us-east-1``

Replace the slug, AWS account, email address and region as appropriate.

```
#!/usr/bin/env bash
set -euo pipefail

# ── Parse named parameters ───────────────────────────────────────────────────
while [[ $# -gt 0 ]]; do
  case "$1" in
    --slug)    SLUG="$2";    shift 2 ;;
    --awsacct) AWSACCT="$2"; shift 2 ;;
    --email)   EMAIL="$2";   shift 2 ;;
    --region)  REGION="$2";  shift 2 ;;
    *) echo "Unknown parameter: $1"; exit 1 ;;
  esac
done

# ── Validate all required params present ────────────────────────────────────
for var in SLUG AWSACCT EMAIL REGION; do
  [ -z "${!var:-}" ] && { echo "Missing required parameter: --${var,,}"; exit 1; }
done

# ── Discover SSO instance ────────────────────────────────────────────────────
echo "Looking up IAM Identity Center instance in $REGION..."
INSTANCE_DATA=$(aws sso-admin list-instances --region "$REGION" --query 'Instances[0]' --output json)
INSTANCE_ARN=$(echo "$INSTANCE_DATA"      | python3 -c "import sys,json; print(json.load(sys.stdin)['InstanceArn'])")
IDENTITY_STORE_ID=$(echo "$INSTANCE_DATA" | python3 -c "import sys,json; print(json.load(sys.stdin)['IdentityStoreId'])")

echo "Instance ARN:      $INSTANCE_ARN"
echo "Identity Store ID: $IDENTITY_STORE_ID"

GROUP_NAME="${SLUG}-workload-group"
USER_NAME="${SLUG}-workload-admin"

# ── 1. Create group ──────────────────────────────────────────────────────────
echo "Creating group: $GROUP_NAME..."
GROUP_ID=$(aws identitystore create-group \
  --identity-store-id "$IDENTITY_STORE_ID" \
  --display-name "$GROUP_NAME" \
  --region "$REGION" \
  --query 'GroupId' --output text)
echo "Created group: $GROUP_NAME ($GROUP_ID)"

# ── 2. Find AdministratorAccess permission set ───────────────────────────────
echo "Looking up AdministratorAccess permission set..."
PERMISSION_SET_ARN=""
NEXT_TOKEN=""
while true; do
  if [ -z "$NEXT_TOKEN" ]; then
    PAGE=$(aws sso-admin list-permission-sets \
      --instance-arn "$INSTANCE_ARN" \
      --region "$REGION" \
      --output json)
  else
    PAGE=$(aws sso-admin list-permission-sets \
      --instance-arn "$INSTANCE_ARN" \
      --region "$REGION" \
      --next-token "$NEXT_TOKEN" \
      --output json)
  fi

  for PSA in $(echo "$PAGE" | python3 -c "import sys,json; [print(p) for p in json.load(sys.stdin)['PermissionSets']]"); do
    NAME=$(aws sso-admin describe-permission-set \
      --instance-arn "$INSTANCE_ARN" \
      --permission-set-arn "$PSA" \
      --region "$REGION" \
      --query 'PermissionSet.Name' --output text)
    if [ "$NAME" = "AdministratorAccess" ]; then
      PERMISSION_SET_ARN="$PSA"
      break 2
    fi
  done

  NEXT_TOKEN=$(echo "$PAGE" | python3 -c "import sys,json; d=json.load(sys.stdin); print(d.get('NextToken',''))")
  [ -z "$NEXT_TOKEN" ] && break
done

[ -z "$PERMISSION_SET_ARN" ] && { echo "AdministratorAccess permission set not found"; exit 1; }
echo "AdministratorAccess ARN: $PERMISSION_SET_ARN"

# ── 3. Assign group to account with AdministratorAccess (async + poll) ───────
echo "Assigning $GROUP_NAME to account $AWSACCT..."
ASSIGNMENT_REQUEST_ID=$(aws sso-admin create-account-assignment \
  --instance-arn "$INSTANCE_ARN" \
  --target-id "$AWSACCT" \
  --target-type AWS_ACCOUNT \
  --permission-set-arn "$PERMISSION_SET_ARN" \
  --principal-type GROUP \
  --principal-id "$GROUP_ID" \
  --region "$REGION" \
  --query 'AccountAssignmentCreationStatus.RequestId' --output text)

echo "Waiting for account existence confirmation (request: $ASSIGNMENT_REQUEST_ID)..."
while true; do
  STATUS=$(aws sso-admin describe-account-assignment-creation-status \
    --instance-arn "$INSTANCE_ARN" \
    --account-assignment-creation-request-id "$ASSIGNMENT_REQUEST_ID" \
    --region "$REGION" \
    --query 'AccountAssignmentCreationStatus.Status' --output text)
  echo "  Status: $STATUS"
  case "$STATUS" in
    SUCCEEDED) echo "Account confirmed to exist."; break ;;
    FAILED)
      REASON=$(aws sso-admin describe-account-assignment-creation-status \
        --instance-arn "$INSTANCE_ARN" \
        --account-assignment-creation-request-id "$ASSIGNMENT_REQUEST_ID" \
        --region "$REGION" \
        --query 'AccountAssignmentCreationStatus.FailureReason' --output text)
      echo "Account existence check FAILED: $REASON"; exit 1 ;;
    *) sleep 10 ;;
  esac
done

# ── 4. Create user ───────────────────────────────────────────────────────────
echo "Creating user: $USER_NAME..."
USER_ID=$(aws identitystore create-user \
  --identity-store-id "$IDENTITY_STORE_ID" \
  --user-name "$USER_NAME" \
  --display-name "$USER_NAME" \
  --emails "Value=${EMAIL},Type=work,Primary=true" \
  --name "GivenName=${SLUG},FamilyName=Workload Admin" \
  --region "$REGION" \
  --query 'UserId' --output text)
echo "Created user: $USER_NAME ($USER_ID)"

# ── 5. Add user to group ─────────────────────────────────────────────────────
echo "Adding $USER_NAME to $GROUP_NAME..."
aws identitystore create-group-membership \
  --identity-store-id "$IDENTITY_STORE_ID" \
  --group-id "$GROUP_ID" \
  --member-id "UserId=${USER_ID}" \
  --region "$REGION"

echo ""
echo "Done. $USER_NAME is now a member of $GROUP_NAME, which is assigned AdministratorAccess via permissions on account $AWSACCT."
```

## Caveats

While automation is good, there are a couple of assumptions worth noting:

1. You're operating the customer's AWS account within a Partner organization.
2. You have not installed Landing Zone Accelerator or Control Tower based configurations over the customer's
AWS account. Should you ? Maybe.
4. You've got IAM Identity Center activated in the region you are working in.
5. Not everything is instantaneous and synchronous, the script waits and polls at certain places, and the
customer email address will be notified that their account needs to be activated.
 
## The wrap up

There's lots of ways to do basic account provisioning for AWS for a new account ranging from DIY in the Console through 
to using various forms of automation. This is one simple example, which at least keeps things pretty organized in
the absence of an overlay like Control Tower.


[Back to awyspr fieldnotes index](https://fieldnotes.awyspr.com)
