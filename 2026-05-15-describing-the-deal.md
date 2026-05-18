<a href="https://awyspr.com/"><img src="https://awyspr.com/assets/images/image07.svg?v=b4a015c2" width="10%" height="10%" align="left"></a>

# Describing the Deal (ContractDuration support in PartnerCentral Selling API)

2026-05-15

## What's this one all about then ?

AWS have updated the PartnerCentral Selling API with a handful of new features/fields which finer grained description of commercial
aspects of opportunities.

### The details

Both [Stacklet](https://awsapichanges.info/archive/changes/994b6d-partnercentral-selling.html) and [TrustOnCloud](https://awsapichanges.com/archive/changes/994b6d-partnercentral-selling.html) picked this up or you can try your luck with the [actual AWS doco].(https://docs.aws.amazon.com/partner-central/latest/APIReference/API_Operations_Partner_Central_Selling_API.html)

Specifically there's now the ability to add some additional fields to an API call which creates, queries, or updates an opportunity:

* CreateOpportunity via ```{'Project': {'ExpectedContractDuration': {'Term': 'Months', 'Value': 'string'}}}```
* GetOpportunity again via ```{'Project': {'ExpectedContractDuration': {'Term': 'Months', 'Value': 'string'}}}```
* GetResourceSnapshot via ```{'Payload': {'OpportunitySummary': {'Project': {'ExpectedContractDuration': {'Term': 'Months', 'Value': 'string'}}}}}```
* ListOpportunities via ```{'OpportunitySummaries': {'Project': {'ExpectedContractDuration': {'Term': 'Months', 'Value': 'string'}}}}```
* UpdateOpportunity again via ```{'Project': {'ExpectedContractDuration': {'Term': 'Months', 'Value': 'string'}}}```

Unsurprisingly, these fields actually reflect the project's duration and total commercial value. Prior to this, you could only add this information in the description of the opportunity in ACE (for duration) and as ARR (or more recently MRR, for value) and then neither the partner or AWS could ever really work with it.

## The wrap up

In late 2025 the first move was from ACE opportunity ARR to MRR and links to both an AI validator and new cost estimator, and then supported through the PartnerCentral Selling API. That was helpful but didn't tell anyone how long you expected this arrangement to go on for (was it one month, one year, one decade).

This might seem like a small change, but it significantly shifts the understanding of the customer's spend in terms of both quantum and timing. If we are the partner, we can now differentiate and resource around a longer period + lower spend, and a shorter period + higher spend opportunity. If we are AWS, then it also helps us understand spikey vs smoothed vs sustained adoption which then allows different types of co-sell support. And this can be done natively in ACE or via API, rather than held out in a CRM or a 3rd party CRM-ACE sync solution.

[Back to awyspr fieldnotes index](https://fieldnotes.awyspr.com)
