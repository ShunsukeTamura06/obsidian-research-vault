---
name: lint-wiki
description: Use when the user says「wikiをlintして」「wikiチェックして」「wikiの健全性確認」to inspect wiki structure, Obsidian graph quality, frontmatter, sources, and likely stale or inconsistent content without auto-fixing.
---

# lint-wiki

## Default

Detect and report. Do not modify wiki files unless the user explicitly asks for fixes after reviewing the report.

## Workflow

Progress:
- [ ] Scan `wiki/` Markdown files.
- [ ] Extract frontmatter, tags, aliases, sources, and Wikilinks.
- [ ] Check structural problems.
- [ ] Check graph quality problems.
- [ ] Flag content risks best-effort.
- [ ] Write `outbox/lint-report_YYYY-MM-DD.md`.

## Checks

| Category | Detect |
|---|---|
| Broken links | `[[...]]` targets that do not exist |
| Orphan pages | Pages with no incoming wiki links |
| Weak graph nodes | New or concept pages with fewer than 3 related Wikilinks |
| Missing backlinks | Important one-way relationships that should be navigable both ways |
| Frontmatter | Missing `title`, `date`, `tags`, `aliases`, or `sources` when required |
| Tag rules | Missing `#requirements`, `#system`, `#operations`, `#decision`, or `#concept` by folder/type |
| Source gaps | Numbers, claims, or named entities without source evidence |
| Stale wording | Old pages using terms like 最新, 今後, 現在 without dates |
| Contradictions | Pages that appear to state conflicting facts about the same entity/date |

## Report Template

```markdown
# wiki lint レポート YYYY-MM-DD

## 構造的問題
### リンク切れ
### 孤立ページ
### frontmatter 不備

## グラフ品質
### リンク不足ページ
### 戻りリンク不足

## 内容的問題（要確認）
### 出典欠如
### 古い可能性がある記述
### 矛盾の可能性

## 推奨アクション
- 優先度順に 3-5 件
```

## Gotchas

- `raw/`, `daily/`, `inbox/`, and `outbox/` are not wiki graph targets.
- Full-path Wikilinks are required; short ambiguous links are findings.
- The report may flag possible contradictions; do not present them as proven facts.
- Do not auto-fix, because link changes can alter the knowledge graph.

## Validation

Before reporting completion:
- [ ] `outbox/lint-report_YYYY-MM-DD.md` exists.
- [ ] Counts are included for each finding category.
- [ ] Findings include concrete file paths or Wikilinks.
- [ ] Recommended actions are prioritized.

Report one line: `リンク切れX件、孤立Y件、frontmatter不備Z件、要確認N件。`
