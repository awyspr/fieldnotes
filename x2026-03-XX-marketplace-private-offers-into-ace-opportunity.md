<a href="https://awyspr.com/"><img src="https://awyspr.com/assets/images/image07.svg?v=b4a015c2" width="10%" height="10%" align="left"></a>

# Turning Marketplace private offers into ACE opportunities

2026-03-XX

## What's this one all about then ?

It seems pretty reasonable that if you've invested in putting products and services up on AWS Marketplace that you want to be 
able to kick off an ACE opportunity at the point where a potential customer requests a private offer on Marketplace - right ?

This feature is [available for the new shiny multi-product solution private offers](https://docs.aws.amazon.com/marketplace/latest/userguide/multi-product-solutions-faq.html#what-is-ace). But its not available for "older" single product private offers - or at least not yet anyway.

So we set out to see if we could solve, eg automate the solution to capture an event from AWS marketplace private offer 
request so that we can create an ACE opportunity from it, using respective APIs and passing the payload between the two. 

It turns out you can _almost_ do this but not quite. Why is there a gap ? Who knows but its probably to do with the fact
that ACE and Marketplace teams have been historically separate.

tl;dr 
* you can kick off an ACE opportunity from a Marketplace action with "agreement" being the trigger but not 
"request private offer" being the trigger.
* with 1-step manual handling you can do the same with "private offer" as well. Automagic is just not quite strong enough.

### Marketplace agreements to ACE oppportunities

You can use AWS Marketplace agreements as the trigger for creating and advancing ACE opportunities. 

The bad news - ACE opportunities still need validation, so despite you having an actual agreement for purchase of the product or service from marketplace, syncing that over to the ACE side of the house requires a delay until validation happens, and then advancing the ACE Stage essentially from Approved to Launched in one step.

No matter, lets look at the how.

1. Catch the [Purchase Agreement Created - Acceptor event from EventBridge](https://docs.aws.amazon.com/marketplace/latest/buyerguide/agreement-eventbridge.html). Assumes you have EventBridge setup, or you can wrangle your systems team to do the same [more info](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-create-rule.html)

2. Extract the Agreement ID from the payload:
  
```
    "agreement": {
      "id": "agmt-4mwg1nevbokzw95eca5797ixs",
      "intent": "NEW",
      "status": "ACTIVE",
      "acceptanceTime": "2024-06-26T21:36:03Z",
      "startTime": "2024-08-30T21:36:03Z",
      "endTime": "2025-05-30T21:36:03Z"
    },
```

3. Lookup the Agreement to get additional details

?? https://docs.aws.amazon.com/marketplace/latest/APIReference/API_marketplace-agreements_DescribeAgreement.html

4. Construct the ACE opportunity

--- somehow in here get the extra data you need ---

https://docs.aws.amazon.com/partner-central/latest/APIReference/API_CreateOpportunity.html

5. Catch the ACE opportunity approval event

Regularly poll the ListOpportunities API and filter the results by LifecycleStage and look for ```Prospect```.
[More info](https://docs.aws.amazon.com/partner-central/latest/APIReference/API_ListOpportunities.html)

Allegedly you can use [EventBridge for this](https://docs.aws.amazon.com/partner-central/latest/APIReference/selling-api-events.html)
and trapping for the [Opportunity Updated details](https://docs.aws.amazon.com/partner-central/latest/APIReference/selling-api-events.html#opportunity-updated)

6. Link the AWSMP Agreement to the ACE Opportunity


### Marketplace private offer requests to ACE oppportunities

[WIP]

## The wrap up

There's not a lot of guidance or advice around as to whether or not syncing Marketplace transactions back to ACE opportunities 
is a desirable thing - but think about it like this - if you have a partner relationship or tier entitlement that is at least 
partially driven by ACE opportunity lifecycle progression, you're going to miss out on some amount of performance attribution 
if you have Marketplace business running and are not bringing at least some of those transactions back to the ACE side. It would
be nice if you could grab both private offers and agreements automatically, but for now, its just not quite possible.

[Back to awyspr fieldnotes index](https://fieldnotes.awyspr.com)







