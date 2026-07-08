<a href="https://awyspr.com/"><img src="https://awyspr.com/assets/images/image07.svg?v=b4a015c2" width="10%" height="10%" align="left"></a>

# PartnerCentral Agents in your CRM via MCP

2026-03-29

## What's this one all about then ?

So just on 2 weeks ago AWS released Agents in PartnerCentral, including MCP support (allowing external tools - like CRMs - to call into PartnerCentral
and pull back AWS AI-generated advice about customers, opportunities, funding etc). 
Of course, we have had a bit of an experiment.

## Early experiences

Up front: the CRM we're using for these experiments is Hubspot. Hubspot has pretty advanced agent support and MCP support out of the box, so connecting
it to PartnerCentral wasn't difficult. [The docs](https://docs.aws.amazon.com/partner-central/latest/APIReference/partner-central-mcp-server.html) if you are that way inclined.

This Hubspot instance also contains a few hundred opportunities - ranging from historical ones through to actively progressed ones.

Here's a few of our observations:

- the PartnerCentral Agent is quite lengthy and prescriptive in its advice - if you ask for meeting preparation and sales planning support, you will be provided with an extract and replay summary of information on the ACE opportunity (good), and then quite lengthy advice about how to 'do all the things' to tick AWS boxes (eg get POC funding, involve AWS co-sell resources - good-bad depending) and then fairly generic advice about classic XaaS B2B sales engagements being run based on a MEDDPICC process (bad - typically untuned). _If_ you combine that advice with more nuanced and locally adapted advice from the Hubspot Prospecting or Sales Agents, you get more relevant recommendations that are richer context aware from your local CRM.

- most of the time the PartnerCentral Agent results are very AWS-seller biased, not so much partner-business aligned. That seems like a dial AWS might want to be able to tweak as a partner based on a persona or deal basis or even whole partner-ACE basis - whats the recommendation if I am a partner AE vs an AWS seller, or if I am a supervisor+ of partner AEs vs a territory manager. Again, _if_ you treat this as input and allow Hubspot to reprocess and reweight it, sometimes you can pick up convenient linkage points.

- with one partner we work with, we have done some compare/contrast work on pulling (via MCP) the recommendations that the PartnerCentral Agent makes on an ACE deal vs the recommendations that are made from a CRM-embedded context. This is more typically what a 3PI might do, but there are folks that use CRMs which are connected without a 3PI being involved, and CRMs which have "AI deal advisors". Unsuprisingly - probably because of richer context on the partner CRM side, the advice is often different - sometimes there's an overlap, but the PartnerCentral Agent tends towards "how to do agentic/programmatic co-sell" whereas the partner CRM tends towards "how to close the deal" - you'll appreciate these are not the same all the time.

## Other Notes
A few other things we noticed working with PartnerCentral Agents and reading the supporting release material:

- In the Agents in PartnerCentral announcement and the docs, one future direction seems to be that partners could upload raw/unstructured data to the PartnerCentral Agents - eg call transcripts, documents, diagrams etc. While there's potentially some good utility with this there are two counterpoints: 1) perhaps these artefacts should go into a partner's CRM via a similar AI analysis process and then get synced to ACE and 2) if you are uploading those additional raw materials, what are the safeguards about the content and the arrangements for data ownership ?

- We ran a few experiments with asking PartnerCentral Agent about opportunities which straddle the partner boundary - for example being legitimately shared with another partner as joint pursuits. It turns out that there is potential for leakage unless the AI guardrails are tightened a bit - opportunity sharing seems to allow you some level of insight into the other partner's history with the customer in question (eg how many other opportunities in a period), or beyond (how many other opportunities which have a similar solution and their industry/segment distribution). Take care.
 
## The wrap up

MCP offers a very low barrier to integration for AI tools, but using it requires a degree of 'trust but verify' behaviour in terms of the responses
collected from the remote system (whether AI enabled with Agents or not). In most cases, the "local" context is far richer and more current, and so MCP
responses should be treated as supplementary compared to AI/Agent analysis over the source materials.

With PartnerCentral Agents via MCP the value is somewhere towards the partner side, and most likely operationalized in the CRM, not in ACE. Pull the opportunity summary/recommendations through into CRM, merge/compare with local intelligence that is not synced up, and then decide what to do.

[Back to awyspr fieldnotes index](https://fieldnotes.awyspr.com)
