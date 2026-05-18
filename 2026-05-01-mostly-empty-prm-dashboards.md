<a href="https://awyspr.com/"><img src="https://awyspr.com/assets/images/image07.svg?v=b4a015c2" width="10%" height="10%" align="left"></a>

# Mostly empty PRM dashboards

2026-05-01

## What's this one all about then ?

In the drip feed of features around Partner Revenue Measurement, AWS yesterday released its [Attributed Revenue Dashboard](https://docs.aws.amazon.com/partner-central/latest/getting-started/partner-analytics-attributed-revenue.html).

As it says on the label:

_"The Attributed Revenue dashboard provides visibility into the AWS revenue impact of your solutions as measured by Partner Revenue Measurement (PRM). The dashboard displays aggregated monthly attributed revenue by Partner product, AWS service, and billing period."_

Sounds good ? There are a few gotchas.

## Headline functionality and data

#### Filters
The Attributed Revenue dashboard incorporates the following filtering capabilities for analyzing your attributed revenue data:
- Time Frame: Select a date range to view attributed revenue for specific billing periods.
- Product Name: Filter by one or more of your AWS Marketplace product listings to view revenue for specific products.
- AWS Service: Filter by specific AWS services (for example, Amazon EC2, Amazon S3, Amazon RDS) to understand which services your solutions drive consumption for.
- AWS Account ID: Filter by specific AWS account IDs to view revenue associated with an account.

### Key metrics
The dashboard displays three key metrics at the top of the page:
- Products Measured: The number of your AWS Marketplace products that have attributed revenue measured by Partner Revenue Measurement during the selected time frame.
- AWS Services Measured: The number of distinct AWS services where your products are driving consumption during the selected time frame.
- Total Attributed Revenue: The total aggregated revenue measured by Partner Revenue Measurement across all your products and AWS services during the selected time frame.

### Charts
- Attributed Revenue by Product: This chart displays month-over-month attributed revenue for each of your AWS Marketplace products. Each product is represented as a separate series, allowing you to compare revenue trends across your product portfolio over time. Use this chart to identify which products are driving the most AWS consumption and monitor growth patterns.
- Attributed Revenue by AWS Service: This chart displays attributed revenue by AWS service. Use this chart to understand which AWS services your solutions drive the most consumption for and how service-level revenue trends change over time.

### Tables
- Attributed Revenue: This table shows attributed revenue measured by Partner Revenue Measurement capabilities aggregated by Partner product and AWS service.
- Onboarding Status: This table shows your products that are enabled with any of the Partner Revenue Measurement capabilities. Use this table to verify that your PRM implementation is active and to identify products that may need additional configuration.

### Our investigation

Lets start with the first question any reasonable person will ask - where's my data and when does it get updated ?

So here's the bad news:

_"Revenue data is updated 45 days after the month end for the previous billing month."_

That means that we won't see data for April 2026 until mid June 2026. A 6 week delay (assuming you have tags in place at the end of April).
... Meanwhile you can get "day by day" attributed cost from Cost Explorer for a tag or set of tags if you have tagged up your workloads.

And if you've not crossed the "apply PRM tags" bridge yet, the delay will be 6 weeks after the end of the first month you've tagged something.

Here's another bit of not quite good news:

_"Partners have visibility to aggregated attributed revenue data at the product and AWS service level."_

Product here means "AWS Marketplace Listing Product Code", ie the magic ```pc:XXXXXXXXXX``` value that sits 
against the ```aws-apn-id``` key. Service here means "AWS Service", ie the SKU-based item that is provisioned or consumed.

The obvious question is whether you can slice and dice this product and service level data by customer. The filter suggests you might: 

_"AWS Account ID: Filter by specific AWS account IDs to view revenue associated with an account."_ 

But in practice this means your own partner accounts, ie in your AWS Organization. If you've deployed workload into an account that is outside your AWS organization, then its invisible, even if you have IAM rights or Billing Transfer turned on. If you're a multi-tenant SaaS company this works, but if you are an AMI company then you're out of luck here. 

The better news is that the Onboarding Status table works regardless of the delay in Attributed Revenue, ie within 24 hours of a resource being tagged. We wonder why its not at the top of the page - because unless you have onboarded products by tagging with a code, then nothing else will work ... and if you have a portfolio of products/services on AWS Marketplace you're going to need to do this a few times over to get coverage.

## The wrap up

PRM is clearly an emerging capability - we've seen the tagging side extended from resource tags to metering and user agents over the last few months, and we'd expect the Attributed Revenue Dashboards to similarly evolve, particularly after the 31 July deadline when "any form of PRM" is required by a partner to continue to qualify for funding.

[Back to awyspr fieldnotes index](https://fieldnotes.awyspr.com)
