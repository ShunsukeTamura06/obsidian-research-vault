# セットアップ手順

## 必要なもの

- [Obsidian](https://obsidian.md/) (Desktop)
- [Claude Code](https://docs.claude.com/en/docs/claude-code/overview) CLI
- `git` と（任意）`gh` CLI
- 社内リモートリポジトリへのアクセス権限
- 社内チャット、会議ツール、文字起こしツール、調査ツールへの業務利用権限

## ステップ

### 1. clone

```bash
git clone https://github.com/ShunsukeTamura06/obsidian-research-vault.git my-research-vault
cd my-research-vault
```

### 2. kepano の Obsidian スキルを追加（推奨）

```bash
git clone https://github.com/kepano/obsidian-skills.git .claude/skills-kepano
```

これを入れると Claude が Wikilink・Callout・JSON Canvas・Bases を
正確に書けるようになる。`.gitignore` で除外済みなので fork した
リポジトリには含まれない。

### 3. Obsidian で開く

Obsidian → Open folder as vault → `my-research-vault` を選択

最初のプラグイン推奨:
- Dataview （DataviewJS でクエリビューを書く場合）
- Templater （日次ノートのテンプレ）

### 4. Claude Code を同じディレクトリで起動

```bash
claude
```

最初にこう言う:

```
CLAUDE.md を読んで、このvaultの運用ルールを把握して。
理解したら「準備完了」とだけ返事して。
```

### 5. 試運転

何か URL を 1 つ用意して:

```
これ capture して: https://...
```

`raw/news/` にファイルができ、`wiki/` のどこかが更新され、
`daily/YYYY-MM-DD.md` にログが残っていれば成功。

### 6. 日次同期の試運転

終業前の差分を `inbox/daily-deltas/YYYY-MM-DD/` に置き、Claude に依頼する:

```text
日次更新して
```

`daily/YYYY-MM-DD.md` に同期ログができ、必要な `wiki/` が更新されれば成功。

## 会社環境での使い方

ローカル業務環境では、社内で別途共有されるワークスペース配下にプロジェクトを置く。
具体的なユーザー ID、クラウド検証環境のホスト、社内 URL はテンプレート内に実値で記録しない。

社内リモートリポジトリを使う場合は、空リポジトリを作成し、以下のように remote を設定する:

```bash
git remote add origin <社内リポジトリURL>
git push -u origin main
```

調査素材は、社内外の調査ツール、社内チャット、会議・文字起こしツールから取得し、
`CLAUDE.md` の情報源ルールに従って `raw/` と `wiki/` に分離する。

終業前の自動更新を行う場合は、社内スクリプトやタスクスケジューラで当日の差分を
`inbox/daily-deltas/YYYY-MM-DD/` に出力し、Claude の `daily-sync` を定時実行する。
詳細は [DAILY_WORKFLOW.md](DAILY_WORKFLOW.md) を参照。

## カスタマイズ

最初の 1 週間で **必ず** 編集する:

### `CLAUDE.md`
- 自分の業務領域の語彙を「出力ルール」に追加
- 業界特有の禁止事項を追加（例: 銀行なら未公表情報の扱い）
- 必要なら frontmatter 必須項目を追加

### `wiki/` のサブフォルダ
- 自分の領域に合わせて改名（例: `銘柄/` → `企業/`）
- 新規領域を追加（例: `論文/`、`OSS/`）

### `.claude/skills/`
- 自分の定型業務をスキル化
- 既存の 3 スキルをコピーして改造するのが最短
