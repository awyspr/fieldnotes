<a href="https://awyspr.com/"><img src="https://awyspr.com/assets/images/image07.svg?v=b4a015c2" width="10%" height="10%" align="left"></a>

# Pathfinding updates to Organizations API methods

2026-04-02

## What's this one all about then ?

This week AWS sneaked out a change to AWS Organizations API, and its got a bigger benefit than you might think
if you have never worked with Organizations via automation.

~ 2 Apr
https://awsapichanges.com/archive/changes/080f45-organizations.html
2026/03/31 - AWS Organizations - 8 updated api methods

### Pathfinding in Organizations

The simple version: all methods on the Organizations API now support a path, because the path field has been
added to `Account` and `OrganizationalUnit` objects in AWS Organizations API responses.

Iton s every method on this API, which makes complete sense, because path is a property for any/all actions 
on the Organizations API.

The more complex version: Organizations has always supported an N-level hierarchy for managing and grouping
AWS Accounts within an Organization. But until now, you've never been able to use the hierarchical path
as the means to navigate or automate Organization actions. If you're using the Organizations UI, it probably
feels like a natural thing to do to expand and collapse the Organization hierarchy, and the UI has hidden
the requirement to traverse paths. But if you work with Organizations programmatically, you've not had the ability 
to do the equivalent of Unix's `cd ..` (or `cd ../../../../`).

## The wrap up

Text

[Back to awyspr fieldnotes index](https://fieldnotes.awyspr.com)
