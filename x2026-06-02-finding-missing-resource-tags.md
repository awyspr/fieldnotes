<a href="https://awyspr.com/"><img src="https://awyspr.com/assets/images/image07.svg?v=b4a015c2" width="10%" height="10%" align="left"></a>

# Finding missing resource tags

2026-06-02

## What's this one all about then ?

AWS sneaked out a small but significant change to their Resource Tagging API yesterday. 

If you've ever been responsible for managing resource tags (not just applying them), you'll know that Resource Tagging has
been around a long time and while critical for purposes ranging from billing and cost management, operational management and change
control, has been a bit unloved in terms of functionality.

### xxx

~ 2 Jun behold the missing resource tags https://awsapichanges.com/archive/changes/e7ba6b-tagging.html

The [AWS docs](https://docs.aws.amazon.com/resourcegroupstagging/latest/APIReference/API_GetResources.html) have been updated.

Specifically what has been added is that the `GetResources` API now returns `MissingTagKeys` in `ComplianceDetails`, 
listing tag keys defined as required in the `ReportRequiredTagBlock` block of the effective tag policy that are absent from 
the resource.

This means that a call to `GetResources` can return all the tagged or *previously* tagged resources that are located in the 
specified Amazon Web Services Region for the account. The *previously* tagged part is where the magic is - without maintaining
your own inventory of resources and applied tags, you can simply ask "were there any resources which were previously tagged
that are now no longer tagged" and get an answer direct from the API.

The two big submethods are:
- `ExcludeCompliantResources` which specifies whether to exclude resources that are compliant with the tag policy. Set this to true if you are interested in retrieving information on noncompliant resources only.
- `IncludeComplianceDetails` which wpecifies whether to include details regarding the compliance with the effective tag policy. Set this to true to determine whether resources are compliant with the tag policy and to get details.

Depending on what information you want returned, you can also specify the following:
- Filters that specify what tags and resource types you want returned.
- The response includes all tags that are associated with the requested resources.
- Information about compliance with the account's effective tag policy.

## The wrap up

Perhaps PRM has brought resource tagging back into focus, or maybe there's another reason for these changes - either way,
the new capability on the API allows you to _finally_ get back resources that have missing resource tags compared
to a prior state.

[Back to awyspr fieldnotes index](https://fieldnotes.awyspr.com)
