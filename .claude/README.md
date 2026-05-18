# .claude/

このディレクトリは Claude Code 用の設定とスキルを格納する。

## skills/

カスタムスキル。各スキルは `<name>/SKILL.md` の形式で配置。
frontmatter の `description` に書かれたトリガー句で起動する。

## skills-kepano/ （別途追加）

Obsidian CEO Kepano 製の公式スキル。clone して配置:

```bash
git clone https://github.com/kepano/obsidian-skills.git .claude/skills-kepano
```

これを入れると Claude が Wikilinks・Callouts・Bases・JSON Canvas を
ネイティブに扱えるようになる。**強く推奨**。
