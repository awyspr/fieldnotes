<a href="https://awyspr.com/"><img src="https://awyspr.com/assets/images/image07.svg?v=b4a015c2" width="10%" height="10%" align="left"></a>

# Pathfinding updates to Organizations API methods

2026-04-02

## What's this one all about then ?

This week AWS sneaked out a change to the [AWS Organizations API](https://docs.aws.amazon.com/organizations/latest/APIReference/Welcome.html), and its got a bigger benefit than you might think if you have never worked with Organizations via automation.

Account and organizational unit (OU) objects now include path information in API responses. Account APIs (such as `DescribeAccount` and `ListAccounts`) and OU APIs (such as `DescribeOrganizationalUnit`) return a path field showing where entities exist within an organization.

### Pathfinding in Organizations

The simple version: all methods on the Organizations API now support a path, because the path field has been
added to `Account` and `OrganizationalUnit` objects in AWS Organizations API responses.

It's on every method on this API, which makes complete sense, because path is a property for any/all actions 
on the Organizations API.

The more complex version: Organizations has always supported an N-level hierarchy for managing and grouping
AWS Accounts within an Organization and organization Units (OUs) within an Organziation. But until now, you've 
never been able to use the hierarchical path as the means to navigate or automate these actions. If you're using 
the Organizations UI, it probably feels like a natural thing to do to expand and collapse the Organization hierarchy, 
and the UI has hidden the requirement to traverse paths. 

But if you work with Organizations programmatically, you've not had the ability 
to do the equivalent of Unix's `cd ..` (or `cd ../../../../`), let alone being able to do that using regular 
expressions which match certain path contents before taking actions like applying policies or moving things around.

The [new path method now supports regular expressions](https://docs.aws.amazon.com/organizations/latest/APIReference/API_OrganizationalUnit.html#organizations-Type-OrganizationalUnit-Path) to enumerate and navigate paths:

- `Pattern: ^(o-[a-z0-9]{10,32}\/r-[0-9a-z]{4,32}(\/ou\-[0-9a-z]{4,32}-[a-z0-9]{8,32})*(\/\d{12})*)\/`

## The wrap up

Its great to see Organizations API get these new methods added in, in our view some of these older APIs have not had 
enough attention with the rapid growth of AWS services.

[Back to awyspr fieldnotes index](https://fieldnotes.awyspr.com)
