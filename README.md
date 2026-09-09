# minami-skills

kminami-tech 用のプライベート Claude Code プラグインマーケットプレース。

## 追加する

```bash
claude plugin marketplace add kminami-tech/minami-skills
claude plugin install writing-conventional-commits@minami-skills
```

Claude Code のセッション内からは `/plugin` で追加・管理できる。

プライベートリポジトリなので、`gh auth` または git 認証情報で
kminami-tech のリポジトリを読める環境からのみ取得できる。

## プラグイン

| プラグイン | 内容 |
|---|---|
| `writing-conventional-commits` | ステージされた diff を読み、Conventional Commits 形式のコミットメッセージを組む（説明は日本語）。`git commit` は実行しない |

## 構成

```
.claude-plugin/marketplace.json     マーケットプレース定義
plugins/<plugin-name>/
  .claude-plugin/plugin.json        プラグイン定義
  skills/<skill-name>/SKILL.md      スキル本体
```

## プラグインを追加する

1. `plugins/<name>/` を作り、`.claude-plugin/plugin.json` と `skills/<name>/SKILL.md` を置く
2. `.claude-plugin/marketplace.json` の `plugins` 配列に追記する
3. push したら `claude plugin marketplace update minami-skills` で反映する
