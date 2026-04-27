<a href="https://awyspr.com/"><img src="https://awyspr.com/assets/images/image07.svg?v=b4a015c2" width="10%" height="10%" align="left"></a>

# Attributed Revenue Dashboards - almost completing the PRM puzzle

2026-04-22

## What's this one all about then ?

The previously flagged "PRM Dashboards" for partners were 
[released today](https://aws.amazon.com/blogs/apn/unlock-revenue-insights-in-the-new-attributed-revenue-dashboard/), 
available in PartnerCentral (v3, in Console) under the Partner Analytics > Attributed Revenue item.

### First pass

A quick look shows the following:
* A headline - count of products measured, services measured and attributed revenue
* 3 widgets - showing different revenue alignments 
* 1 widget - showing origin of data 

### Attributed revenue

The first 3 widgets are: 
* AWS attributed revenue by product
* AWS attributed revenue by service
* AWS attributed revenue (total, presumably)

they only get data updated on 15th of each month, apparently, so since its 22 April, they are all empty and 
we won't see anything until 15 May - even though we tagged resources way back in February when PRM was first 
announced as a requirement. 

(Also rumour has it that there's a minimum number of resources to be tagged for which revenue is attributed 
before data will appear - customer anonymization is apparently the explanation but to be honest that sounds 
a bit wierd - if its our customer and its workload we create/manage for the customer, its workload that we can 
see costs for in Cost Explorer either directly because its on an Account in our Organization, or its accessible 
and aggregated from customer held Accounts via IAM Billing permissions or via Billing Transfer then surely we 
should see the revenue here too ??).

### Onboarding status

The 4th (bottom) widget shows a partner's products and corresponding AWS services enabled for Partner Revenue 
Measurement, aka "onboarding status". 

If you have tagged resources via one means or another, you can see the link between the AWSMP listing, its 
product code, the AWS service and a source (of the tag - Resource Tag, User Agent, Metering). You can't see 
the actual workload that makes up the tag .... for that you'll need to use Resource Explorer (to get actual 
resources) or Cost Explorer (in Billing & Cost Management, to get actual $).

## The wrap up

PRM has been socialised with partners as being a foundation layer on which other future items (like funding 
entitlements, funding apportionment, partner stack-ranking, presumably other program eligibility) is based. 
It still needs a bit of work - lets hope that the missing pieces are found before too much is built on top.

[Back to awyspr fieldnotes index](https://fieldnotes.awyspr.com)
