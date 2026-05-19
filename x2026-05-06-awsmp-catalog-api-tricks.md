<a href="https://awyspr.com/"><img src="https://awyspr.com/assets/images/image07.svg?v=b4a015c2" width="10%" height="10%" align="left"></a>

# AWSMP Catalog API Tricks

2026-05-06

## What's this one all about then ?

~4 May finding the offer ID for a draft listing (aka Bhagirath call)

### DUMP

1) There is reference code and many many changeset examples for AWSMP available in Java and Python at:

https://github.com/aws-samples/aws-marketplace-reference-code/tree/main/java
https://github.com/aws-samples/aws-marketplace-reference-code/tree/main/python

There are things in the changeset examples which are not completely described in the AWSMP API documentation :-)

2) Getting the offer ID for a product - you need to do this before attempting to attach things like terms, and it exists for a draft product listing as well as a released one. You can use the list-entities method:
# A. Get public offer ID for the AWSMP listing

``OFFER_ID=$(aws marketplace-catalog list-entities \ --region "$REGION" \ --catalog AWSMarketplace \ --entity-type Offer \ --entity-type-filters '{ "OfferFilters": { "ProductId": { "ValueList": ["'"$PRODUCT_ID"'"] }, "Targeting": { "ValueList": ["None"] }, "State": { "ValueList": ["Released"] } } }' \ --query 'EntitySummaryList[0].EntityId' --output text) echo "Offer: $OFFER_ID"`` 

Gotchas here are: 
* Targeting=None will retrieve public (any account) offers, Targeting=BuyerAccounts will retrieve data only for nominated accounts.
* State=Released - if you have not used the ReleaseOffer method to make the offer available (normal case when you are creating a new product) then you need to set State=Draft. Omitting the State defaults to retrieving only Released offers.

#B. Get full offer document for that offer ID
``aws marketplace-catalog describe-entity \ --region "$REGION" \ --catalog AWSMarketplace \ --entity-id "$OFFER_ID"``

3) Public vs Private offers
Only a public offer exists by default (and you can get the offer ID as above). 

A private offer only exists because you combine a product and a target account and use ReleaseOffer to publish it. Unlike for a public offer, there is no draft state - it either exists or it does not. So if you want to work with a private offer you have a one-shot to create then release it.

4) Setting things like SupportTerms, LegalTerms, Targeting
Getting the public offer ID from 2A is the trick because you can only attach SupportTerms,LegalTerms,Targeting to an offer ID.

#4A update the support terms = refund policy

``OFFER_ID="offer-xxxxxxxxxxxxx"
aws marketplace-catalog start-change-set \ --region us-east-1 \ --catalog AWSMarketplace \ --change-set "$(cat <<JSON [ { "ChangeType": "UpdateSupportTerms", "Entity": { "Type": "Offer@1.0", "Identifier": "$OFFER_ID" }, "DetailsDocument": { "Terms": [ { "Type": "SupportTerm", "RefundPolicy": "Pro-rata refund within 30 days of subscription start. Contact support@company.com to initiate." } ] } } ] JSON )"``

Gotcha: the thing called SupportTerm in AWSMP is actually the refund policy. If you want to update the SupportDescription, its a different call:

#4B update support description via UpdateInformation

