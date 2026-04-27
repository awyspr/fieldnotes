<a href="https://awyspr.com/"><img src="https://awyspr.com/assets/images/image07.svg?v=b4a015c2" width="10%" height="10%" align="left"></a>

# New PartnerCentral Benefits APIs

2026-01-05

## What's this one all about then ?

In the re:Invent rush and the Christmas-New Year rush we didn't yet look at the 4th API set that AWS released in early December,
for [PartnerCentral Benefits interactions](https://docs.aws.amazon.com/partner-central/latest/APIReference/API_Operations_Partner_Central_Benefits_API.html)

IYKYK - the funding portal (APFP) has been pretty painful to work with. Hopefully we get some new things here ?

### Opening the box

Here's what we got:

```
Candidate 5 version of the AWS Partner Central API released. ...
Introduced a new Benefits API to AWS Partner Central, enabling partners to discover, apply for,
and manage benefits across AWS Partner Programs through a centralized interface.
```

Sounds interesting. In detail, here's what we got (again re-organized the alphabetical list into logical groups):

Right up front, how to file and lifecycle manage former APFP funding claims via API:
* ListBenefitApplications
* CreateBenefitApplication
* GetBenefitApplication
* SubmitBenefitApplication
* AmendBenefitApplication
* RecallBenefitApplication
* CancelBenefitApplication
* UpdateBenefitApplication

Ways to attach things:
* AssociateBenefitApplicationResource
* DisassociateBenefitApplicationResource

Of course to do that you want to be able to see what you're entitled to as a partner:
* ListBenefits
* GetBenefit

Then some ways to check how you're travelling (eg MDF type benefits which are drawn down against a periodic quota):
* ListBenefitAllocations
* GetBenefitAllocation

And the obligatory "tag this" support:
* ListTagsForResource
* TagResource
* UntagResource

## The wrap up

This set of APIs will change the game for partners that have programmatic integration with AWS. Previously, you
could automate/integrate the ACE (opportunity) side and the Marketplace side, but not handle anything to do with
funding. We'll drill down into specific aspects of the Benefits API  over the next few weeks as we work with partners 
to file and progress their funding claims with AWS.

[Back to awyspr fieldnotes index](https://fieldnotes.awyspr.com)
