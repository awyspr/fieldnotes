<a href="https://awyspr.com/"><img src="https://awyspr.com/assets/images/image07.svg?v=b4a015c2" width="10%" height="10%" align="left"></a>

# PartnerCentral Selling APIs

2025-12-02

## What's this one all about then ?

Its re:Invent season so we must have heaps of new things - and we got some more. AWS has just released a heap of new APIs for PartnerCentral Selling interaction - the [PartnerCentral Selling API](https://docs.aws.amazon.com/partner-central/latest/APIReference/API_Operations_Partner_Central_Selling_API.html)

This will be interesting because its a bit of a cross-over into the older ACE (CRM) APIs and maybe some Marketplace stiff. Lets take a look.

### Opening the box

Lets look at what we got:

```
Candidate 5 version of the AWS Partner Central API released. ... Enhanced Selling API engagement actions to support lead management workflow.
... Enhanced Selling API documentation for Engagement management with Lead context.
```

So what's that actually mean ? We got all these methods, and we re-organized the alphabetical list into logical groups:

Unsurprisingly, the fundamentals for opportunities are here:
* ListOpportunities
* GetOpportunity
* GetAwsOpportunitySummary
* AssignOpportunity
* AssociateOpportunity
* CreateOpportunity
* SubmitOpportunity
* UpdateOpportunity
* DisassociateOpportunity
* ListOpportunityFromEngagementTasks
* StartOpportunityFromEngagementTask

A group about engagement, which is really the word AWS uses for co-sell collaboration:
* ListEngagements
* CreateEngagement
* GetEngagement
* GetEngagementInvitation
* CreateEngagementContext
* CreateEngagementInvitation
* AcceptEngagementInvitation
* RejectEngagementInvitation
* UpdateEngagementContext
* ListEngagementByAcceptingInvitationTasks
* ListEngagementFromOpportunityTasks
* ListEngagementInvitations
* ListEngagementMembers
* ListEngagementResourceAssociations
* StartEngagementByAcceptingInvitationTask
* StartEngagementFromOpportunityTask

A bunch associated with resources:
* ListResourceSnapshots
* GetResourceSnapshot
* CreateResourceSnapshot
* ListResourceSnapshotJobs
* GetResourceSnapshotJob
* CreateResourceSnapshotJob
* StartResourceSnapshotJob
* StopResourceSnapshotJob
* DeleteResourceSnapshotJob

A couple of loose ends:
* GetSellingSystemSettings
* PutSellingSystemSettings

A real loner, about solutions. (You know, we thought they might finally release an API for managing solutions, but no, not yet):
* ListSolutions

And the obligatory "tag this" method collection:
* ListTagsForResource
* TagResource
* UntagResource

## The wrap up

Thats quite a lot, but really focused on opportunities and engagement.

[Back to awyspr fieldnotes index](https://fieldnotes.awyspr.com)

