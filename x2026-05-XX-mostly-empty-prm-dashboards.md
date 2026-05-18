<a href="https://awyspr.com/"><img src="https://awyspr.com/assets/images/image07.svg?v=b4a015c2" width="10%" height="10%" align="left"></a>

# Mostly empty PRM dashboards

2026-05-01

## What's this one all about then ?

In the drip feed of features around Partner Revenue Measurement, AWS yesterday released its [Attributed Revenue Dashboard](https://docs.aws.amazon.com/partner-central/latest/getting-started/partner-analytics-attributed-revenue.html).

As it says on the label:

The Attributed Revenue dashboard provides visibility into the AWS revenue impact of your solutions as measured by Partner Revenue Measurement (PRM). The dashboard displays aggregated monthly attributed revenue by Partner product, AWS service, and billing period.

Sounds good ? There are a few gotchas.

### Headline data

### Our investigation

Lets start with the first question any reasonable person will ask - where's my data and when does it get updated ?

So here's the bad news:

"Revenue data is updated 45 days after the month end for the previous billing month."

That means that we won't see data for April 2026 until mid June 2026. A 6 week delay (assuming you have tags in place at the end of April).
... Meanwhile you can get "day by day" attributed cost from Cost Explorer for a tag or set of tags if you have tagged up your workloads.

And if you've not crossed the "apply PRM tags" bridge yet, the delay will be 6 weeks after the end of the first month you've tagged something.

Here's another bit of not quite good news:

"Partners have visibility to aggregated attributed revenue data at the product and AWS service level."

Product here means "AWS Marketplace Listing Product Code", ie the magic ```pc:XXXXXXXXXX``` value that sits 
against the ```aws-apn-id``` key. Service here means "AWS Service", ie the SKU-based item that is provisioned or consumed.

The obvious question is whether you can slice and dice this product and service level data by customer.

???


## The wrap up

Text

[Back to awyspr fieldnotes index](https://fieldnotes.awyspr.com)
