# Zoho People

API Evangelist index repo for **[Zoho People](https://www.zoho.com/people/)** — Zoho's AI-first, cloud-based HRMS that spans the Core HR, Time & Attendance, Leave, Performance, Learning, Recruitment, Payroll and HR Analytics domains and ships as part of the broader Zoho One business suite.

> "AI-first HR software for every business"
> — [zoho.com/people](https://www.zoho.com/people/)

This repo follows the [APIs.json](https://apisjson.org) convention. The root `apis.yml` is the machine-readable index; everything else lives in its dedicated subfolder.

## API surface

| API | Base URL | Auth | Reference |
|---|---|---|---|
| Zoho People REST API | `https://people.zoho.com/people/api` (US DC) | Zoho Accounts OAuth 2.0, scope namespace `ZOHOPEOPLE` | [overview](https://www.zoho.com/people/api/overview.html) |

The provider publishes **seven OAuth scopes** (verified on [the scopes page](https://www.zoho.com/people/api/scopes.html)):
`employee`, `forms`, `dashboard`, `automation`, `timetracker`, `attendance`, `leave` — each with one or more operation types (`ALL`, `READ`, `CREATE`, `UPDATE`, `DELETE`). Scope strings follow the pattern `ZohoPeople.<scope>.<operation>`.

Tokens are issued by [Zoho Accounts](https://www.zoho.com/accounts/protocol/oauth.html) using the **Authorization Code** grant; access tokens live for **1 hour**, refresh tokens are long-lived.

Eight regional data centers are documented as servers in [`openapi/zoho-people-openapi.yml`](openapi/zoho-people-openapi.yml) (US, EU, IN, AU, JP, CN, CA, SA).

## Artifacts in this repo

| Folder | Files |
|---|---|
| `openapi/` | `zoho-people-openapi.yml` — OpenAPI 3.1 covering Employee, Forms, Leave, Attendance, Time Tracker, Dashboard, Automation. |
| `rules/` | `zoho-people-rules.yml` — Spectral ruleset enforcing Title Case summaries, lowerCamelCase operationIds, OAuth-on-every-op, scope-format validation, and the multi-DC server list. |
| `capabilities/shared/` | `zoho-people-capabilities.yaml` — Naftiko per-API capability map (one capability per operation, with scope hints and governance flags). |
| `capabilities/` | `employee-onboarding.yaml`, `leave-request-lifecycle.yaml`, `timesheet-billing.yaml` — workflow compositions. |
| `json-schema/` | `zoho-people-employee-schema.json`, `zoho-people-leave-request-schema.json`, `zoho-people-attendance-entry-schema.json`, `zoho-people-time-log-schema.json`, `zoho-people-leave-type-schema.json`. |
| `json-ld/` | `zoho-people-context.jsonld` — JSON-LD context aligning People entities with [schema.org](https://schema.org/) and the `zp:` namespace. |
| `vocabulary/` | `zoho-people-vocabulary.yml` — domain vocabulary keyed to the seven OAuth scopes. |
| `examples/` | `list-employees`, `apply-for-leave`, `check-in-out`, `list-leave-types`, `create-time-log`, `trigger-workflow`. |
| `plans/` | `zoho-people-plans-pricing.yml` — API Commons Plans profile (Free → Essential HR → Professional → Premium → Enterprise). |
| `rate-limits/` | `zoho-people-rate-limits.yml` — API Commons Rate Limits profile (token lifetime + per-plan ceilings; plan numbers flagged unverified). |
| `finops/` | `zoho-people-finops.yml` — FOCUS-aligned FinOps profile (per-user subscription, annual discount, cost drivers). |

## Provider properties indexed

- **Website** — https://www.zoho.com/people/
- **Pricing** — https://www.zoho.com/people/zohopeople-pricing.html
- **API Guide (5.0)** — https://help.zoho.com/portal/en/kb/people/api-guide
- **API overview** — https://www.zoho.com/people/api/overview.html
- **OAuth overview** — https://www.zoho.com/people/api/oauth.html
- **Scopes** — https://www.zoho.com/people/api/scopes.html
- **Integrations** — https://www.zoho.com/people/integrations.html
- **Status page** — https://status.zoho.com/ (RSS: https://status.zoho.com/rss)
- **Blog** — https://www.zoho.com/blog/people/
- **GitHub org** — https://github.com/zoho (237 public repos across the Zoho portfolio)

## Notable findings

- Verified seven OAuth scopes — the public scopes page enumerates `employee, forms, dashboard, automation, timetracker, attendance, leave`, which is the cleanest authoritative carve-up of the API surface.
- The API is bundled with **Essential HR, Professional, Premium, and Enterprise** plans (not Free), confirmed against the Zoho People 5.0 API Guide.
- Operates on Zoho's standard **multi-DC** topology: `.com / .eu / .in / .com.au / .jp / .com.cn / zohocloud.ca / .sa`.
- Integrations footprint spans Zoho Payroll, Zoho Recruit, Zoho Books, Zoho Sign, Microsoft 365, Google Workspace, Slack, MS Teams, Zapier, Zoho Flow, Adobe Sign, Docusign, QuickBooks, Xero, Paybooks, greytHR, Xoxoday, Vantage Circle, Zoho Vault, Zoho Directory.

## Notable absences

- **No public OpenAPI spec** shipped by Zoho People (unlike Zoho CRM which publishes one). The OpenAPI in this repo is reverse-engineered from the documented OAuth scopes and the canonical request/response patterns Zoho uses across its product line.
- **No dedicated GitHub org** for Zoho People — the `github.com/zoho` org carries CRM, Catalyst, SalesIQ, WorkDrive samples, but no People SDK.
- **No public per-call rate-limit table** — the pricing page only states that "API call limits increase substantially with higher plans."
- **No verifiable list prices** captured from the public pricing page in this run (toggle UI only); plan price fields in `plans/` are flagged `verified: false`.
- **No status-page RSS dedicated to People** — only the global `status.zoho.com/rss`.

## Maintainer

- [Kin Lane](https://apievangelist.com/) — kin@apievangelist.com
