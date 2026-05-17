OFFCUTS

## 2026-05

~ 15 May PartnerCentral Selling API 5 updated methods
https://awsapichanges.com/archive/changes/994b6d-partnercentral-selling.html

~4 May finding the offer ID for a draft listing (aka Bhagirath call)

## 2026-04
~ 6 Apr
https://awsapichanges.com/archive/changes/080f45-agreement-marketplace.html
2026/03/31 - AWS Marketplace Agreement Service - 8 new api methods

~ 2 Apr
https://awsapichanges.com/archive/changes/080f45-organizations.html
2026/03/31 - AWS Organizations - 8 updated api methods

## 2026-03
~ 31 Mar
https://awsapichanges.com/archive/changes/99ac86-partnercentral-account.html
2026/03/30 - Partner Central Account API - 2 updated api methods

~ 23 Mar - Mapping PartnerCentral Users to Managed Policies
https://docs.aws.amazon.com/partner-central/latest/getting-started/managed-policy-mappings.html
https://docs.aws.amazon.com/partner-central/latest/getting-started/managed-policies.html#security-iam-awsmanpol-updates



NEW-IN-TOWN: Partner Central Agents/MCP compare and contrast Opportunity advice.
Disclosure - using Hubspot as CRM. They're unsuprisingly different and so the value is somewhere in the middle, and most likely operationalized on the CRM side not in ACE. Pull the opportunity summary/recommendations through into CRM, merge/compare with local intelligence that is not synced up, and then decide what to do.

Automation can surface signals and suggest actions, but it doesn’t solve the core problem that partnerships were designed to address in the first place: trust. Buyers still purchase through people and organisations they trust to interpret options, challenge assumptions, and advocate on their behalf. Agents can process data, but they don’t replace that trust layer. There’s also an inherent tension when the platform recommending “next steps”, funding, or incentives is the same platform selling the infrastructure. Customers aren’t naïve — they know when recommendations may be steering them toward the vendor’s preferred outcome.

## 2026-02

~26/27 Feb 
https://awsapichanges.com/archive/changes/b6a65c-partnercentral-selling.html
2026/02/24 - Partner Central Selling API - 1 updated api methods


HOW-TO: Using Resource Explorer vs Cost Explorer for Tagged Workloads

HOW-TO: Mass Tagging for PRM
PRM tagging and exposure of additional info


## 2026-01

MISSING-IN-ACTION: Can't import CloudFormation-based Workload Cost Estimates from calculator.aws into PartnerCentral "Estimator"

HOW-TO: Port Old Estimate to New Estimate

HOW-TO: Create Workload Cost Estimates from CloudFormation
https://docs.aws.amazon.com/cli/latest/reference/cloudformation/estimate-template-cost.html


NEW-IN_TOWN Deal Sizing from Estimates

https://aws.amazon.com/about-aws/whats-new/2025/12/aws-partner-central-opportunity-deal-sizing/


HOW-TO: Service-link ACE Opps with Solution Support
As we reported earlier, you can't attach AWS products/Services to Solutions, nor inherit Products/Services from a Solution onto an Opportunity. So instead, you have to do a two-stepper. Here's one way to achieve the goal without resorting to manual UI click-errors, or needing a 3PI to fill the gap.

Template Products/Services for Solutions

Link Solutions to Opportunities

Iterate Solutions to Link Products/Services to Opportunities using Template


MISSING IN ACTION - Can't attach AWS Products/Services to Solutions, only from Solutions to Opps (no inheritance) - (Timothy/Tom)

We'll attack this as a two-stepper in a separate post shortly.


MISSING-IN-ACTION: Can't link ProSrv Solutions to AWS Products/Services via API
Another thing thats still not possible is linking Professional Services type Solutions to AWS Products/Services via API.

MISSING-IN-ACTION: Can't edit/maintain Partner Solutions in PartnerCentral via API (Tom/Timothy)
Its a long standing thing, but we're reminded of it while looking at all of the wonderful things you can do with the new PartnerCentral Account API - you can't maintain Solutions. You can link Solutions to Opportunities (or vice versa) as you'd expect and as been available in the legacy  PartnerCentral and in the new PartnerCentral v3.0 (in Console) but you can't create, edit/update Solutions - thats a UI only task.

