---
name: weekly-report
description: Use when the user says「週次レポート作って」「週報まとめて」「今週のまとめ」to draft a reviewable weekly report from recent daily logs and wiki changes.
---

# weekly-report

## Default

Use the last 7 days including today unless the user specifies a date range.

## Workflow

Progress:
- [ ] Determine the report period.
- [ ] Read `daily/YYYY-MM-DD.md` files in the period.
- [ ] Identify `wiki/` pages modified in the period.
- [ ] Extract what changed, what was decided, and what remains unresolved.
- [ ] Draft `outbox/週次レポート_YYYY-MM-DD.md`.
- [ ] Mark the report as human-review required.

## Selection Rules

- Prefer durable knowledge, decisions, requirements, system changes, operations changes, and unresolved risks.
- Do not summarize every daily activity.
- Use full-path Wikilinks for referenced wiki pages.
- Separate facts from implications.
- Do not include sensitive internal URLs, credentials, customer information, or unmasked identifiers.

## Report Template

```markdown
---
title: 週次レポート YYYY-MM-DD → YYYY-MM-DD
date: YYYY-MM-DD
tags: [#週次レポート, #draft]
status: ドラフト（人間レビュー必須）
---

# 週次レポート YYYY-MM-DD → YYYY-MM-DD

> ⚠️ これは Codex が生成したドラフトです。必ず人間レビュー後に配布してください。

## エグゼクティブサマリ
- 3 行以内

## 今週の主要動向
1. **<トピック>** — [[wiki/...]]
   - 事実:
   - 含意:

## 領域別アップデート
### 調査・検証
### 要件・設計
### システム・運用

## 未決事項
- <確認が必要な項目>

## 出典
- daily/YYYY-MM-DD ...
- [[wiki/...]]
```

## Gotchas

- This is a draft, not a deliverable for external distribution.
- If a claim lacks a source in `daily/` or `wiki/`, list it under `未決事項` instead of presenting it as fact.
- Do not create new wiki knowledge while drafting the report; report from existing `daily/` and `wiki/`.

## Validation

Before reporting completion:
- [ ] The report file exists in `outbox/`.
- [ ] The report states the period and review-required status.
- [ ] All substantive claims cite `daily/` or `wiki/`.
- [ ] Sensitive internal details are absent or masked.

Report one line: `outbox/週次レポート_YYYY-MM-DD.md に出力しました。レビューしてください。`
