<a href="https://awyspr.com/"><img src="https://awyspr.com/assets/images/image07.svg?v=b4a015c2" width="10%" height="10%" align="left"></a>

# Short-lived (but short-sighted) IAM permissions for AWSMP provisioning

2025-11-22

## What's this one all about then ?

An announcement came out this week about a [new short-lived IAM permission designed to streamline provisioning of AWSMP products](https://aws.amazon.com/about-aws/whats-new/2025/11/streamline-integration-partner-products-iam-delegation/).

This really scratches an itch, as the "get the right permissions available to deploy into a customer account" can really delay things.
Often someone who makes the purchase on Marketplace does not have the IAM permissions required to actually deploy the purchased 
product, and that causes a bit of a run round between the buyer and their systems team, often with the partner-publisher acting as 
a facilitator to get the product deployed. It can eat up hours, weeks, or even months - which for a monthly subscription effectively
means that the customer didn't get the functionality-benefits they wanted.

### A quick glance

We took at look at the short-lived IAM delegation.

This isn't the first time AWS has released a short-lived IAM delegation - the [AWS Security Token Service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp.html) has been around for years.

This one is different to STS. 

Here's the AWS diagram of the end-to-end flow.

<img src="https://docs.aws.amazon.com/images/IAM/latest/UserGuide/images/delegation-flow.png">

* The partner-publisher makes a request for temporary access.
* Request is routed into Console as an IAM request.
* Someone at the customer-account with the right permissions needs to review it and approve it.
* Once granted, partner-publisher can do the thing.

Sounds good.

But the [devil is in the details](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies-temporary-delegation.html)

"You can only delegate permissions to a product provider if you have permissions to the services and 
actions included in the temporary delegation request." 

Sooo ... someone on the customer-account side that initiates or understands the AWSMP purchase has been made needs to match-make with
someone on the customer-account side who has the permissions to approve the scope in the temporary delegation
request. Since every product is different you can imagine the permissions requested range from basic/common things to far more
rare and exotic.

But its a bit worse, because ...

"If you don't have access to the requested services and actions, the product provider does not receive these 
permissions when you approve the request."

In other words, someone on customer-account side who sees the request and approves it but does not understand the
scope of the request or have the permissions to delegate those will effectively null-out the partner-publisher request.
Failure is silent - the notification goes back to the partner-publisher, but without any hint that the approver had 
the right IAM-fu. And so the partner-publisher will try to do whatever the thing is, and it will fail. And the process 
will have to start again, because the request is "approve once" whether or not the right delegation is
in hand.

To counter, there is a [new set of IAM permissions that can be given out by a customer-account administrator](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies-temporary-delegation.html#temporary-delegation-managing-permissions). But they only address the request approval piece (ie process),
not the actual permissions scope matching and authorization.

Also, "temporary" delegation requests apparently live forever - they are closed off when "approved" but actually don't expire.
This exposes a different risk that someone comes along a lot later, sees the request and then clicks the wrong button.

## The wrap up

What has really changed here is partner-publisher being able to make a structured and traceable request for permissions
associated with a product provisioning action. That's a good thing.

What has not changed here is that there's still a potential run-around to find the holder of the correct set of 
permissions on the customer-account to be able to approve the fancy new delegation request and to coordinate that so that
action = success.

[Back to awyspr fieldnotes index](https://fieldnotes.awyspr.com)
