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

### Minor heading

The `CanelBenefitApplication` method allows you to cancel an in-progress benefit (ie funding)
application. If you use this method, it sets the application status to cancelled, which
permanently stops processing.

We need to do a few things to set this up.

### Finding the Benefit Application
First up we need to work out the Benefit Application metadata.
You can do this in the PartnerCentral UI if you like, but since you can't do anything
with that information, its probably more sensible to work with the API.

Using the AWS CLI:

TBC

### Cancelling

So now we are serious, we can cancel the application. Using the AWS CLI:

``aws partnercentral-benefits cancel-benefit-application \
--catalog "" \
--client-token "" \
--identifier "benappl-XXXXXXXXXX" \
--reason "customer cancelled engagement"
``

As usual, `catalog` means . 

The `client-token` is a user-supplied token which is used to guarantee idempotency. You can use
whatever you like, but better practice would be to reference a CRM case/activity etc and add a date-timestamp.

The `identifier` is the unique ID of the benefit application, which you got back from the first call set.
You can also use an ARN if you want to be fancy.

The `reason` is optional, but encouraged - some text which describes why you are withdrawing the funding application.

Be very clear - **this is not reversible**. Once an appliction is cancelled, it cannot be reactivated and you must start
again from the top with a new application.


no cancel funding in PC UI, how to do it with API instead

As a bonus though, you can reset



Text

```
code block
```

<img src="assets/aws-icons-resource-explorer.png" width="25%" height="25%">

## The wrap up

Text

[Back to awyspr fieldnotes index](https://fieldnotes.awyspr.com)
