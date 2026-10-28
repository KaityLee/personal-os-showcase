# AGENTS.md

Rules for contributors and coding agents working in this repository.

## Scope

This is a **public, documentation-only** repository (Markdown and diagrams, no application code). Everything committed here is visible to the world, permanently. When in doubt, leave it out.

## Rules

### 1. No sensitive information

Never write any of the following, in text, diagrams, screenshots, examples, or commit messages:

- Real filesystem paths, usernames, or machine names
- Hostnames, IP addresses, tailnet names, internal URLs, ports of real deployments
- Tokens, API keys, passwords, certificates, `.env` values (key *names* are fine, values never)
- Company names, client or customer names, internal project names, colleagues' names
- Personal contact details (email, phone, address) and personal notes

Use placeholders instead: `<owner>`, `<host>`, `<tailnet>`, `/path/to/vault`, `example.com`.

### 2. Copying from private repositories requires the disclosure policy

Before copying or paraphrasing anything from a private repository (design documents, ADRs, notes, benchmark logs, screenshots), it must pass [docs/disclosure-policy.md](docs/disclosure-policy.md), including its pre-publication checklist. ADRs follow [docs/decisions/README.md](docs/decisions/README.md) in addition.

### 3. Numbers carry date and unit

Every number must state what it measures, its **unit**, and its **measurement date** (ISO 8601, UTC). Monetary values are in **USD** and include the date of measurement and the pricing date. Never present an estimate as a measurement; mark it as an estimate. See [docs/benchmarks/README.md](docs/benchmarks/README.md).

### 4. Globalization baseline

- Times and dates: UTC, ISO 8601 (`2026-10-28T01:23:45Z`, or `2026-10-28` for dates).
- Languages: BCP 47 tags (`ko`, `en`).
- File and directory names: ASCII kebab-case.
- Do not hardcode region-dependent values (currency, units, time zones) without stating them.

### 5. Language

Documents under `docs/` are written in English. `README.md` (English) and `README.ko.md` (Korean) must be kept in sync: change one, update the other in the same change.

### 6. Documents must be self-consistent

- Diagrams use fenced ```` ```mermaid ```` blocks and must parse.
- Every relative link must point to an existing file.
- Anything described as a plan or design must not read as an implemented, measured fact.

### 7. Working practices

- Do not delete or overwrite existing files without approval.
- Do not push, publish, or deploy without approval.
- Report what you changed.
