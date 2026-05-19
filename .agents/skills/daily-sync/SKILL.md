---
name: daily-sync
description: Use when the user says「日次更新して」「今日の差分を同期して」「daily syncして」to process unclassified daily work artifacts from inbox/drop/, update wiki/daily/outbox, and move processed files to inbox/processed/YYYY-MM-DD/.
---

# daily-sync

## Default

Read `inbox/drop/` first. Only if it is empty, read `inbox/daily-deltas/YYYY-MM-DD/` for backward compatibility.

The user should not classify, rename, or template files. Infer type and importance from content.

## Workflow

Progress:
- [ ] Determine target date; default to today.
- [ ] Read `inbox/drop/`; fallback to `inbox/daily-deltas/YYYY-MM-DD/` only if drop is empty.
- [ ] Classify each artifact by source and long-term value.
- [ ] Promote only reusable knowledge, decisions, requirements, system facts, and operations knowledge to `wiki/`.
- [ ] Preserve source evidence in `raw/` only when it is an original source worth citing.
- [ ] Append a sync log to `daily/YYYY-MM-DD.md`.
- [ ] Create `outbox/daily-summary_YYYY-MM-DD.md` only when a human-readable summary is useful.
- [ ] Move successfully processed `inbox/drop/` files to `inbox/processed/YYYY-MM-DD/`.

## Classification

| Content | Action |
|---|---|
| Meeting transcript or chat decision | Save citation source in `raw/meetings/`; synthesize only decisions, issues, and unresolved points into `wiki/` |
| Research notes or public references | Save citation source in `raw/news/` only if source URL/date is clear; otherwise record as unconfirmed in `daily/` |
| Local or remote workspace logs | Extract durable system, requirement, or operations knowledge; do not copy raw logs into `wiki/` |
| GitLab issue/MR/commit summaries | Extract design intent, review decisions, constraints, and system behavior; mask internal URLs/IDs |
| LLM chat logs | Capture reusable conclusions and adoption/rejection rationale; do not treat LLM output as primary evidence |
| TODOs, work-in-progress notes, unclear fragments | Record in `daily/` only; do not promote to `wiki/` |

## Wiki Graph Requirements

- Prefer updating existing pages over creating new pages.
- New pages must have frontmatter, required tags, and at least 3 full-path Wikilinks in the body.
- Add `aliases` for abbreviations, English/Japanese names, and likely search terms.
- When adding an important relation, link from the updated page to the related page and, when practical, add a backlink in the related page’s `関連` section.
- Do not turn daily activity logs into wiki nodes; only durable concepts, requirements, systems, operations, and decisions become nodes.

## Gotchas

- Never store unmasked internal URLs, tokens, credentials, IPs, hostnames, user IDs, or customer information.
- Treat research-tool and LLM outputs as secondary sources; promote only information with traceable evidence.
- Do not delete files. Move only processed `inbox/drop/` files after successful processing.
- Leave unreadable or ambiguous files in `inbox/drop/` and record the reason under `未確定`.
- Keep new wiki pages to 10 or fewer per run.

## Daily Log Template

```markdown
## 日次同期

- HH:MM /daily-sync
  - 入力: inbox/drop/ または inbox/daily-deltas/YYYY-MM-DD/
  - 更新: [[wiki/...]], [[wiki/...]]
  - 新規: [[wiki/...]]
  - 未確定: <確認が必要な項目>
```

## Validation

Before reporting completion:
- [ ] `daily/YYYY-MM-DD.md` contains the sync log.
- [ ] Every new wiki page has required frontmatter, tags, sources, aliases, and at least 3 full-path Wikilinks.
- [ ] No unmasked sensitive internal values were written.
- [ ] Processed drop files were moved to `inbox/processed/YYYY-MM-DD/`.
- [ ] Remaining drop files are explained in `daily/YYYY-MM-DD.md` as unresolved.

Report one line: `更新X件、新規Y件、未確定Z件。`
