# minami-skills

kminami-tech 用のプライベート Claude Code プラグインマーケットプレース。

## 追加する

```bash
claude plugin marketplace add kminami-tech/minami-skills
claude plugin install git-workflow@minami-skills
claude plugin install learning@minami-skills
```

Claude Code のセッション内からは `/plugin` で追加・管理できる。

プライベートリポジトリなので、`gh auth` または git 認証情報で
kminami-tech のリポジトリを読める環境からのみ取得できる。

## プラグイン

### `git-workflow`

git 周りの文章を、実際の diff を読んで日本語で書く。どちらのスキルも
コマンドの実行はせず、文章を提示するところまでを担う。

| スキル | 内容 |
|---|---|
| `writing-conventional-commits` | ステージされた diff から Conventional Commits 形式のコミットメッセージを組む |
| `writing-pull-requests` | ベースブランチとの差分から PR のタイトルと説明文を組む |

### `learning`

新しい技術を、ユーザー自身が手を動かして学ぶのを支援する。Claude は調査・
ドキュメント作成・結果の分析を担い、コマンドの実行はユーザーが行う。

| スキル | 内容 |
|---|---|
| `hands-on-learning` | 学習用ドキュメントを 1 ステップずつ作り、実行結果を反映しながら進める。`/hands-on-learning` で呼んだときだけ動く |

## スキル単位の制御

プラグインを有効にしたまま、スキルごとに表示を変えられる。
`~/.claude/settings.json`（プロジェクト限定なら `.claude/settings.json`）に書く。

```json
{
  "skillOverrides": {
    "writing-pull-requests": "user-invocable-only"
  }
}
```

| 値 | 挙動 |
|---|---|
| `on`（既定） | 通常どおり |
| `name-only` | 一覧に出すが description を隠す |
| `user-invocable-only` | モデルからは見えず、`/名前` で呼んだときだけ動く |
| `off` | どちらからも見えない |

## 構成

```
.claude-plugin/marketplace.json     マーケットプレース定義
plugins/<plugin-name>/
  .claude-plugin/plugin.json        プラグイン定義
  skills/<skill-name>/SKILL.md      スキル本体
```

## スキルを追加する

同じ系統のスキルなら既存プラグインの `skills/` に足すだけでよい。
系統が違うなら新しいプラグインを作る。

1. `plugins/<plugin>/skills/<skill>/SKILL.md` を置く
2. 新しいプラグインなら `.claude-plugin/plugin.json` も作り、
   `.claude-plugin/marketplace.json` の `plugins` 配列に追記する
3. `plugin.json` と marketplace.json の `version` を上げる
4. push したら `claude plugin marketplace update minami-skills` で反映する
