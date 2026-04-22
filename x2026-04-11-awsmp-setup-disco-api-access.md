<a href="https://awyspr.com/"><img src="https://awyspr.com/assets/images/image07.svg?v=b4a015c2" width="10%" height="10%" align="left"></a>

# Setting up AWSMP Discovery API access

2026-04-11

## What's this one all about then ?

So if you were following along the new AWSMP Discovery API trail you might have noticed that its got [access control](https://docs.aws.amazon.com/marketplace/latest/APIReference/discovery-api-access-control.html).

In practice what this means is:

1. Ask your AWS systems team to create an IAM user specific to the AWSMP Discovery API, and put it in a group for the same purpose. You can add extra permissions to an existing IAM user, but generally thats considered a bit dangerous as you can end up accumulating all kinds of permissions over time.

2. Create an access key pair for the account, there's two items that result from this - the AWS Access Key ID and the AWS Secret Access Key. (No, we won't paste ours here here for you!)

3. Ask your AWS systems team to create an IAM group specific to the AWSMP Discovery API, and add the IAM user from step 1 into that group. Putting a user into a group and adding a policy to a group is better practice than attaching permissions or policies directly - I digress.

4. Ask your AWS systems team to review the Discovery API access control requirements for the group from step 3, they can find the details [here](https://docs.aws.amazon.com/marketplace/latest/APIReference/discovery-api-access-control.html) The permissions are read-only but allow the following:

* ```GetListing``` – Grants permission to retrieve information about a listing.
* ```GetProduct``` – Grants permission to retrieve information about a product.
* ```GetOffer``` – Grants permission to retrieve information about an offer.
* ```GetOfferTerms``` – Grants permission to retrieve terms for an offer.
* ```GetOfferSet``` – Grants permission to retrieve information about an offer set.
* ```ListPurchaseOptions``` – Grants permission to list purchase options available to the buyer.
* ```ListFulfillmentOptions``` – Grants permission to list fulfillment options for a product.
* ```SearchListings``` – Grants permission to search for product listings.
* ```SearchFacets``` – Grants permission to retrieve facet values for filtering listings.

So its read only. Its a subset of the AWS Managed policy for [MarketplaceRead-Only](https://docs.aws.amazon.com/marketplace/latest/buyerguide/buyer-security-iam-awsmanpol.html#security-iam-awsmanpol-awsmarketplaceread-only), but cut down just to the forward facing components, none of the transactional access.

4. Apply the actual IAM policy to the group, again [from the docs](https://docs.aws.amazon.com/marketplace/latest/APIReference/discovery-api-access-control.html):

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "aws-marketplace:GetListing",
                "aws-marketplace:GetProduct",
                "aws-marketplace:GetOffer",
                "aws-marketplace:GetOfferTerms",
                "aws-marketplace:GetOfferSet",
                "aws-marketplace:ListPurchaseOptions",
                "aws-marketplace:ListFulfillmentOptions",
                "aws-marketplace:SearchFacets",
                "aws-marketplace:SearchListings"
            ],
            "Resource": [
                "arn:aws:aws-marketplace:::catalog/<catalog-name>/product/*",
                "arn:aws:aws-marketplace:::catalog/<catalog-name>/listing/*",
                "arn:aws:aws-marketplace:::catalog/<catalog-name>/offer/*",
                "arn:aws:aws-marketplace:::catalog/<catalog-name>/offerSet/*",
                "arn:aws:aws-marketplace:::catalog/<catalog-name>/purchaseOption/*"
            ]
        }
    ]
}
```

6. Quite reasonably, your AWS systems folk will want to know how to test/prove, here's a simple suggestion to use the AWS CLI.

First make sure its a very recent copy of AWS CLI, since the ```marketplace-discovery``` method is only just released. We're using ```aws-cli/2.34.30``` if that helps :-)

Then:

```
# Configure the profile once 
aws configure --profile drata-search 
# (enter AWS Access Key ID, AWS Secret, default region: us-east-1, output: json) when prompted 

# Execute the search 
aws marketplace-discovery search-listings \ 
--profile drata-search \ 
--region us-east-1 \ 
--search-text "Drata"
```

Like many AWS integration services for PartnerCentral and Marketplace, the Discovery API only works in ```us-east-1```, so make sure your systems team tests it there. And make sure its not having a hiccup at the time ...

The ```IntegrationId``` is the one wierd bit for this API. Allegedly according to docs you need to include it (does not matter what the value is, just not zero), but our testing suggests its not supported by the ```marketplace-discovery``` method - wierd.

Systems folks should get back something like this:

```
{
    "listingSummaries": [
        {
            "listingId": "prodview-3xw4sjqv2pb22",
            "listingName": "Drata Security & Compliance Automation Platform",
            "publisher": {
                "sellerProfileId": "f717f717-faab-4726-bb7f-b09cbac8508c",
                "displayName": "Drata"
            },
            "catalog": "AWSMarketplace",
            "shortDescription": "An AWS Security Competency Partner, Drata is a GRC solution that enables companies to continuously monitor security and compliance controls, automatically collect evidence needed for an audit, and manage and remediate risk. Drata also allows you to share your real-time compliance posture with prospects and customers to build trust and accelerate growth.",
            "logoThumbnailUrl": "https://d7umqicpi7263.cloudfront.net/img/product/ef9576fc-b0ca-4fe6-99d1-c84db6785107.com/d3509d5b0e23957146ac186105784e8d",
```

... and a whole bunch more. Regardless of the rest, if they get back the first bit, its working.


## The wrap up

There's a bit of fiddling with this as its an IAM access controlled API; which is normal for AWS infrastructure but often a bit beyond what a partner alliance lead or team member might have to deal with. That relationship you established with your AWS systems folk when you got PartnerCentral migrated over to the Console will be something you keep coming back to. But basically the Marketplace Discovery API works if you've got the right permissions on the account. So now we can have some fun!

[Back to awyspr fieldnotes index](https://awyspr.github.io/awyspr-fieldnotes)
