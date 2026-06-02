<a href="https://awyspr.com/"><img src="https://awyspr.com/assets/images/image07.svg?v=b4a015c2" width="10%" height="10%" align="left"></a>

# deal sizing from estimates

2026-01-16

## What's this one all about then ?

Back in action in the New Year, and trying to work out what we missed between pre:Invent, re:Invent, end of year, Christmas/New Year holidays, and we spotted this this post-re:Invent announcement about being able to [generate or compare deal sizing estimates with AI in PartnerCentral in the ACE workflow](https://aws.amazon.com/about-aws/whats-new/2025/12/aws-partner-central-opportunity-deal-sizing/).

`This new feature, available within the APN Customer Engagements (ACE) Opportunities, uses AI to provide deal 
size estimates and AWS service recommendations. Deal Sizing capability allows Partners to save time on deal
management by simplifying the process of estimating AWS monthly recurring revenue (MMR) when creating or updating
opportunities.`

`Partners can optionally import AWS Pricing Calculator URLs to automatically populate AWS service selections
and corresponding spend estimates into their opportunities, reducing the need for manual re-entry. When a Pricing
Calculator URL is provided, deal sizing delivers enhanced insights including pricing strategy optimization
recommendations, potential cost savings analysis, Migration Acceleration Program (MAP) eligibility indicators,
and modernization pathway analysis. These enhanced insights help Partners refine their technical approach and
strengthen funding applications, accelerating the funding approval process.`

So of course, we took a look.

### AI suggested MRR

Scenario 1: We edited an existing ACE opportunity which had an arbitrary MRR (it was a professional services 
opportunity, where MRR is extremely rubbery) and no service selections. Our suggested MRR for this opportunity was $480. 

Somehow, AI decided that $372 was more appropriate. Given there was no service selections and it was pro serv, 
this seems pretty random.

So we tried it with a new ACE opportunity with the same title/description/customer/solution and arbitrary MRR $500.
Somehow, AI decided this one should have been $480.

Wierd.

Scenario 2: Again we edited an existing ACE opportunity with an educated MRR (it was a bundled proserv + infra
opportunity, with service selections. There were similar ACE opportunities already closed lost and launched,
all linked to the same solution

The MRR was $750. AI decided that $926 was more appropriate. 

Comparatively, the average MRR of closed lost and launched opportunities for scenario 2 was $750. So somehow,
AI decded that this one should be bigger. The only factor we can put it down to is perhaps something from
the customer's profile which influences the upgrade.

Scenario 3: We created a "moderately well described" ACE opportunity with a $1 MRR. 
AI decided that $230 was more appropriate.

Our take aways from this:
- x
- y
- z

### Importing Pricing Calculator URLs

tbc

Our take aways from this:
- x
- y
- z

### Learnings, better practices reinforced

- Reinforces the practice of ACE opportunities being (extensively) tagged with service selections. We wrote about this earlier ...
  
## The wrap up

Text

[Back to awyspr fieldnotes index](https://fieldnotes.awyspr.com)
