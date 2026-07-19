# Offcuts & WIP Notes

## 2026-08 Running

## 2026-07 Running

https://awsiamchanges.com/changes/1782907200-partnercentral.html
Lots of methods (15-20) re marketplace revenue shares in AWS Partner Central
And an associated set of IAM managed policy changes
https://github.com/zoph-io/IAMTrail/commit/34f3a5ae63c9f7945b9aa8d32f5e48ae980b0918
https://github.com/zoph-io/IAMTrail/commit/45b641a8d8a00e624733af1492562d5fad6986d8



https://awsapichanges.com/archive/changes/7ad90e-partnercentral-selling.html
This release adds AwsMarketplaceSolutions and AwsMarketplaceProducts entity types to the Associate and Disassociate APIs, returns them in GetOpportunity, and adds AwsMarketplaceSolutionArn to ListSolutions ,letting partners link Marketplace listings directly to opportunities.


https://aws.amazon.com/blogs/aws-cloud-financial-management/automate-aws-invoice-retrieval-with-new-programmatic-apis
Automate AWS Invoice Retrieval with New Programmatic APIs -
An API to download the invoices documenting how much they charge you, free of charge. The generosity is staggering. Finance teams have spent years clicking through hundreds of payer accounts like it's 2009, the post admits this, but somehow presents it as "innovation" rather than "dreadfully, painfully late."


https://docs.aws.amazon.com/marketplace/latest/userguide/search-engine-optimization.html

## 2026-06 Running

17/Jun Agentic GRTS for AWSMP
https://aws.amazon.com/blogs/apn/get-ready-to-sell/
Fairly well telegraphed progression down the "integrate, automate and agentify" partner motions - partners not in this game are going to be left
behind.

17/Jun NY Summit Storefronts
https://aws.amazon.com/marketplace/partners/storefront
Might be interpreted as AWS recognising that partners are more likely to be successful if they manage the channel to market under their own steam
rather than trying to push them directly to marketplace, and hey AWS takes the same clip of the transaction anyway. Agentic probably native. Non-agentic will be distributed. Thoughts.

In a lot of ways this feels really like a layer on top of the older Buy with AWS program and platform.
No APIs yet.

16/Jun
https://aws.amazon.com/about-aws/whats-new/2026/06/ai-assisted-product-listing/
Maybe we are biased but the "Strength" analysis is kinda interesting. Would be even more so if it was exposed as a metric on an API for comparison.

16/Jun 
https://awsapichanges.com/archive/changes/e078c6-partnercentral-selling.html
Added Prospecting APIs to convert engagements into AI-enriched leads with scoring insights. Extended Engagement APIs with ProspectingResult and Lead contexts. Added CoSell Scoring to GetAwsOpportunitySummary- quality score, trend, agent-driven recommendations, and engagement classification.
https://docs.aws.amazon.com/partner-central/latest/APIReference/API_GetAwsOpportunitySummary.html#API_GetAwsOpportunitySummary_ResponseSyntax
Joining some dots - human co-sell will be heavily biased based on propensity and other deal factors (size, timing), agentic co-sell will be in the middle, and partners will be doing it for themselves at low propensity. Presume that incentives will be rebalanced in a similar way, with or without PRM.


## 2026-02 Older

HOW-TO: Using Resource Explorer vs Cost Explorer for Tagged Workloads

HOW-TO: Mass Tagging for PRM
PRM tagging and exposure of additional info

## 2025 Even Older ...

HOW-TO: Service-link ACE Opps with Solution Support
As we reported earlier, you can't attach AWS products/Services to Solutions, nor inherit Products/Services from a Solution onto an Opportunity. So instead, you have to do a two-stepper. Here's one way to achieve the goal without resorting to manual UI click-errors, or needing a 3PI to fill the gap.

Template Products/Services for Solutions

Link Solutions to Opportunities

Iterate Solutions to Link Products/Services to Opportunities using Template

- It would be amazing if you could attach AWS Services to Solutions and then inherit them down to Opportunities which are linked to that Solution. Currently you can't do this, if you want to connect AWS Services to Opportunities you have to do it directly, and at scale the way you do this is to write a query that essentially says "for solution X here is a map of the attached/impacted AWS Services, now go and find all the Opportunities that are connected to that Solution, and then for each of those Opportunities, attach/link the AWS Services that are included in the map". If you use a 3PI, this is logic that they build-maintain, if you don't use a 3PI for CRM you can't do anything with it but flag it for the partner seller that it needs to be added manually (and so it never happens). There will always be the case that for a specific Opportunity there might be non-standard Services attached if its a Solution with a few tweaks around the edges, but currently its a first order problem which is needing to double handle. Whats the ask ? Make it possible to connect AWS Services to a Solution via API, nd then make it possible to inherit that relationship onto the Opportunity.


MISSING IN ACTION - Can't attach AWS Products/Services to Solutions, only from Solutions to Opps (no inheritance) - (Timothy/Tom)

We'll attack this as a two-stepper in a separate post shortly.


MISSING-IN-ACTION: Can't link ProSrv Solutions to AWS Products/Services via API
Another thing thats still not possible is linking Professional Services type Solutions to AWS Products/Services via API.

MISSING-IN-ACTION: Can't edit/maintain Partner Solutions in PartnerCentral via API (Tom/Timothy)
Its a long standing thing, but we're reminded of it while looking at all of the wonderful things you can do with the new PartnerCentral Account API - you can't maintain Solutions. You can link Solutions to Opportunities (or vice versa) as you'd expect and as been available in the legacy  PartnerCentral and in the new PartnerCentral v3.0 (in Console) but you can't create, edit/update Solutions - thats a UI only task.

