# Forum

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Forum is a centralized exchange offering exposure to engagement-backed assets — "the first exchange to trade on attention." It turns online attention across social, search, and streaming data into measurable, tradable attention indices, then lists continuous perpetual-style futures contracts on top of them so participants can go long or short on cultural relevance as a new asset class. Forum (Y Combinator W26, based in New York City) exposes a full public developer surface: an OpenAPI 3.1 REST API at api.forum.market/v1 for market data, order management, positions, and account queries, and an AsyncAPI 3.0 WebSocket feed at wss://api.forum.market/ws/v1 for real-time order book, ticker, trade, index, and funding updates. Authentication is HMAC-SHA256 request signing with read/trade API-key permissions, and the docs ship an agent-native discovery surface (llms.txt, agent-card, agent-skills, and a documentation MCP server).

**Areas:** Company · Trading · Exchange · Perpetual Futures · Market Data · Attention Economy · Fintech · WebSocket · Real-Time

## Forum on APIs.io

Everything profiled for Forum is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/forum/](https://apis.io/providers/forum/)** — or go straight to one of the APIs or properties below.

### APIs (9)

- [Forum Account API](https://apis.io/apis/forum/forum-account-api/) — Account summary and balance
- [Forum Exchange API](https://apis.io/apis/forum/forum-exchange-api/) — Exchange status and server time
- [Forum Fills API](https://apis.io/apis/forum/forum-fills-api/) — Trade execution history
- [Forum Funding API](https://apis.io/apis/forum/forum-funding-api/) — Funding rates and history
- [Forum Indices API](https://apis.io/apis/forum/forum-indices-api/) — Attention index values and history
- [Forum Market Data API](https://apis.io/apis/forum/forum-market-data-api/) — Order books, tickers, trades, and candles
- [Forum Markets API](https://apis.io/apis/forum/forum-markets-api/) — Market listings and details
- [Forum Orders API](https://apis.io/apis/forum/forum-orders-api/) — Order placement, cancellation, and queries
- [Forum Positions API](https://apis.io/apis/forum/forum-positions-api/) — Open position data

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### Arazzo workflows (1)

Multi-step workflows that chain operations into a business task.

- [Forum — discover a market and place an order](https://apis.io/arazzos/forum/forum-place-order/)

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Forum WebSocket Feed](https://apis.io/asyncapis/forum/forum-websocket-asyncapi/)

#### Event channels (19)

Individual events and webhooks the provider emits.

- [/](https://apis.io/channels/forum/auth/)
- [bookUpdates](https://apis.io/channels/forum/bookupdates/)
- [candleUpdates1d](https://apis.io/channels/forum/candleupdates1d/)
- [candleUpdates1m](https://apis.io/channels/forum/candleupdates1m/)
- [candleUpdates5m](https://apis.io/channels/forum/candleupdates5m/)
- [/](https://apis.io/channels/forum/errors/)
- [fundingEvents](https://apis.io/channels/forum/fundingevents/)
- [heartbeat](https://apis.io/channels/forum/heartbeat/)
- [indexUpdates](https://apis.io/channels/forum/indexupdates/)
- [/](https://apis.io/channels/forum/listsubscriptions/)
- [/](https://apis.io/channels/forum/logout/)
- [/](https://apis.io/channels/forum/subscribe/)
- [tickerUpdates](https://apis.io/channels/forum/tickerupdates/)
- [trades](https://apis.io/channels/forum/trades/)
- [/](https://apis.io/channels/forum/unsubscribe/)
- [userAccount](https://apis.io/channels/forum/useraccount/)
- [userFills](https://apis.io/channels/forum/userfills/)
- [userOrders](https://apis.io/channels/forum/userorders/)
- [userPositions](https://apis.io/channels/forum/userpositions/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [Forum Docs Docs MCP](https://apis.io/servers/forum/forum-docs-docs-mcp/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Forum Agentic Access](https://apis.io/agentic-access/forum/forum-agentic-access/)

#### Collections (9)

Postman and Open Collection request collections.

- [Forum Account API](https://apis.io/collections/forum/open-forum-account-api/)
- [Forum Account Exchange API](https://apis.io/collections/forum/open-forum-exchange-api/)
- [Forum Account Fills API](https://apis.io/collections/forum/open-forum-fills-api/)
- [Forum Account Funding API](https://apis.io/collections/forum/open-forum-funding-api/)
- [Forum Account Indices API](https://apis.io/collections/forum/open-forum-indices-api/)
- [Forum Account Market Data API](https://apis.io/collections/forum/open-forum-market-data-api/)
- [Forum Account Markets API](https://apis.io/collections/forum/open-forum-markets-api/)
- [Forum Account Orders API](https://apis.io/collections/forum/open-forum-orders-api/)
- [Forum Account Positions API](https://apis.io/collections/forum/open-forum-positions-api/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Forum Openapi Overlay](https://apis.io/overlays/forum/forum-openapi-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Forum Authentication](https://apis.io/security/forum/forum-authentication/)
- [Forum Domain Security](https://apis.io/security/forum/forum-domain-security/)

#### Rate limits (1)

Published request limits.

- [Forum Rate Limits](https://apis.io/rate-limits/forum/forum-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.forum.market/)
- [Documentation](https://docs.forum.market/)
- [Getting started](https://docs.forum.market/api-reference/quick-start)
- [API reference](https://docs.forum.market/api-reference/introduction)
- [Sign up](https://app.forum.market/)
- [Support](https://docs.forum.market/guide/feedback)
- [Blog](https://www.forum.market/blog/)
- [Terms of service](https://forum-legal.s3.us-east-2.amazonaws.com/terms-of-service.pdf)

## API Evangelist rating

**Kin Score 38.3** — thin · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 59.9 |
| Contract governance | 4.5 |
| Operational transparency | 55.3 |
| Developer ergonomics | 21.4 |
| Access clarity | 23.7 |

**Agent readiness 42.3** — agent-native

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | documented (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | documented (partial credit) |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | partial |
| Rate Limit Signal | verified |
| Event Surface Described | derived (partial credit) |
| Agent Skills | yes |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | partial |
| Operation Distinctiveness | distinct |

**Regulatory alignment 19.4** — Securities & Market Data

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/forum/](https://apis.io/providers/forum/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Forum: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/forum/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
