---
name: daily-sync
description: 17時など終業前に inbox/daily-deltas/ の日次更新差分を読み、raw/・wiki/・daily/・outbox/ を更新する。「日次更新して」「今日の差分を同期して」「daily syncして」で起動する。
---

# daily-sync

## トリガー
- 「日次更新して」
- 「今日の差分を同期して」
- 「daily syncして」
- 17時など終業前の自動実行ジョブ

## 入力

`inbox/daily-deltas/YYYY-MM-DD/` 配下に置かれた当日の業務差分を対象にする。

想定する入力:
- 社内リポジトリの差分、Issue、Merge Request、commit log
- クラウド検証環境関連の調査メモ、ログ要約、API 仕様変更メモ
- 社内外の調査ツールで調べた結果のメモ
- 社内チャットの重要な決定事項・依頼事項
- オンライン会議・文字起こしツールのトランスクリプト

## 手順

### 1. 対象日と入力フォルダを確認

- 日付指定がなければ今日の日付を使う
- `inbox/daily-deltas/YYYY-MM-DD/` を確認する
- フォルダが無い、または空なら `daily/YYYY-MM-DD.md` に「差分なし」と記録し、wiki は更新しない

### 2. 差分を分類

| 内容 | 保存・反映先 |
|---|---|
| 会議 transcript、社内チャットの決定事項 | `raw/meetings/` |
| 調査メモ、検索結果、社内外の調査ツールの要点 | `raw/news/` または `inbox/` |
| 社内リポジトリの設計・実装上の知見 | `wiki/` の関連ページ |
| クラウド検証環境の仕様・運用知見 | `wiki/` の関連ページ |
| 出典や意味が不明な断片 | `daily/` に未確定として記録 |

### 3. wiki 更新

- 既存ページを優先して追記・修正する
- 新規ページは 1 日あたり最大 10 件まで
- 出典は `sources:` frontmatter または本文中に明示する
- 社内サービスの未マスク URL、認証情報、内部識別子、個人 ID は保存しない
- 調査ツールの回答は一次情報として扱わず、裏取りできた内容だけ wiki に反映する

### 4. daily ログ

`daily/YYYY-MM-DD.md` に以下を追記する:

```markdown
## 日次同期

- HH:MM /daily-sync
  - 入力: inbox/daily-deltas/YYYY-MM-DD/
  - 更新: [[wiki/...]], [[wiki/...]]
  - 新規: [[wiki/...]]
  - 未確定: <確認が必要な項目>
```

### 5. サマリ出力

必要に応じて `outbox/daily-summary_YYYY-MM-DD.md` を作成する。

```markdown
# 日次サマリ YYYY-MM-DD

## 今日増えた知見
- ...

## 更新した wiki
- [[wiki/...]]

## 明日確認すること
- ...
```

## 完了条件

- `inbox/daily-deltas/YYYY-MM-DD/` の入力を確認済み
- 必要な wiki 更新が完了している
- `daily/YYYY-MM-DD.md` に同期ログが残っている
- 未確定事項が明示されている
- ユーザーに「更新件数、新規件数、未確定件数」を 1 行で報告している

## やらないこと

- 未マスクの社内 URL、内部識別子、認証情報を保存しない
- `raw/` の既存ファイルを上書きしない
- 根拠がない内容を wiki に昇格しない
- 自動修正のために社内リポジトリやクラウド検証環境へ勝手に push・deploy しない
