<a href="https://awyspr.com/"><img src="https://awyspr.com/assets/images/image07.svg?v=b4a015c2" width="10%" height="10%" align="left"></a>

# Workload cost estimates from CloudFormation

2026-01-19

## What's this one all about then ?

Our recent fieldnote about deal sizing from estimates jogged our memory about an old feature which is worth revisiting: generating
estimates from CloudFormation workload definitions.

This was the hook:

``"Partners can optionally import AWS Pricing Calculator URLs to automatically populate AWS service selections
and corresponding spend estimates into their opportunities, reducing the need for manual re-entry.``

### Workload cost estimates from CloudFormation

This is actually a fairly old CLI/API, but its a goodie.

Essentially, if you have a CloudFormation definition of your workload, you can use that definition to bootstrap
the workload cost estimator. [The details](https://docs.aws.amazon.com/cli/latest/reference/cloudformation/estimate-template-cost.html) 
are tucked away in a place many alliance people will not know exists :-(

A worked example: if we have a Cloudformation yaml file like this:

```
example from devinfrasingle.yaml
```

We can run it like this:

```
aws login
aws cloudformation estimate-template-cost \
  --region us-west-2 \
  --template-body file://devinfrasingle.yaml \
  --parameters \
    ParameterKey=KeyPairName,ParameterValue=your-keypair-name \
    ParameterKey=DBUsername,ParameterValue=dbadmin \
    ParameterKey=DBPassword,ParameterValue=YourSecurePassword123! \
    ParameterKey=AllowedSSHCidr,ParameterValue=0.0.0.0/0 \
    ParameterKey=EnvironmentName,ParameterValue=dev
```

And we get back [a result like this](https://calculator.aws/#/estimate?id=cloudformation/b317e025032ca5e4fb755c4d989429443126e2fb)

<img src="assets/estimator.png" width="50%" height="50%">

### Gotchas

Unfortunately the `estimate-template-cost` function works per region, so if you have a complex solution
with multi-region footprint you need to run the same process a few times with a different region each time. You can wrap it easily enough:

```
for REGION in us-west-2 ap-southeast-2 eu-west-1; do
  echo "=== $REGION ==="
  aws cloudformation estimate-template-cost \
    --region $REGION \
    --template-body file://devinframulti.yaml \
    --parameters \
      ParameterKey=KeyPairName,ParameterValue=your-keypair-name \
      ParameterKey=DBUsername,ParameterValue=dbadmin \
      ParameterKey=DBPassword,ParameterValue=YourSecurePassword123! \
      ParameterKey=AllowedSSHCidr,ParameterValue=0.0.0.0/0 \
      ParameterKey=EnvironmentName,ParameterValue=dev \
    --query 'Url' \
    --output text
done
```

In revisiting this we discovered there's a bug in the new PartnerCentral Estimator which means you
can't import CloudFormation-based Workload Cost Estimates from calculator.aws. We've reported it in detail
and presume it will be fixed eventually (it seems like this was a use case missed in testing).

## The wrap up

If you're working with a solution architect as you develop opportunities for customers, or if you're 
wondering what the cost will be for an internal project, there's an advantage to taking the CloudFormation
route that pays off twice - most people know that IaC = ability to deploy infrastructure from a script, repeatedly,
reliably. A smaller number know you can use the same script to work out the likely cost.

[Back to awyspr fieldnotes index](https://fieldnotes.awyspr.com)
