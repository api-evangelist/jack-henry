# Jack Henry & Associates

API Evangelist profile of **Jack Henry & Associates** (Nasdaq: **JKHY**) — an
S&P 500 financial-technology company providing core banking, payments,
lending, digital banking, and fraud-prevention technology to roughly
**7,400** community and regional banks, credit unions, and other financial
institutions in the United States. Headcount of approximately **7,240**
associates as of fiscal year-end June 30, 2025.

This repo indexes the **public developer surface** at
[jackhenry.dev](https://jackhenry.dev/) (mirrored at
[banno.github.io/open-api-docs](https://banno.github.io/open-api-docs/)) and
the related Banno GitHub organization at
[github.com/Banno](https://github.com/Banno).

## What's here

| Folder | Contents |
|---|---|
| [`apis.yml`](apis.yml) | Master index — every API, common property (portal, docs, GitHub, support, status, IR, blog), and artifact link. |
| [`openapi/`](openapi/) | OpenAPI 3.0 specs for the six documented HTTP surfaces. |
| [`asyncapi/`](asyncapi/) | AsyncAPI 2.6 spec for the Enterprise Event System (Kafka pub/sub). |
| [`capabilities/`](capabilities/) | Naftiko capability definitions — one per API plus two cross-surface workflow compositions. |
| [`json-schema/`](json-schema/) | Canonical JSON Schemas for key resources (Account, Transaction, Transfer, AbilitiesMap, Customer, LoanAccount, ACH Transaction). |
| [`json-structure/`](json-structure/) | Field-level structure documentation. |
| [`json-ld/`](json-ld/) | JSON-LD `@context` aligning Jack Henry terms to schema.org. |
| [`examples/`](examples/) | Request / response payload examples. |
| [`rules/`](rules/) | Spectral rulesets enforcing per-surface conventions (path versioning, OIDC, scope domains, Title Case summaries). |
| [`vocabulary/`](vocabulary/) | Domain vocabulary spanning identity, Banno, jXchange, payments, events, and corporate terms. |
| [`plans/`](plans/) | Commercial plans surface (API Commons Plans 0.1) — captures Jack Henry's enterprise MSA + Fintech Integration Network model. |
| [`rate-limits/`](rate-limits/) | Documented and observable rate-limit posture per API. |
| [`finops/`](finops/) | FinOps Framework + FOCUS mapping for cost allocation, forecasting, and rate optimization. |

## APIs documented

| API | Type | Base URL | Docs |
|---|---|---|---|
| **Banno Consumer API** | OpenAPI | `https://api.banno.com` | [consumer-api/](https://jackhenry.dev/open-api-docs/consumer-api/) |
| **Banno Admin API** | OpenAPI | `https://api.banno.com` | [admin-api/](https://jackhenry.dev/open-api-docs/admin-api/) |
| **Banno Plugin Framework** | OpenAPI + Bridge SDK | `https://digital.banno.com` | [plugins/](https://jackhenry.dev/open-api-docs/plugins/) |
| **Banno Authentication Framework** | OpenAPI (OIDC) | `https://api.banno.com` | [authentication-framework/](https://jackhenry.dev/open-api-docs/authentication-framework/) |
| **jXchange REST** | OpenAPI | `https://jxchange.jackhenry.com` | [jxchange-rest/](https://jackhenry.dev/jxchange-rest/) |
| **Jack Henry Payments** | OpenAPI | `https://api.payments.jackhenry.com` | [developer portal](https://api.payments.jackhenry.com/developer/) |
| **Enterprise Event System** | AsyncAPI (Kafka) | `events.jackhenry.com` | [ees/](https://jackhenry.dev/ees/) |
| **SymXchange** | Documentation | `https://symxchange.jackhenry.com` | [symxchange-api-docs/](https://jackhenry.dev/symxchange-api-docs/) |
| **Operational Data Integration (ODI)** | Documentation | `https://odi.jackhenry.com` | [odi/](https://jackhenry.dev/odi/) |
| **Data Hub** | Documentation | `https://datahub.jackhenry.com` | [data-hub/](https://jackhenry.dev/data-hub/) |
| **Digital Core** | Documentation | `https://digital-core.jackhenry.com` | [digital-core-api-docs/](https://jackhenry.dev/digital-core-api-docs/) |

All Banno HTTP surfaces use **OAuth 2.0 + OpenID Connect** at
`https://api.banno.com/a/oidc/.well-known/openid-configuration`. Endpoints
are scope-gated under the `https://api.banno.com/*` URI namespace
(e.g. `https://api.banno.com/consumer/auth/transactions.detail.readonly`).

## Workflow capability compositions

| File | Workflow |
|---|---|
| [`capabilities/digital-banking-experience.yaml`](capabilities/digital-banking-experience.yaml) | OIDC authorize -> token exchange -> get user -> list accounts -> list transactions -> render plugin card -> (transfer or Zelle). |
| [`capabilities/payments-orchestration.yaml`](capabilities/payments-orchestration.yaml) | jXchange customer + deposit-account lookup -> Payments Orchestrator routes the cross-rail payment -> Enterprise Event System emits the transaction event for reconciliation. |

## Notable Banno GitHub repos referenced

- [`Banno/banno-plugin-framework-bridge`](https://github.com/Banno/banno-plugin-framework-bridge) — the `@jack-henry/banno-plugin-framework-bridge` JS message bridge.
- [`Banno/consumer-api-openid-connect-example`](https://github.com/Banno/consumer-api-openid-connect-example) — example of connecting to Banno via OIDC.
- [`Banno/admin-api-openid-connect-example`](https://github.com/Banno/admin-api-openid-connect-example) — Admin API OIDC example.
- [`Banno/simple-plugin-example`](https://github.com/Banno/simple-plugin-example) — companion to the Plugin Quickstart.
- [`Banno/basic-plugin-example`](https://github.com/Banno/basic-plugin-example), [`Banno/simple-announcements-plugin`](https://github.com/Banno/simple-announcements-plugin) — sample plugins.
- [`Banno/jhid-client-creds-helper`](https://github.com/Banno/jhid-client-creds-helper) — helper utilities for Banno's Platform API.
- [`Banno/jack-henry-design-system`](https://github.com/Banno/jack-henry-design-system) — Jack Henry design-system web components.
- [`Banno/banno-powerons`](https://github.com/Banno/banno-powerons) — Banno PowerOn library for the Symitar core.

## Notable absences

- **No public OpenAPI YAML downloads.** The reference docs at
  banno.github.io describe paths, methods, schemas, and scopes, but the
  canonical `.yaml`/`.json` artifacts are not exposed for download. The
  OpenAPI specs in `openapi/` are reconstructed from documented endpoints
  and would need to be re-validated against any first-party spec drop.
- **No public per-API list prices** anywhere on jackhenry.dev. Pricing is
  contract-driven per institution (see [`plans/`](plans/) for full notes).
- **No published per-key rate limits** on the Banno or jXchange surfaces
  (see [`rate-limits/`](rate-limits/)).
- **No self-serve sandbox signup** — developer-portal access is gated by
  institution sponsorship or Fintech Integration Network (FIN) onboarding.
- **No public AsyncAPI/Webhook schema** for the Enterprise Event System
  — the AsyncAPI in this repo is reconstructed from documented event
  categories.

## Sources

- Developer portal: [jackhenry.dev](https://jackhenry.dev/)
- API reference mirror: [banno.github.io/open-api-docs](https://banno.github.io/open-api-docs/)
- GitHub org: [github.com/Banno](https://github.com/Banno)
- Corporate: [jackhenry.com](https://www.jackhenry.com/)
- Investor relations: [ir.jackhenry.com](https://ir.jackhenry.com/)
- Status: [status.banno.com](https://status.banno.com/)

---

Profiled by [API Evangelist](https://apievangelist.com/) as part of the
[api-evangelist network](https://github.com/api-evangelist).
