OFFCUTS & NOTES

## 2026-06
~ 1 Jun creating budgets via API https://docs.aws.amazon.com/aws-cost-management/latest/APIReference/API_budgets_CreateBudget.html

~ 5 May https://aws.amazon.com/blogs/awsmarketplace/deploy-aws-marketplace-spg-dashboard-unified-insights/

## 2026-05

## 2026-04
~ 6 Apr
https://awsapichanges.com/archive/changes/080f45-agreement-marketplace.html
2026/03/31 - AWS Marketplace Agreement Service - 8 new api methods

~ 2 Apr
https://awsapichanges.com/archive/changes/080f45-organizations.html
2026/03/31 - AWS Organizations - 8 updated api methods

## 2026-03

## 2026-02

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

- It would be amazing if you could attach AWS Services to Solutions and then inherit them down to Opportunities which are linked to that Solution. Currently you can't do this, if you want to connect AWS Services to Opportunities you have to do it directly, and at scale the way you do this is to write a query that essentially says "for solution X here is a map of the attached/impacted AWS Services, now go and find all the Opportunities that are connected to that Solution, and then for each of those Opportunities, attach/link the AWS Services that are included in the map". If you use a 3PI, this is logic that they build-maintain, if you don't use a 3PI for CRM you can't do anything with it but flag it for the partner seller that it needs to be added manually (and so it never happens). There will always be the case that for a specific Opportunity there might be non-standard Services attached if its a Solution with a few tweaks around the edges, but currently its a first order problem which is needing to double handle. Whats the ask ? Make it possible to connect AWS Services to a Solution via API, nd then make it possible to inherit that relationship onto the Opportunity.


MISSING IN ACTION - Can't attach AWS Products/Services to Solutions, only from Solutions to Opps (no inheritance) - (Timothy/Tom)

We'll attack this as a two-stepper in a separate post shortly.


MISSING-IN-ACTION: Can't link ProSrv Solutions to AWS Products/Services via API
Another thing thats still not possible is linking Professional Services type Solutions to AWS Products/Services via API.

MISSING-IN-ACTION: Can't edit/maintain Partner Solutions in PartnerCentral via API (Tom/Timothy)
Its a long standing thing, but we're reminded of it while looking at all of the wonderful things you can do with the new PartnerCentral Account API - you can't maintain Solutions. You can link Solutions to Opportunities (or vice versa) as you'd expect and as been available in the legacy  PartnerCentral and in the new PartnerCentral v3.0 (in Console) but you can't create, edit/update Solutions - thats a UI only task.

