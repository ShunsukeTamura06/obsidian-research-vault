# obsidian-research-vault

Andrej Karpathy の [LLM Wiki パターン](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) を
Obsidian + Claude Code で実装する vault テンプレート。

調査業務（市場リサーチ、AI動向ブリーフィング、銘柄分析など）で
**「毎回ゼロから再発見する」のではなく「合成済みの wiki が育っていく」**
ワークフローを最小構成で実現する。

## なぜ必要か

LLM はセッションを閉じれば文脈を忘れる。RAG も毎回ゼロから検索する。
このテンプレートは 3 層構造で、調査の蓄積を **コンパウンド** させる。

- **raw/** : 生の資料（記事、PDF、議事録）— Claude は読むだけ、書き換えない
- **wiki/** : Claude が合成し維持する Markdown ページ群
- **CLAUDE.md** : Claude の振る舞いを規定するスキーマ

詳細: [docs/PHILOSOPHY.md](docs/PHILOSOPHY.md)

## クイックスタート

```bash
# 1. clone
git clone https://github.com/ShunsukeTamura06/obsidian-research-vault.git my-vault
cd my-vault

# 2. kepano の obsidian-skills を追加（推奨）
git clone https://github.com/kepano/obsidian-skills.git .claude/skills-kepano

# 3. Obsidian でこのフォルダを Vault として開く
# 4. 同じディレクトリで claude を起動
claude
```

最初に Claude にこう言う:

```
CLAUDE.md を読んで、このvaultの運用ルールを把握して。
理解したら「準備完了」とだけ返事して。
```

## 基本的な使い方

| やりたいこと | コマンド |
|---|---|
| URL/PDF を取り込んで wiki を更新 | `URL を capture して` |
| 週次レポートのドラフト生成 | `週次レポート作って` |
| wiki の健全性チェック | `wiki を lint して` |

## フォルダ構造

```
.
├── CLAUDE.md       ← 運用ルール（最初に編集）
├── .claude/skills/ ← カスタムスキル
├── raw/            ← 生資料を投げ込む場所
├── wiki/           ← Claude が育てる知識ベース
├── daily/          ← 日次作業ログ
├── inbox/          ← 仮置き
└── docs/           ← このテンプレート自体のドキュメント
```

## カスタマイズ

最初の 1 週間で以下を自分の業務に合わせて編集:

1. **`CLAUDE.md`** — 出力ルール、禁止事項、命名規則
2. **`wiki/` 直下のサブフォルダ** — 自分の領域に合わせて改名
3. **`.claude/skills/`** — 自分の定型業務をスキル化

詳細: [docs/SETUP.md](docs/SETUP.md) → [docs/ROADMAP.md](docs/ROADMAP.md)

## ライセンス

MIT
