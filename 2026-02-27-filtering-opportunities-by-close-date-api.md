<a href="https://awyspr.com/"><img src="https://awyspr.com/assets/images/image07.svg?v=b4a015c2" width="10%" height="10%" align="left"></a>

# Filtering opportunities by close date on PartnerCentral Selling API

2026-02-27

## What's this one all about then ?

AWS have updated the PartnerCentral Selling API with 1 very useful method to support opportunity close date filtering in search.

### The details

Its a bit unusual for us to comment on a single API method change - but its a very useful and important change.

Why is this one so important ?

Anyone managing ACE opportunities at scale and via API - whether its a roll-your-own integration or using a 3rd party CRM integration provider,
is going to be somewhere along the line looking to search and filter/sort opportunities _by close date_.

Until now, you've been able to do this in the legacy PartnerCentral and over the UI in the new PartnerCentral ACE view, but not on the API.

And now you can - filter results to return opportunities with a target close date before or after a specified date, enabling more precise opportunity searches based on expected closure timelines.

The change itself is very simple:

* ListOpportunities via ```{'Sort': {'SortBy': {'TargetCloseDate'}},'TargetCloseDate': {'AfterTargetCloseDate': 'string', 'BeforeTargetCloseDate': 'string'}}```

Essentially - anything that closes before a date, or closes after a date can now be filtered from the rest.

The details are in [the doco](https://docs.aws.amazon.com/partner-central/latest/APIReference/API_ListOpportunities.html).

## The wrap up

Filling in little gaps like this is disproportionally beneficial in support of the AWS campaign to make partner business more integrated
and automated moving through 2026.

[Back to awyspr fieldnotes index](https://fieldnotes.awyspr.com)
