<a href="https://awyspr.com/"><img src="https://awyspr.com/assets/images/image07.svg?v=b4a015c2" width="10%" height="10%" align="left"></a>

# AWSMP Discovery API - what you get and what you don't

2026-04-13 

## What's this one all about then ?

So the obvious thing to do with the AWSMP Discovery API was to compare it to the browser UI/UX and 
see what was the same or different.

### Whats here and what isnt ? 
Lets take search first then product.

For search, we'll put in a query, lets say "XX"

Now lets look at the left hand menu, which is categories. Disco API allows you to get this info 
back, or preset/navigate/select from it using https://docs.aws.amazon.com/marketplace/latest/APIReference/API_marketplace-discovery_SearchFacets.html - thats a tick. While that left hand menu content "seems" trivial to 
scrape with a one page load and a DOM parser, its generally better not to go down that path if 
you need to work with that data when you can get it back as JSON. Assuming of course you have 
an AWS account and a user with the right IAM permissions to call the Disco API (see our earlier post).

Counter point, in the browser, we get an AI summary of the result set "sometimes" (when there's 
"reasonable" commonality between results, rather than it being a true mixed bag. That summary 
isn't available over the Disco API. here's what you're missing: [IMG]

For product, we can again either select an item off the search or just pass in the prodview- ID 
if we know what it is. Doesn't matter how we do this, so lets just pick one. https://aws.amazon.com/marketplace/pp/prodview-brb73nceicv7u will do.

AWSMP Discovery API and using https://docs.aws.amazon.com/marketplace/latest/APIReference/API_marketplace-discovery_GetProduct.html and https://docs.aws.amazon.com/marketplace/latest/APIReference/API_marketplace-discovery_GetListing.html 
allows us to get back most of the info that appears on the page, which is helpful because DOM 
parsing it out from a scrape isn't that pleasant.

But whats missing - compared to the browsing experience - are these two pieces: 

* Similar Products - there's nothing on the Disco API for this part. You're missing this 
section with the Disco API: [IMG]

* Customer Reviews - you can get the reviews metadata (eg counts, sources as a part of XXX), 
but not the actual reviews. Here's what you're missing: [IMG]

Now in both cases - the missing bits for search, its probably fair to say that most programmatic 
interactions with AWSMP via Discovery API are not likely to be looking for the AWSMP-provided AI summary/overview. 
If you're building some kind of overlay on AWSMP though, its pretty likely your users are going to 
care about similar products and about actual customer reviews (rather than just the counts).

_MORE NOTES HERE_

## The wrap up

The availability of the AWS Marketplace Discovery API unlocks a heap of new possibilities 
in terms of sourcing, embedding, analysing marketplace data and interacting with AWS Marketplace 
from other surfaces like CRMs. There's still gaps, but we're getting a lot closer to a world where 
a system programmatically work with the Marketplace surface at the same breadth and depth that a user can.

[Back to awyspr fieldnotes index](https://awyspr.github.io/awyspr-fieldnotes)




NOTES:

What the API does NOT provide: Ranked search position (no rank integer in response — sorting by RELEVANCE exists but no per-item rank), AI overview text, screenshots, seller bio/profile body, seller catalog product list, AgentMode results, individual review text, product overviewText (the long-form prose block), the AWSMP prodviewId URL slug directly (unconfirmed until spike runs).

seller profile is linkable, but there is no discovery API equivalent of "who is this seller" which you can get with 1 click on the UI.