OFFER_ID="offer-xxxxxxxxxxxxx"
aws marketplace-catalog start-change-set \ --region us-east-1 \ --catalog AWSMarketplace \ --change-set "$(cat <<JSON [ {{ "ChangeType": "UpdateInformation","Entity": { "Type": "SaaSProduct@1.0", "Identifier": "prod-xxx" } "DetailsDocument": { "SupportDescription": "24x7 at support@company.com..." } } ] } } ] JSON )" ```

#4C update legal terms

``OFFER_ID="offer-xxxxxxxxxxxxx"
# --- Custom EULA (your own document hosted at a stable URL) -----------------
aws marketplace-catalog start-change-set \ --region us-east-1 \ --catalog AWSMarketplace \ --change-set "$(cat <<JSON [ { "ChangeType": "UpdateLegalTerms", "Entity": { "Type": "Offer@1.0", "Identifier": "$OFFER_ID" }, "DetailsDocument": { "Terms": [ { "Type": "LegalTerm", "Documents": [ { "Type": "CustomEula", "Url": "https://your-bucket.s3.amazonaws.com/eula/v3.pdf" } ] } ] } } ] JSON )"``

#4D updating targeting

This is a little bit different because targeting exists in two forms

* on the product eg SaaSProduct@1.0 = Allowlist of AWS accounts that can see the product while it's in Limited state (preview before Public). Irrelevant once visibility goes Public.

* on the offer eg Offer@1.0Who can see/buy the offer. Combines BuyerAccounts (private) and/or CountryCodes (geo).

Assuming you want to set it on the product:

``aws marketplace-catalog start-change-set \ --region us-east-1 --catalog AWSMarketplace \ --change-set '[{"ChangeType":"UpdateTargeting","Entity":{"Type":"SaaSProduct@1.0","Identifier":"'"$PRODUCT_ID"'"},"DetailsDocument":{"PositiveTargeting":{"BuyerAccounts":["111122223333","444455556666"]}}}]'``

Assuming you want to set the offer:

``OFFER_ID="offer-xxxxxxxxxxxxx"
# Geo restriction: allow only AU, NZ, US, CA (positive allowlist)
aws marketplace-catalog start-change-set \ --region us-east-1 --catalog AWSMarketplace \ --change-set "$(cat <<JSON [ { "ChangeType": "UpdateTargeting", "Entity": { "Type": "Offer@1.0", "Identifier": "$OFFER_ID" }, "DetailsDocument": { "PositiveTargeting": { "CountryCodes": ["AU", "NZ", "US", "CA"] } } } ] JSON )"``

Last thing, about that setting dimensions and verification in UI, it seems like a UI flow validation error over an API-creation error.

You could verify if your addition has "stuck" properly using:

``aws marketplace-catalog describe-entity --entity-id $PRODUCT_ID --query 'DetailsDocument.Dimensions'``

If that comes back empty after you created the dimensions either via API or UI, then thats a problem.


Try these two working CLI wraps to simplify things. 1st one calls back the entities in an authenticated AWSMP publisher account, 2nd one uses one of those EntityIds to get extra detail. These are private offers for a proserv wrap, but I can make the same work for public and drafts, and for SaaS too.

MMM1-BADENH:~ badenh$ aws marketplace-catalog list-entities --region us-east-1 --catalog AWSMarketplace --entity-type Offer
{
    "EntitySummaryList": [
        {
            "Name": "XXXXXXXXXXXXX",
            "EntityType": "Offer",
            "EntityId": "offer-u2ss5wgupr4zs",
            "EntityArn": "arn:aws:aws-marketplace:us-east-1:676206901714:AWSMarketplace/Offer/offer-u2ss5wgupr4zs",
            "LastModifiedDate": "2026-04-14T05:18:44Z",
            "Visibility": "Private",
            "OfferSummary": {
                "Name": "XXXXXXXXXXXX",
                "ProductId": "prod-XXXXXXXXXX",
                "ReleaseDate": "2026-04-14T05:18:40Z",
                "AvailabilityEndDate": "2026-04-30T23:59:59Z",
                "BuyerAccounts": [
                    "XXXXXXXXXX",
                    "XXXXXXXXXX"
                ],
                "State": "Released",
}
MMM1-BADENH:~ badenh$ aws marketplace-catalog describe-entity --region us-east-1 --catalog AWSMarketplace --entity-id offer-u2ss5wgupr4zs
{
    "EntityType": "Offer@1.0",
    "EntityIdentifier": "offer-u2ss5wgupr4zs@2",
    "EntityArn": "arn:aws:aws-marketplace:us-east-1:XXXXXXXXXX:AWSMarketplace/Offer/offer-u2ss5wgupr4zs",
    "LastModifiedDate": "2026-04-14T05:18:44Z",
    "Details": "{\"Id\":\"offer-u2ss5wgupr4zs\",\"Name\":\"XXXXXXXXXX\",\"Description\":\"XXXXXXXXXX\",\"ProductId\":\"prod-XXXXXXXXXX\",\"Terms\":[{\"Type\":\"LegalTerm\",\"Documents\":[{\"Type\":\"CustomEula\",\"Url\":\"https://aws-mp-offer-legal-artifacts-us-east-1-prod.s3.amazonaws.com/offer-u2ss5wgupr4zs/d1f7d354-e5e0-44a7-b496-f443f0b1da50?X-Amz-Security-Token=IQoJb3JpZ2luX2VjELX%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJGMEQCICPOtrdiv3urg7FQnd9TLeMTSLxKgeBpKh3lxjFCLDYtAiAt0gU3uNPfN7WZ7NCZzOTpo3ovJdqZi%2Be9go2rA58%2BGyr9Awh%2BEAIaDDc0NjIzMDc0OTIyNCIMrgnE5u7lJyiNUv8HKtoDSi4z18h7MSFvyWSp7xRSZm0UA%2Bcw%2FP6zoOGeGu%2BV9vRt%2F3FtEIXqGFzBUA%2Bd2d2dq3M22%2BB3%2B6xrM%2FbXKhXbCpEnNpYQE6D8zoKuFTGJK2U88ifE86NbCIEA0V1RddLqKbFci679rCqIG0c6%2BNScf8c4zdESyXXWgXem%2Bg2Gl%2B2%2FrSWSh7sHiV9gxrzcT1TrJ81vn2juVWmzgGoufydcnWsIypSoU5tz5rPZDRGMXdQM0DpCthr7CYGMp2SoDiWWJb2qykSUtMsJ2iF9lMmp%2BhcmKRi6EsuBCnJUGUZo5NUsXNJe0euWKGpa7FY9njXo7%2FtqLu6mW5efXZ4RTedPfVe8MZWvz6ETX1Z5bQB4p5nkpRayEu5O2i4nrQVYZRkFIaCWkwKY4rs14bhwfNWJBAMoWpMONp6423xvHn2RlQQQiBFSsJCCEG68iiWGufBKPEIcUrDa31ni7KUOYNYLrc5%2F4Lx6zsXUxOjWzmvHMWBFR0BZPIdzV3atI6yRpEh%2FC2l6NYrrOibtxYovhkESJO7PJtg1dXQ9q3T%2FfMGz6sh6Y6Xvv5utaK%2FJt1ogLb48yOypNj679MAv6lnceAaCjNN%2BNBV41Y8ksG2%2FHJketYwqaEXmrCjLR6rVMPny5c8GOqIBow%2FN4cdyE7z2Io9eqTAbHGZaUJepdyo1kaBoE1zX2ufqMtZS5bxXXHyql4%2Ba1G9LVeOgoTgAzxrEop1bNtT53OaEf5BfvD0cMGtL02jUQZyTU6FZgW7cG6%2FQnJdDYruJWpS7n%2FNi0PYVnJNMdqWyfyB1dXxdskgvSC%2BA3UXTyrs1sUWGJW4emsyQVr8ym0gPiJCfJbdzES9paVoAgdwFTh49&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20260505T063129Z&X-Amz-SignedHeaders=host&X-Amz-Expires=86400&X-Amz-Credential=ASIA23PWRTAUAYWPXN63%2F20260505%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=70622e2d820d85c6355dc6fce34ca878165ccd59e19da81832f6e49cc72dc0a7\"}]},{\"Type\":\"FixedUpfrontPricingTerm\",\"CurrencyCode\":\"AUD\",\"Price\":\"0\",\"Grants\":[{\"DimensionKey\":\"AWSMP_XFCLYCKLNARTHHSSCLJYCRGHQYYN_MarketplaceMonitorSubscripton\",\"MaxQuantity\":1}]},{\"Type\":\"ValidityTerm\",\"AgreementDuration\":\"P8M\"},{\"Type\":\"PaymentScheduleTerm\",\"CurrencyCode\":\"AUD\",\"Schedule\":[{\"ChargeDate\":\"2026-05-01T00:00:00.000Z\",\"ChargeAmount\":\"36.92\"},{\"ChargeDate\":\"2026-06-01T00:00:00.000Z\",\"ChargeAmount\":\"36.92\"},{\"ChargeDate\":\"2026-07-01T00:00:00.000Z\",\"ChargeAmount\":\"36.92\"},{\"ChargeDate\":\"2026-08-01T00:00:00.000Z\",\"ChargeAmount\":\"36.92\"},{\"ChargeDate\":\"2026-09-01T00:00:00.000Z\",\"ChargeAmount\":\"36.92\"},{\"ChargeDate\":\"2026-10-01T00:00:00.000Z\",\"ChargeAmount\":\"36.92\"},{\"ChargeDate\":\"2026-11-01T00:00:00.000Z\",\"ChargeAmount\":\"36.92\"},{\"ChargeDate\":\"2026-12-01T00:00:00.000Z\",\"ChargeAmount\":\"36.92\"}]}],\"Rules\":[{\"Type\":\"AvailabilityRule\",\"AvailabilityEndDate\":\"2026-04-30T23:59:59.999Z\"},{\"Type\":\"TargetingRule\",\"PositiveTargeting\":{\"BuyerAccounts\":[\"XXXXXXXXXXX\",\"XXXXXXXXXXX\"]}}],\"State\":\"Released\"}",
    "DetailsDocument": {
        "Id": "offer-u2ss5wgupr4zs",
        "Name": "XXXXXXXXXX",
        "Description": "XXXXXXXXXX,
        "ProductId": "prod-vdpsxjiuga6qe",
        "Terms": [
            {
                "Type": "LegalTerm",
                "Documents": [
                    {
                        "Type": "CustomEula",
                        "Url": "https://aws-mp-offer-legal-artifacts-us-east-1-prod.s3.amazonaws.com/offer-u2ss5wgupr4zs/d1f7d354-e5e0-44a7-b496-f443f0b1da50?X-Amz-Security-Token=IQoJb3JpZ2luX2VjELX%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJGMEQCICPOtrdiv3urg7FQnd9TLeMTSLxKgeBpKh3lxjFCLDYtAiAt0gU3uNPfN7WZ7NCZzOTpo3ovJdqZi%2Be9go2rA58%2BGyr9Awh%2BEAIaDDc0NjIzMDc0OTIyNCIMrgnE5u7lJyiNUv8HKtoDSi4z18h7MSFvyWSp7xRSZm0UA%2Bcw%2FP6zoOGeGu%2BV9vRt%2F3FtEIXqGFzBUA%2Bd2d2dq3M22%2BB3%2B6xrM%2FbXKhXbCpEnNpYQE6D8zoKuFTGJK2U88ifE86NbCIEA0V1RddLqKbFci679rCqIG0c6%2BNScf8c4zdESyXXWgXem%2Bg2Gl%2B2%2FrSWSh7sHiV9gxrzcT1TrJ81vn2juVWmzgGoufydcnWsIypSoU5tz5rPZDRGMXdQM0DpCthr7CYGMp2SoDiWWJb2qykSUtMsJ2iF9lMmp%2BhcmKRi6EsuBCnJUGUZo5NUsXNJe0euWKGpa7FY9njXo7%2FtqLu6mW5efXZ4RTedPfVe8MZWvz6ETX1Z5bQB4p5nkpRayEu5O2i4nrQVYZRkFIaCWkwKY4rs14bhwfNWJBAMoWpMONp6423xvHn2RlQQQiBFSsJCCEG68iiWGufBKPEIcUrDa31ni7KUOYNYLrc5%2F4Lx6zsXUxOjWzmvHMWBFR0BZPIdzV3atI6yRpEh%2FC2l6NYrrOibtxYovhkESJO7PJtg1dXQ9q3T%2FfMGz6sh6Y6Xvv5utaK%2FJt1ogLb48yOypNj679MAv6lnceAaCjNN%2BNBV41Y8ksG2%2FHJketYwqaEXmrCjLR6rVMPny5c8GOqIBow%2FN4cdyE7z2Io9eqTAbHGZaUJepdyo1kaBoE1zX2ufqMtZS5bxXXHyql4%2Ba1G9LVeOgoTgAzxrEop1bNtT53OaEf5BfvD0cMGtL02jUQZyTU6FZgW7cG6%2FQnJdDYruJWpS7n%2FNi0PYVnJNMdqWyfyB1dXxdskgvSC%2BA3UXTyrs1sUWGJW4emsyQVr8ym0gPiJCfJbdzES9paVoAgdwFTh49&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20260505T063129Z&X-Amz-SignedHeaders=host&X-Amz-Expires=86400&X-Amz-Credential=ASIA23PWRTAUAYWPXN63%2F20260505%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=70622e2d820d85c6355dc6fce34ca878165ccd59e19da81832f6e49cc72dc0a7"
                    }
                ]
            },
            {
                "Type": "FixedUpfrontPricingTerm",
                "CurrencyCode": "AUD",
                "Price": "0",
                "Grants": [
                    {
                        "DimensionKey": "AWSMP_XFCLYCKLNARTHHSSCLJYCRGHQYYN_MarketplaceMonitorSubscripton",
                        "MaxQuantity": 1
                    }
                ]
            },
            {
                "Type": "ValidityTerm",
                "AgreementDuration": "P8M"
            },
            {
                "Type": "PaymentScheduleTerm",
                "CurrencyCode": "AUD",
                "Schedule": [
                    {
                        "ChargeDate": "2026-05-01T00:00:00.000Z",
                        "ChargeAmount": "36.92"
                    },
                    {
                        "ChargeDate": "2026-06-01T00:00:00.000Z",
                        "ChargeAmount": "36.92"
                    },
                    {
                        "ChargeDate": "2026-07-01T00:00:00.000Z",
                        "ChargeAmount": "36.92"
                    },
                    {
                        "ChargeDate": "2026-08-01T00:00:00.000Z",
                        "ChargeAmount": "36.92"
                    },
                    {
                        "ChargeDate": "2026-09-01T00:00:00.000Z",
                        "ChargeAmount": "36.92"
                    },
                    {
                        "ChargeDate": "2026-10-01T00:00:00.000Z",
                        "ChargeAmount": "36.92"
                    },
                    {
                        "ChargeDate": "2026-11-01T00:00:00.000Z",
                        "ChargeAmount": "36.92"
                    },
                    {
                        "ChargeDate": "2026-12-01T00:00:00.000Z",
                        "ChargeAmount": "36.92"
                    }
                ]
            }
        ],
        "Rules": [
            {
                "Type": "AvailabilityRule",
                "AvailabilityEndDate": "2026-04-30T23:59:59.999Z"
            },
            {
                "Type": "TargetingRule",
                "PositiveTargeting": {
                    "BuyerAccounts": [
                        "XXXXXXXXXX",
                        "XXXXXXXXXX"
                    ]
                }
            }
        ],
        "State": "Released"
    }
}
```

Then I'd add the entity ID filter over the top (ie get the biggest response payload and then filter it by adding query terms).

What I do know - if you can't make the simple call work right on the CLI which directly invokes the API(s), then embedding it in boto3 etc doesn't help.



## The wrap up

Text

[Back to awyspr fieldnotes index](https://fieldnotes.awyspr.com)
