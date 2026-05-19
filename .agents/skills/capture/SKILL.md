---
name: capture
description: Use when the user says「captureして」「これ取り込んで」「rawに入れて」「これ整理して」with a URL, PDF path, file path, or pasted text to preserve a source and synthesize reusable wiki knowledge.
---

# capture

## Default

Use `capture` for a specific source. For messy daily work artifacts, prefer `daily-sync` through `inbox/drop/`.

## Workflow

Progress:
- [ ] Acquire the source from URL, local path, PDF, or pasted text.
- [ ] Classify the source and choose a destination.
- [ ] Extract the subject, named entities, concepts, dates, numbers, claims, and evidence.
- [ ] Search `wiki/` for affected pages; target 5-15 candidates when available.
- [ ] Update existing wiki pages first; create new pages only for durable concepts.
- [ ] Append a `/capture` log to `daily/YYYY-MM-DD.md`.

## Destination Defaults

| Source type | Destination |
|---|---|
| Public article, official documentation, research note | `raw/news/` |
| Disclosure, earnings, IR, statutory filing | `raw/disclosures/` |
| Meeting transcript, minutes, chat decision | `raw/meetings/` |
| Unclear or low-evidence material | `inbox/` or `daily/` as unconfirmed |

Use filename format `YYYY-MM-DD_short-slug.md`. Do not overwrite existing `raw/` files.

## Wiki Graph Requirements

- Preserve facts and inferences separately.
- Add source links through `sources:` frontmatter or body citations.
- Use full-path Wikilinks, e.g. `[[systems/顧客管理API]]`.
- New wiki pages must include required frontmatter, required tag, useful `aliases`, and at least 3 related Wikilinks.
- Add backlinks on related pages when the relation is important and the edit is small.
- Do not create more than 10 new wiki pages from one source.

## Gotchas

- Never add information without a source.
- Mask internal URLs, credentials, hostnames, IPs, user IDs, and customer information.
- Do not treat LLM or research-tool output as primary evidence.
- Do not rewrite existing wiki pages wholesale; append or make focused edits.

## Daily Log Template

```markdown
- HH:MM /capture: <ソース1行サマリ>
  - source: [[raw/news/YYYY-MM-DD_slug]]
  - 更新: [[wiki/...]], [[wiki/...]]
  - 新規: [[wiki/...]]
  - 未確定: <確認が必要な項目>
```

## Validation

Before reporting completion:
- [ ] Source handling is explicit: saved to `raw/`, left in `inbox/`, or recorded as unconfirmed.
- [ ] At least one wiki page was updated when reusable knowledge exists.
- [ ] New wiki pages are not isolated and have at least 3 full-path Wikilinks.
- [ ] `daily/YYYY-MM-DD.md` contains the capture log.

Report one line: `更新X件、新規Y件、未確定Z件。`
