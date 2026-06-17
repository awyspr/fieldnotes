<a href="https://awyspr.com/"><img src="https://awyspr.com/assets/images/image07.svg?v=b4a015c2" width="10%" height="10%" align="left"></a>

# Ability to cancel funding has been itself been cancelled (or has it) ?

2026-06-04

## What's this one all about then ?

In the legacy version of PartnerCentral, and specifically in APFP, you could lifecycle manage funding applications
in the UI, including cancelling existing funding applications.

With the move to PC v3.0 in Console, this UI cancellation option isn't available any more. 

One of our customers asked us about this, so we asked our friendly PDM and AWS partner support and were 
told "yes, we know because many people complained that this has gone away, we are assured it will come back 
eventually" (thats not verbatim ... but you get the idea).

Then we worked it out anyway.

You can do this with the PartnerCentral Benefits API, which was released in late 2025.
Its not even as hairy as you might think.

## Cancelling or not, the choice is yours

The `CanelBenefitApplication` method allows you to cancel an in-progress benefit (ie funding)
application. If you use this method, it sets the application status to cancelled, which
permanently stops processing.

We need to do a few things to set this up.

### Finding the Benefit Application
First up we need to work out the Benefit Application metadata.
You can do this in the PartnerCentral UI if you like, but since you can't do anything
with that information, its probably more sensible to work with the API.

We can use the [`ListBenefitApplications` method](https://docs.aws.amazon.com/cli/latest/reference/partnercentral-benefits/list-benefit-applications.html)

Using the AWS CLI:

```
aws partnercentral-benefits list-benefit-applications --catalog AWS
```

Now by default that pulls back all benefit/funding applications for a partner. you might have a few, in which
case you probably want to use one or more of the filters available:

If you know the specific benefit identifier (eg nicked it from PartnerCentral UI) you can use:

- `--benefit-identifiers <value>`

Else some other useful parameters are:

- `--programs <value>` - to filter by partner program type
- `[--fulfillment-types <value>` - to filter by fulfillment types (CASH, CREDIT, ACCESS)
- `--status <value>` (PENDING_SUBMISSION, IN_REVIEW, ACTION_REQUIRED, APPROVED, REJECTED, CANCELED)

### Cancelling

We can use the (`CancelBenefitsApplication` method](https://docs.aws.amazon.com/partner-central/latest/APIReference/API_benefits_CancelBenefitApplication.html]

if we are serious, we can cancel the application. Using the AWS CLI:

```
aws partnercentral-benefits cancel-benefit-application \
--catalog "aws" \
--client-token "XXXXXX" \
--identifier "benappl-XXXXXXXXXX" \
--reason "customer cancelled engagement"
```

As usual, `catalog` means `AWS` unless you're using GovCloud or European Sovereign Cloud.

The `client-token` is a user-supplied token which is used to guarantee idempotency. You can use
whatever you like, but better practice would be to reference a CRM case/activity etc and add a date-timestamp.

The `identifier` is the unique ID of the benefit application, which you got back from the first call set.
You can also use an ARN if you want to be fancy.

The `reason` is optional, but encouraged - some text which describes why you are withdrawing the funding application.

Be very clear - **this is not reversible**. Once a benefit/funding application is cancelled, it cannot be reactivated and you must start
again from the top.

### Not Cancelling, Just Recalling
As a bonus though, you can recall a benefit application via the API as well.

Recalling puts the application in draft. You can't recall an application that has progressed past Pre-Approval though, you
need to cancel it and start again. 

This time we can use the [`RecallBenefitApplication` method](https://docs.aws.amazon.com/partner-central/latest/APIReference/API_benefits_RecallBenefitApplication.html)

Using the CLI:

```
aws partnercentral-benefits recall-benefit-application \
--catalog <value> \ 
--client-token <value> \
--identifier <value> \ 
--reason <value>
```

## The wrap up

Its unfortunate that sometimes AWS partner facing tools go through changes which remove previously available
functionality, and cause a bit of stress when processes built around them break. In this case, the UI certainly
changed but as is more and more the case with AWS partnerships, if you are programmatically inclined or integrated,
you can use more technical tools to achieve not only the original objective but sometimes even things that were
not available earlier. Benefits Cancellation is just one of them.


[Back to awyspr fieldnotes index](https://fieldnotes.awyspr.com)
