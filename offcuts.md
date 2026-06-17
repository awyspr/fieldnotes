# Offcuts & WIP Notes

## 2026-06 Running

17/Jun Agentic RTS for AWSMP
https://aws.amazon.com/blogs/apn/get-ready-to-sell/

17/Jun NY Summit Storefronts
https://aws.amazon.com/marketplace/partners/storefront

16/Jun 
https://awsapichanges.com/archive/changes/e078c6-partnercentral-selling.html


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

