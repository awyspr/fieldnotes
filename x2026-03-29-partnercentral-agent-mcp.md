<a href="https://awyspr.com/"><img src="https://awyspr.com/assets/images/image07.svg?v=b4a015c2" width="10%" height="10%" align="left"></a>

# partnercentral-agent-mcp

2026-03-29

## What's this one all about then ?

So just on 2 weeks ago AWS released Agents in PartnerCEntral, including MCP support (allowing external tools - like CRMs - to call into PartnerCentral
and pull back AWS advice about customers, opportunities, funding etc).

Of course, we have had a bit of an experiment.

## Early experiences

Up front: the CRM we're using for these experiments is Hubspot. Hubspot has pretty advanced agent support and MCP support out of the box, so connecting
it to PartnerCentral wasn't difficult. 

This Hubspot instance also contains a few hundred opportunities - ranging from historical ones through to actively progressed ones.

- Turning to PartnerCentral Agent advice, I was glad to hear that the Agent has been instructed to "tone it down a bit" in terms of its advice particularly for meeting preparation and sales plan generation - its very long, very prescriptive and most of the time the results are very AWS-seller biased, not partner-business aligned. That seems like a dial you might want to be able to tweak as a partner based on a persona or deal basis or even whole partner-ACE basis - whats the recommendation if I am a partner AE vs an AWS seller, or if I am a supervisor+ of partner AEs vs a territory manager.

- With one partner I work with, we have done some compare/contrast work on pulling (via MCP) the recommendations that the PartnerCentral Agent makes on a deal vs the ones that are made from a CRM-embedded context. This is more typically what a 3PI might do, but there are folks that use CRMs which are connected without a 3PI being involved, and CRMs which have "AI deal advisors". Unsuprisingly - probably because of richer context on the partner CRM side, the advice is often different - sometimes there's an overlap, but the PartnerCentral Agent tends towards "how to do agentic/programmatic co-sell" whereas the partner CRM tends towards "how to close the deal" - you'll appreciate these are not the same all the time. I think the trick will be (and this is probably not new) to combine local intel from a partner's CRM including whatever local agent makes deal progression recommendations with whatever the PartnerCentral Agent gives back on the same deal.

NEW-IN-TOWN: Partner Central Agents/MCP compare and contrast Opportunity advice.
Disclosure - using Hubspot as CRM. They're unsuprisingly different and so the value is somewhere in the middle, and most likely operationalized on the CRM side not in ACE. Pull the opportunity summary/recommendations through into CRM, merge/compare with local intelligence that is not synced up, and then decide what to do.

## Other Notes
Here's some thoughts/questions that I made note of over the last couple of weeks including as PartnerCentral Agents came into the open. I appreciate these issues/feedback may not all belong to you, but they seem to be in close enough proximity to warrant at least mentioning them.

- In the Agents in PartnerCEntral announcement and the docs, one future direction seems to be that partners could upload raw/unstructured data to the PartnerCentral Agents - eg call transcripts, documents, diagrams etc.

- Accepting that some of this might end up in a partner CRM and hence be synced in summary to PartnerCentral anyway, the real question is about what conditions apply to those documents which are typically customer-partner or partner confidential. The hand wavy response is usually that AWS Partner terms apply, but they don't actually address these emerging use cases very well. I am sure a lot of other partners are going to ask this - if we upload this data into PartnerCentral Agents, then does it remain ours ? yours ? shared ? can you guarantee the boundary ie that this won't leak over into another partner (eg competitor).

- Speaking of leakage, I have had a few experiments with asking PartnerCentral Agent about opportunities I have admin access to and specifically about other opportunities for the same customer account that may have been lodged by the primary partner I represent at the time or even _other_ partners. There is certainly some Agent response leakage about what other opportunities may have been registered and the AWS perspective on the customer that comes back. This seems like somewhere some tightening is required. I can give you examples if you like.

## The wrap up

Text

[Back to awyspr fieldnotes index](https://fieldnotes.awyspr.com)
