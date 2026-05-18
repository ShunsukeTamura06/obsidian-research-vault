# .claude/

このディレクトリは Claude Code 用の設定とスキルを格納する。

## skills/

カスタムスキル。各スキルは `<name>/SKILL.md` の形式で配置。
frontmatter の `description` に書かれたトリガー句で起動する。

標準で含まれるスキル:
- `capture/`: 個別 URL、PDF、テキストを取り込む
- `daily-sync/`: 終業前の日次差分から vault を更新する
- `weekly-report/`: 週次レポートのドラフトを作る
- `lint-wiki/`: wiki の健全性を検査する

## skills-kepano/ （別途追加）

Obsidian CEO Kepano 製の公式スキル。clone して配置:

```bash
git clone https://github.com/kepano/obsidian-skills.git .claude/skills-kepano
```

これを入れると Claude が Wikilinks・Callouts・Bases・JSON Canvas を
ネイティブに扱えるようになる。**強く推奨**。
