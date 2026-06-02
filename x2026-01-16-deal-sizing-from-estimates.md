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

### AI-suggested MRR

First of all, we just looked at the AI-suggested MRR based on the opportunity.

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

Comparatively, the average MRR of closed lost and launched opportunities for scenario 2 was $725. So somehow,
AI decied that this one should be bigger. The only factor we can put it down to is perhaps something from
the customer's profile which influences the upgrade.

Scenario 3: We created a "moderately well described" ACE opportunity with a $1 MRR. 
AI decided that $230 was more appropriate.

Scenario 4: We created a "moderately well described" ACE opportunity for software sale via AWSMP, and gave it an 
MRR based on 100 users x the vendor's public AWSMP pricing of $35 per user per month - so MRR $3,500.

AI decided that it should be $22,800. Yes, thats right, about 8x larger. We think it picked the enterprise license
which is advertised on AWSMP public pricing at $25,000 as the base and somehow discounted it.

Our take aways from this:
- The AI-suggested MRR ranges from reasonable to something which is very unreasonable.
- It appears that the AI MRR suggesting mechanism is influenced by a range of factors, including the partner's similar
opportunities, the customer's opportunity history, scale indicators in the description of the opportunity, the service
selection mix, and AWSMP public pricing.
- Compare your own hand-developed MRRs against AI, but don't ever take the lazy default of accepting its recommendation. If 
the MRR on an ACE opportunity is 'maleable', at least you know what went into that, with AI, you have no idea of the provenance.

### Importing Pricing Calculator URLs

Next, we used the pricing calculator import

Scenario 1: a moderately well specified calculator against a well defined solution with linked services - completing most options to completely define a classic 3 tiered web data ingest and analyse application (Amplify, RDS, S3, Glue, Athena, EC2 Fargate, Lambda, Quicksight). The pricing calculator came in at MRR $183, and we imported it into the ACE opportunity.

AI-adjusted it was recommended to be MRR $192. That's pretty close although given that it was well specified, its not clear where the 2-3% bump came from.

Scenario 2: a sparsely specified calculator vs a well defined solution with linked services - a bare bones S3, EC2, RDS. The pricing calculator came in at MRR $53, and we imported it into the ACE opportunity.

AI-adjusted it was recommended to be MRR $134. That wasn't what we expected, we thought AI would bump the number up, realising that the solution specification was larger - not least we had selected a few services for the opportunity that were not represented in the pricing calculator.

Our take aways from this:
- Even w
- y
- z

### Learnings, better practices reinforced

- Reinforces the practice of ACE opportunities being (extensively) tagged with service selections. We wrote about this earlier ...

### Mysteries

- How is partner provided MRR going to sit alongside AI-suggested MRR in internal AWS seller systems ? Its a logical thing to do,
and AWS internal systems already have various weightings and scorecards applied to partner opportunities to support resource allocation and
stack ranking.
  
## The wrap up

A lot of vendors have introduced AI opportunity sizing support, but few with as diverse a portfolio as AWS, let alone a portfolio
that mixes products and services, and a marketplace.


[Back to awyspr fieldnotes index](https://fieldnotes.awyspr.com)
