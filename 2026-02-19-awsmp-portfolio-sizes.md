<a href="https://awyspr.com/"><img src="https://awyspr.com/assets/images/image07.svg?v=b4a015c2" width="10%" height="10%" align="left"></a>

# Does Marketplace Portfolio Size Matter ?

2026-02-19 (updated 2026-07-23)

## What's this one all about then ?

We've recently been doing some more analytics type work over AWS Marketplace as a community of sellers and products.
We're certainly not new to the game in terms of appreciating the size and scale of some sellers and their product portfolios -
there are a number of public examples of sellers with $1B+ cumulative revenue via Marketplace and a smaller but growing number of
$1B ARR through Marketplace which tells you something about size and scale.

But our understanding has been recalibrated recently with some "outlier" discoveries - where there are sellers with hundreds of
listings. 

## Our (somewhat incorrect) assumptions

We'd assumed prior to this, and based on a few years of experience in working with different sized/shaped AWS partners with Marketplace 
presence that the curve was something like this:

- 75% of AWSMP sellers have 1 product
- 15% of AWSMP sellers have 2-5 products
- 5% of AWSMP sellers have 5-10 products
- 2.5% of AWSMP sellers have 10-25 products
- 1.25% of AWSMP sellers have 25-100 products
- 0.625% of AWSMP sellers have 100-200 products
- 0.625% of AWSMP sellers have 200+ products

Thats a classic long tail distribution, or close enough. We'd never seen actual evidence of the 100+ product sellers, it was a hunch.

## The Data

In our work recently we have been working with a body of about 2500-3000 AWS sellers with a Marketplace presence.
Thanks to the wonders of observability, we came across a few things that stood out in terms of portfolio sizing.

This is by no means a scientific survey, its anecdotal and based on seeing outliers in the data we have
been working with. 

### The Real Big Guns

