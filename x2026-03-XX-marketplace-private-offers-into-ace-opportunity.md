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

[WIP]

[steps]

https://docs.aws.amazon.com/marketplace/latest/buyerguide/agreement-eventbridge.html

There's a gap ... no event emitted to trigger this on the marketplace side for a single product opportunity

https://docs.aws.amazon.com/marketplace/latest/userguide/notifications-eventbridge.html#events-for-agreements

### Marketplace private offer requests to ACE oppportunities

[WIP]

## The wrap up

There's not a lot of guidance or advice around as to whether or not syncing Marketplace transactions back to ACE opportunities 
is a desirable thing - but think about it like this - if you have a partner relationship or tier entitlement that is at least 
partially driven by ACE opportunity lifecycle progression, you're going to miss out on some amount of performance attribution 
if you have Marketplace business running and are not bringing at least some of those transactions back to the ACE side. It would
be nice if you could grab both private offers and agreements automatically, but for now, its just not quite possible.

[Back to awyspr fieldnotes index](https://fieldnotes.awyspr.com)







