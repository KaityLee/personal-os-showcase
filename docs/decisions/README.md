# Public decision records

This directory holds **public copies** of architecture decision records (ADRs) whose originals live in the private repository. The originals stay private and authoritative; a public copy is a reviewed, redacted edition.

## Status

No decision records have been published yet.

| ADR | Title | Status | Decided (UTC) | Published (UTC) |
|---|---|---|---|---|
| — | — | — | — | — |

Add one row per published ADR, sorted by number.

## Rules for copying a private ADR

1. **Gate.** The private ADR must have `visibility: public`, `pii: false`, and `publish_status: approved`. The copy must pass the [disclosure policy](../disclosure-policy.md) checklist. Never copy an ADR that is not approved.
2. **Keep the number.** ADR-003 in the private repository is ADR-003 here. Never renumber. Gaps are expected (some ADRs stay private) and need no explanation.
3. **File name.** `ADR-NNN-kebab-case-title.md`, ASCII only, matching the private file name unless the private name itself contains sensitive wording. The original-language title goes in `title`.
4. **Replace sensitive parts with summaries, not black bars.** Replace the passage with a short neutral summary that preserves the reasoning, and mark it with a blockquote beginning `Redacted summary:`. Do not leave struck-through text, truncated sentences, or comments containing the original.
5. **Record dates.** Keep the original decision date and add the public date. Both are ISO 8601 dates in UTC.
6. **Header block.** Every public ADR starts with the metadata block below.
7. **No silent edits.** After publication, corrections are appended under a `## Revisions` heading with the date, not applied invisibly. If a decision is superseded, update `status` and link to the new ADR.
8. **Language.** English. If the original is Korean, translate and set `lang: en`; mention the original language in `source_lang`.
9. **Links.** Link only to public documents. Links to private files are replaced by a plain-text description.
10. **Index.** Update the table above in the same change.

## Template

```markdown
---
adr: NNN
title: <Title in English>
lang: en
source_lang: <BCP 47 tag of the private original, for example ko>
status: accepted        # proposed | accepted | superseded | deprecated
superseded_by: null     # for example ADR-NNN
decided_on: YYYY-MM-DD  # date of the original decision, UTC
published_on: YYYY-MM-DD  # date this public copy was published, UTC
redacted: true          # true if any passage was replaced by a summary
license: <SPDX-id>
---

# ADR-NNN: <Title in English>

## Context

...

## Decision

...

> Redacted summary: <one or two neutral sentences that keep the reasoning and drop the sensitive detail>

## Consequences

...

## Revisions

- YYYY-MM-DD: <what changed and why>
```

Every value above is a placeholder; this template is not a published record.
