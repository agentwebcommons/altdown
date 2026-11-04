# Changelog

Each version of the specification keeps its own address. The latest version is always at <https://altdown.org/spec/>.

While a version is a draft, its text may change. Each change is listed here with its date, newest first. Once a version is final, its text is frozen.

## Altdown Services 0.1 (Draft)

- 2026-11-04: First draft, at <https://altdown.org/services/>. It applies Altdown's rules to the capabilities a page offers agents: announcement from the page, the round trip, parity of price and terms, descriptions as data, and fallback.

## 1.0 (Draft)

- 2026-11-04: Clarifications. A page may also announce its copy with an HTTP `Link` header. Text that qualifies the main content, such as a disclaimer, is main content. The spot check tests containment, not main-content extraction. The Overview states the relation to `llms.txt` version 2, and the Roadmap names the companion drafts and when 1.0 will be final.
- 2026-11-04: Each copy attachment in the index may carry a `sha256` digest, and agents check it. A removed page stays in the index as a tombstone so agents can forget it.
- 2026-11-04: Intermediaries (hosts, CDNs, proxies, caches) are now a conforming party. A new section, Authority, requires an intermediary that answers with Markdown to return the declared copy unchanged, and agents to prefer a valid copy over any derived Markdown. Added Substitution to the security considerations.
- 2026-11-04: Removed the `signals` field; the name is reserved and ignored. A new section, Usage and access, leaves usage to `robots.txt`, content signals, robots meta tags, and licenses, which apply to a copy as they apply to its page. The `description` field must now match the page's meta description.
- 2026-11-01: The round-trip rule now says what an agent does when it reaches a page at an alias, such as `www`, that does not redirect. Added a hosting note on redirecting aliases, and a line for each in the conformance checklist.
- 2026-10-31: First public draft, at <https://altdown.org/1.0/>.