- First up (best you be sitting down, or leaning against something solid) the seller called [Next Move Strategy Consulting ](https://aws.amazon.com/marketplace/seller-profile?id=seller-juefjvns2luuk) ... drum roll ... *633* public Marketplace entries in July 2026, up from *457* back in February 2026 when we first did the analysis. (That is not a typo, hit the link and see for yourself. This is the biggest we have ever seen, although if you know a seller with more, please drop us a line and we'll update.) 

If you look at NMSC's website ... it seems "a bit unusual" as they are not really a technology vendor but a market research firm, their LinkedIn tells a similar story (with "51-100" employees, the Marketplace listing to staff member ratio is around 4-5 listings per person ??). A fair number of their products are "free" data products - which makes more sense. Regardless they have have hit the Marketplace publish button a whole heap of times to get to this point.

- [Bitnami by VMWare](https://aws.amazon.com/marketplace/seller-profile?id=dbe6480c-fd0d-4625-9bd0-44606ed33fa6)
This seller has *292* public Marketplace entries ... We'd spotted them earlier than NMSC above, and thought close to 300 was already
ridiculous but understanding their business model with OSS AMIs at the core, it wasn't a number that you could see as impossible, just unlikely.

- [ProComputers](https://aws.amazon.com/marketplace/seller-profile?id=cb14f0b8-1ca0-4485-bc79-a2cb2b9a4feb)
This seller has *288* public Marketplace entries. Similar approach to Bitnami.

- [rearc](https://aws.amazon.com/marketplace/seller-profile?id=a8a86da2-b2d1-4fae-992d-03494e90590b)
This seller has 206 public Marketplace entries, dominated by data sets (eg ADX).

### The Not-Quite-So-Big Guns

- [kCloudHubs LLC](https://aws.amazon.com/marketplace/seller-profile?id=seller-kuxjetipx54va)
This seller has 127 public Marketplace entries ... This seemed quite a large number until we found NMSC and Bitnami and ProComputers and rearc.

- [Deloitte Consulting LLP](https://aws.amazon.com/marketplace/seller-profile?id=seller-qkumbjysee36y)
This seller has 126 public Marketplace entries ... Again this seemed quite a large number until we found NMSC and Bitnami and ProComputers and rearc.

- [ATH InfoSystems](https://aws.amazon.com/marketplace/seller-profile?id=d5fbea8c-b245-4d44-9bbe-42f583e64b54)
This seller has 99 public Marketplace entries ...

- [IBM Software](https://aws.amazon.com/marketplace/seller-profile?id=345ea612-6e57-4b07-b5a9-f5747652c4ee)
This seller has 92 public Marketplace entries ...

- [Canonical Group Limited](https://aws.amazon.com/marketplace/seller-profile?id=565feec9-3d43-413e-9760-c651546613f2)
This seller has 82 public Marketplace entries ...

- [WolkenHai](https://aws.amazon.com/marketplace/seller-profile?id=seller-ipgeizbfr7yrk)
This seller has 63 public Marketplace entries ... but they are a publisher-facilitator so most of them are under their seller
profile but actually come from other companies they are contracted for

- [Waltsoft](https://aws.amazon.com/marketplace/seller-profile?id=4bf1a800-d6fc-4c1f-8e88-76ef2dbfb77c)
This seller has 58 public Marketplace entries ...

- [Accenture](https://aws.amazon.com/marketplace/seller-profile?id=4fe793cb-71be-4e10-894c-037dd798e603)
This seller has 55 public Marketplace entries ...

- [NTT Data](https://aws.amazon.com/marketplace/seller-profile?id=30e14a08-5285-42ef-8f0b-5ba04b7ec0fe)
This seller has 52 public Marketplace entries ...

### The Really-Quite-Small Guns

We had to draw the line somewhere, the ones below are still significant but they are clearly
not in the same weight division as the ones in the earlier sections.

- [Incedo](https://aws.amazon.com/marketplace/seller-profile?id=seller-l3wixqx4jffqq)
This seller has 49 public Marketplace entries ...

- [Kyndryl](https://aws.amazon.com/marketplace/seller-profile?id=268da0a8-95a0-442d-92d0-14e40517f09c)
This seller has 41 public Marketplace entries ...

- [Presidio](https://aws.amazon.com/marketplace/seller-profile?id=a844a964-a83a-4e77-83c1-069ab227cb94)
This seller has 37 public Marketplace entries ...

- [EPAM Systems](https://aws.amazon.com/marketplace/seller-profile?id=seller-3eodbqclk7nhu)
This seller has 35 public Marketplace entries ...

- [Sigmoid Analytics](https://aws.amazon.com/marketplace/seller-profile?id=5303d42a-b307-47fa-8fee-e03588511953)
This seller has 33 public Marketplace entries ...

- [TTEC Digital](https://aws.amazon.com/marketplace/seller-profile?id=6e058ead-a758-4f34-8e53-90001832b8f2)
This seller has 31 public Marketplace entries ...

- [InfoSys](https://aws.amazon.com/marketplace/seller-profile?id=b5861500-168b-4fed-9170-102ed06a9641)
This seller has 27 public Marketplace entries ... They hardly even warrant a mention!

## Observations

A few things stand out from this list (again, noting its not a scientific sample, its just a big enough sample to have
some confidence in).

1. Systems Integrators / Consulting Partners tend to have the larger catalogs of Marketplace listings, compared to ISVs.
2. Technology companies that are in the business of shipping images based around open source software are also quite prevalent.
3. Bigger portfolios are mostly bundles of product and service (not claiming "multi-product solutions", but rather a solution which
has both technology product and human effort involved in delivery)
4. There are specialist data set publishers (via Data Exchange) that have larger portfolios of different data sets.

Its completely possible that there are other examples of sellers with even larger portfolios
of listings; or its possible (but unlikely) we've just stumbled across the biggest, and our original view
about the long tail distribution remains valid.

## Potential Bias
These numbers are interesting enough, but consider: 

- Some of these are likely public vs private offer listing stubs - its not uncommon that sellers have
a headline public offer listing and a separate listing for private offers (even though you don't need this, and can
enable Request Private Offer on any listing)
- These counts are for public Marketplace entries, and its not uncommon for sellers to have limited entries 
which are only accessible via [Private Offer](https://docs.aws.amazon.com/marketplace/latest/buyerguide/buyer-private-offers.html) or [geographic constraints](https://aws.amazon.com/blogs/awsmarketplace/aws-marketplace-launches-geo-fencing-to-enable-sellers-to-control-availability-by-country/). We could reasonably imagine these
totals might be boosted by 10-25% if the portfolios were even partially matched with limited entries.

## Practical implications of managing Marketplace portfolios at this size/scale
Now being somewhat "in the game" of helping AWS partners put Marketplace entries together and then back them with co-sell motions
there's a few things that make us wonder about listing portfolios of this size:

- The complexity of managing limited pairs for public entries (a common model)
- The challenge of ensuring content consistency and updates across a portfolio of 50+ listings (most smaller scale sellers find
this hard enough, and automation solutions don't necessarily help a lot)
- The logic and consistency of linking AWSMP entries to ACE opportunities (optional but extremely helpful in the co-sell world, but has
to be done manually at the moment)
- The unlikely scenario of every listing actually generating offers, let alone revenue
- Systems integration/coordination challenge to applying Partner Revenue Measurement tagging for every product code

## The wrap up

As we said a few times, this is definitely not science but it is observation on a sizeable data set. Of course, AWS themselves 
know all the numbers (but as usual they don't give many away). 

[Back to awyspr fieldnotes index](https://fieldnotes.awyspr.com)
