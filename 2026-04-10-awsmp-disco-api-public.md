<a href="https://awyspr.com/"><img src="https://awyspr.com/assets/images/image07.svg?v=b4a015c2" width="10%" height="10%" align="left"></a>

# AWS Marketplace Discovery API is now public

2026-04-10

## What's this one all about then ?

In a notable dispatch from AWSMP HQ this week, the previously limited-access [AWS Marketplace Discovery 
API is finally public](https://docs.aws.amazon.com/marketplace/latest/APIReference/discovery-apis.html)

### So whats in the box ?

We got a few things this time around:

"The AWS Marketplace Discovery API is now available. Added 9 API operations: GetListing, GetProduct, 
GetOffer, GetOfferTerms, GetOfferSet, ListPurchaseOptions, ListFulfillmentOptions, SearchFacets, and 
SearchListings. Standard AWS SDK support and IAM-based access."

That sounds promising, but the devil is in the detail - to what extent can you scope or constrain those 
operations and what type of information comes back in the payload.

Open questions we're going to look into:

* Does a Discovery API call return all of the content thats on the web search version when a user hits up AWSMP 
in a browser ? If not, whats missing ?
* Does a Discovery API call return the same list, order etc of search results as the web interface ? If not, 
what's different, can we find (and perhaps understand) a pattern ?

## The wrap up

The availability of the AWS Marketplace Discovery API unlocks a heap of new possibilities in terms of 
sourcing, embedding, analysing marketplace data and interacting with AWS Marketplace from other surfaces 
like CRMs. It will take a little while to work out whether its functionally or content wise the same, but 
meanwhile, its open for anyone who wants it.

[Back to awyspr fieldnotes index](https://awyspr.github.io/awyspr-fieldnotes)

