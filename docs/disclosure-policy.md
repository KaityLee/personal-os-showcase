# Disclosure policy

What may be published in this repository, what must never be, and how to check before publishing.

## 1. Principle

Visibility is not a single `public` / `private` flag. It is a set of independent axes, each defaulting to the most conservative value. Content appears here only if **every** axis allows it **and** a person has approved it. This repository is a public destination, so it accepts only content that would qualify as `visibility: public`.

## 2. Exposure axes

Defined once for the whole project (Vault frontmatter, database columns, site content schema):

| Axis | Values | Default | Meaning |
|---|---|---|---|
| `visibility` | `private` \| `restricted` \| `public` | `private` | Who can see it. `restricted` means a specific audience or an unlisted link. |
| `audience` | List of tags, for example `self`, `recruiter`, `team`, `public` | `[self]` | Optional finer-grained audience. The tag set is extensible. |
| `publish_status` | `draft` \| `review` \| `approved` \| `published` \| `retracted` | `draft` | Position in the approval workflow. |
| `publish_targets` | List, for example `portfolio-web` | `[]` | Channels the content may be published to. Empty means nowhere. |
| `ai_access` | `none` \| `local-only` \| `cloud-allowed` | `local-only` | Where AI processing may send the content. `none`: never used by AI. `local-only`: only models running on the private backend. `cloud-allowed`: may be sent to an external model API. |
| `pii` | boolean | `false` | The content contains personal data. Content with `pii: true` is never published. |
| `license` | SPDX identifier | none; `CC-BY-4.0` for public writing | License under which published content is offered. |

Publishing needs more than `visibility: public`: the item must also have `publish_status: approved` and be listed in the per-target allowlist in the private Vault. Public repositories then validate the copy again in CI.

## 3. What may be published here

The repository must satisfy: `visibility: public`, `pii: false`, `publish_status: approved`, a `license`, and no entry from section 4.

| Allowed | Conditions |
|---|---|
| Architecture descriptions and diagrams | Generic component names only; no real network layout. Placeholders for anything environment-specific. |
| Design decisions | As public ADRs under [decisions](decisions/README.md); sensitive parts replaced by summaries. |
| Anonymized benchmarks | Measured on synthetic or public data; each number with unit, measurement date, and environment class. See [benchmarks](benchmarks/README.md). |
| Screenshots and demos | Only of synthetic or public content; checked per section 5. |
| Data model and API shape | Schema names and generic examples; no real records. |
| Lessons learned | Written without naming employers, clients, or colleagues. |

## 4. What must never be published here

| Never | Examples (generic) |
|---|---|
| Personal notes | Anything from the Vault that is not an approved, allowlisted, public item; journal entries; career or personal reflections |
| Paths, hosts, tokens | Real filesystem paths, usernames, hostnames, IP addresses, tailnet names, internal URLs, API keys, tokens, passwords, `.env` values, certificates |
| Company and customer information | Employer names, client or customer names, internal project names, internal systems, anything covered by a confidentiality obligation |
| Personal contact details | Email addresses, phone numbers, home or work addresses |
| Private ADR originals | The original text of any decision record in the private repository (only redacted public copies are allowed) |
| Real data in examples | Query logs, chat history, database dumps, or embeddings derived from private notes |

## 5. Anonymization rules

- Replace environment-specific values with placeholders: `<owner>`, `<host>`, `<tailnet>`, `/path/to/vault`, `example.com`.
- Prefer synthetic corpora and queries for demos and benchmarks. Do not use real notes, even "just a few".
- **Screenshots:** crop to the relevant area; check window titles, tab titles, file paths, usernames, notifications, menu bar items, and recently opened files. Strip image metadata (EXIF) before committing.
- **Terminal output and logs:** review every line; redact before pasting.
- **Diagrams:** label with component roles, not machine names or addresses.
- When a detail is sensitive but the point stands without it, summarize instead of quoting.

## 6. Pre-publication checklist

Complete before every commit that copies or derives content from a private source. All items must be checked.

- [ ] The source item has `visibility: public`, `pii: false`, and `publish_status: approved`, and a `license` is set.
- [ ] For Vault notes: the item is in the allowlist for this target.
- [ ] No path, username, hostname, IP address, tailnet name, or internal URL (search the diff for `/Users/`, `/home/`, `.local`, `100.`, `http://`).
- [ ] No token, key, password, or `.env` value; a local secret scan of the diff came back clean.
- [ ] No company, client, customer, or colleague name; no internal project names.
- [ ] No personal contact details or personal-note content.
- [ ] Every number states its unit and measurement date; costs are in USD with the date.
- [ ] Screenshots and images were checked per section 5 and have no metadata.
- [ ] Examples use placeholders or synthetic data.
- [ ] ADR copies follow [decisions](decisions/README.md) (number kept, redaction marked, public date recorded).
- [ ] Mermaid blocks parse; every relative link resolves.
- [ ] `README.md` and `README.ko.md` are consistent if either changed.
- [ ] A second read-through of the full diff was done as a reader who does not know the author.

## 7. If something sensitive was published

1. **Revoke or rotate** any exposed credential first. Deleting a commit does not un-leak a secret: clones, caches, and forks may already hold it.
2. Remove the content from the repository and, if needed, rewrite history; ask the platform to purge cached views.
3. Record what happened and what was changed in the private repository (not here).
4. Add a checklist item or automated check that would have caught it.
