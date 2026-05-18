# セットアップ手順

## 必要なもの

- [Obsidian](https://obsidian.md/) (Desktop)
- [Claude Code](https://docs.claude.com/en/docs/claude-code/overview) CLI
- `git` と（任意）`gh` CLI

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
