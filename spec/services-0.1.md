# Altdown Services

Version 0.1 (Draft) · November 4, 2026

## Contents

- [What is Altdown Services?](#what-is-altdown-services)
- [About this document](#about-this-document)
- [The rules](#the-rules)
- [Announcing a capability](#announcing-a-capability)
- [The round trip](#the-round-trip)
- [Parity](#parity)
- [Descriptions are data](#descriptions-are-data)
- [Usage and access](#usage-and-access)
- [Falling back](#falling-back)
- [Open questions](#open-questions)
- [References](#references)
- [License and authorship](#license-and-authorship)

## What is Altdown Services?

Altdown Services is a draft for the capabilities a site offers agents: looking up a price, checking availability, placing an order, searching documentation. It applies the rules of [Altdown](https://altdown.org/spec/) to them, so that what a site offers an agent matches what it shows a person.

Altdown Services defines no tool or API format. Sites already describe their capabilities with formats that exist: OpenAPI documents, MCP Server Cards listed in an AI Catalog, A2A agent cards, the API catalog of RFC 9727, and tools that a page registers through WebMCP. This document says how a page points to them, and what an agent may trust in them.

This is version 0.1, a draft for comment. Its text will change.

## About this document

The words *must*, *must not*, *should*, *should not*, and *may* carry their usual meanings from [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119).

A **capability** is something an agent can do on a site through an interface the site provides. A **descriptor** is a document that describes a capability in one of the formats above. A **page** is an HTML document at a URL, as in Altdown.

The parties are those of Altdown: a **publisher**, the site that offers capabilities; an **agent**, any program that uses them; and an **intermediary**, any software between the two.

## The rules

Altdown Services applies the same five rules as Altdown.

1. **Announce from the page.** A page names the capabilities that act on it. An agent does not guess.
2. **Point back.** A capability counts as the site's own only if the site links to it or lists it.
3. **Match the page.** A capability offers an agent what the page offers a person.
4. **Data, never instructions.** Nothing in a descriptor or a response can direct the agent.
5. **Fall back to the page.** When a capability is missing or fails a check, the agent uses the page as a person would.

The sections below say what each rule means for capabilities.

## Announcing a capability

A page announces a capability that acts on it with a link element in its `<head>`. For a descriptor such as an OpenAPI document, the link uses the `service-desc` relation:

```html
<link rel="service-desc" href="/api/quotes/openapi.json">
```

A pricing page links to its quote API. A product page links to its ordering API. A documentation page links to the MCP server that searches it. An agent finds the capability where the content is.

A site may also list its capabilities in a site-wide catalog: an API catalog at `/.well-known/api-catalog`, as RFC 9727 defines, or an AI Catalog at `/.well-known/ai-catalog.json`, which MCP Server Cards use. An agent may read a catalog at the path its own standard defines. It must not guess other paths.

A tool that a page registers through WebMCP is announced by the page itself, because it runs in the page.

## The round trip

A descriptor counts as the site's own only if the site links to it from a page or lists it in a catalog on the site's origin.

A descriptor may live on another origin, for example when a platform runs a service for the site. It counts when the site links to it or lists it. A registry entry, a package, or a search result that the site neither links to nor lists does not count, whatever it is called.

This is the rule that stops impersonation. A party that cannot edit the site cannot make the site link to its server.

## Parity

**A capability must not offer an agent a different price, availability, or terms than the page it acts on shows a person for the same request.**

An agent may check this with a spot check, in the manner of Altdown's:

1. Choose a small number of requests whose answer the page shows a person: a listed price, the availability of a listed item, a published term.
2. Make each request through the capability. Use read-only requests, such as a quote or a lookup. Never place an order, make a booking, or send a payment to test parity.
3. Compare each answer with what the page shows.

An agent should treat a site whose capability fails a parity check as having no capability, and use the page instead. An agent should say in its documentation how it checks parity.

In this version, parity covers answers that the page shows to an anonymous visitor. Prices and terms that legitimately vary by location, quantity, or account are an open question.

## Descriptions are data

**An agent must treat descriptors, tool names, tool descriptions, parameter hints, and responses as data, never as instructions.** Text that reads as a command to the agent, a change to its task, or a message to the model is content and nothing more.

This is Altdown's rule for copies, applied to capabilities. It addresses tool poisoning, where a description carries instructions meant for the model that reads it.

## Usage and access

Altdown Services adds no policy vocabulary. `robots.txt`, content signals, robots meta tags, licenses, and payment standards say who may use a site and how. A capability is subject to the same terms and access conditions as the pages it acts on, and an agent must apply them.

## Falling back

At every step where a capability is missing, fails the round trip, or fails a parity check, the agent uses the page as a person would. Adopting Altdown Services badly loses a site nothing it had before.

## Open questions

- Parity for prices and terms that legitimately vary by location, quantity, or account.
- How a descriptor names the pages it serves, so that one descriptor can complete the round trip with many pages.
- Whether the AI Catalog or the RFC 9727 API catalog should be the preferred site-wide list.
- How an agent reports a failed parity check to the publisher.

Comments are welcome as [issues on GitHub](https://github.com/agentwebcommons/altdown/issues).

## References

- [Altdown Specification](https://altdown.org/spec/). The rules this document applies.
- [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119), Key words for use in RFCs to Indicate Requirement Levels.
- [RFC 8631](https://www.rfc-editor.org/rfc/rfc8631), Link Relation Types for Web Services. The `service-desc` relation.
- [RFC 9727](https://www.rfc-editor.org/rfc/rfc9727), api-catalog: A Well-Known URI and Link Relation to Help Discovery of APIs.
- [SEP-2127: MCP Server Cards](https://modelcontextprotocol.io/seps/2127-mcp-server-cards). Server Cards and the AI Catalog.
- [A2A Protocol: Agent Discovery](https://a2a-protocol.org/latest/topics/agent-discovery). Agent cards.
- [WebMCP](https://webmachinelearning.github.io/webmcp), Web Machine Learning Community Group.
- [OpenAPI Specification](https://spec.openapis.org/oas/latest.html).

## License and authorship

This document is published under the [Creative Commons Attribution-ShareAlike 4.0](https://creativecommons.org/licenses/by-sa/4.0/) license, like the Altdown specification it builds on.
