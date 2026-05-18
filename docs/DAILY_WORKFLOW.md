# 日次自動更新ワークフロー

この vault の理想運用は、日中の業務を変えず、終業前に当日の差分だけを集めて Claude が wiki を更新する形にすること。

## 全体像

```text
通常業務
  ↓
17時前後に日次差分を収集
  ↓
inbox/daily-deltas/YYYY-MM-DD/ に配置
  ↓
Claude が daily-sync を実行
  ↓
wiki/ と daily/ と outbox/ が更新される
```

## 日中の運用

ユーザーは通常どおり業務する。

- 社内リポジトリでコードレビュー、Issue、Merge Request を扱う
- クラウド検証環境関連の調査や確認を行う
- 社内外の調査ツールで調査する
- 社内チャットで連絡する
- 会議・文字起こしツールで transcript を得る

日中に vault を逐次更新する必要はない。

## 終業前の差分配置

17時など帰る前に、当日の差分を次のフォルダへ置く。

```text
inbox/daily-deltas/YYYY-MM-DD/
```

例:

```text
inbox/daily-deltas/2026-05-18/
├── repo_change_summary.md
├── chat_decisions.md
├── meeting_transcript_project-a.md
├── research_notes.md
└── reference_links.md
```

このフォルダに置くファイルは、完全なレポートである必要はない。
Claude が分類できるように、日時、出典、対象プロジェクト、要点だけ分かればよい。

## Claude の実行

手動運用では、終業前に Claude Code へ次のように依頼する。

```text
日次更新して
```

自動運用では、OS のタスクスケジューラ、社内ジョブ、または Codex/Claude Code を起動するラッパースクリプトから、
同じ指示を定時実行する。

## 出力されるもの

### `wiki/`

当日の差分から、継続的に参照すべき知見だけが合成される。

例:
- API 仕様変更の背景
- プロジェクト固有の設計判断
- 調査で分かった技術的・業務的な論点
- 会議で決まった継続的に参照すべき事項

### `daily/YYYY-MM-DD.md`

当日の同期ログが残る。

```markdown
## 日次同期

- 17:00 /daily-sync
  - 入力: inbox/daily-deltas/2026-05-18/
  - 更新: [[wiki/...]], [[wiki/...]]
  - 新規: [[wiki/...]]
  - 未確定: <確認が必要な項目>
```

### `outbox/daily-summary_YYYY-MM-DD.md`

必要に応じて、人間が読むための日次サマリを出力する。

## 自動化の責務分担

| 役割 | 担当 |
|---|---|
| 日中の業務 | ユーザー |
| 差分ファイルの収集 | 手動、または社内スクリプト |
| 差分の配置 | `inbox/daily-deltas/YYYY-MM-DD/` |
| wiki 更新 | Claude の `daily-sync` skill |
| 最終確認 | ユーザー |

## 注意点

- `inbox/daily-deltas/` は入力置き場であり、実データは Git にコミットしない。
- 未マスクの社内 URL、内部識別子、認証情報、個人 ID は置かない。
- 調査ツールの回答は一次情報ではないため、裏取りできた内容だけ wiki に反映する。
- 会議 transcript は全文を wiki に転記せず、合意事項・論点・未決事項に要約する。
