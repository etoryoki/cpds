# リポジトリ構成

CPDS リポジトリの推奨ディレクトリ構成と、各ファイルの役割を説明します。

## 推奨ディレクトリ構成

```
cpds/
├── README.md                    # プロジェクトの顔(日本語、メイン)
├── README.en.md                 # 英語版 README(将来)
├── LICENSE                      # CC0 1.0
├── CONTRIBUTING.md              # 議論への参加方法
├── CHANGELOG.md                 # バージョン履歴
│
├── spec/
│   ├── cpds-v0.4.md            # 仕様書本体(現行版)
│   └── archive/                # 過去バージョン
│       ├── cpds-v0.1.md
│       ├── cpds-v0.2.md
│       └── cpds-v0.3.md
│
├── docs/
│   ├── index.html              # HTML プレゼン (GitHub Pages の公開対象)
│   ├── objections.md           # 想定反論集
│   ├── note-article.md         # note 記事原稿
│   ├── faq.md                  # FAQ(将来作成)
│   └── glossary.md             # 用語集(将来作成)
│
├── examples/                    # サンプルコード(将来)
│   ├── provenance-record.json
│   ├── delegation-cert.json
│   └── README.md
│
├── implementations/             # リファレンス実装(将来)
│   └── python/
│
└── .github/
    ├── ISSUE_TEMPLATE/
    │   ├── bug-report.md
    │   ├── design-question.md
    │   └── new-use-case.md
    └── workflows/
        └── pages.yml            # GitHub Pages 自動デプロイ
```

## GitHub Pages の設定

`docs/index.html` を GitHub Pages のソースに設定することで、HTML プレゼンを `https://[username].github.io/cpds/` で公開できます。

### 設定手順

1. リポジトリの Settings → Pages
2. Source: Deploy from a branch
3. Branch: `main`、Folder: `/docs`
4. Save

数分後、URL が発行されます。

## ファイルの配置順序(初期コミット)

最初にプッシュする内容の推奨順序:

### コミット 1: 骨格
```
LICENSE
README.md
.gitignore
```

最初のコミットで「プロジェクトの存在」を作る。README だけで、CPDS が何かが伝わる状態にする。

### コミット 2: 仕様本体
```
spec/cpds-v0.4.md
```

技術的な実体を追加する。これがあることで「真面目なプロジェクト」と認識される。

### コミット 3: 補足ドキュメント
```
docs/objections.md
docs/note-article.md
CONTRIBUTING.md
```

議論の素材を揃える。

### コミット 4: プレゼン
```
docs/index.html
```

GitHub Pages を有効化。

### コミット 5: 過去バージョン
```
spec/archive/cpds-v0.1.md
spec/archive/cpds-v0.2.md
spec/archive/cpds-v0.3.md
```

履歴を残す(透明性のため、こだわらなくてもよい)。

---

## ファイル間のリンク確認

各ファイルにあるリンクが正しく機能するか、初回プッシュ前に確認してください。

- `README.md` → `spec/cpds-v0.4.md` (相対パス)
- `README.md` → `docs/objections.md`
- `README.md` → `docs/note-article.md`
- `README.md` → `https://[username].github.io/cpds/` (GitHub Pages URL)
- `CONTRIBUTING.md` → 各種参照
- `docs/note-article.md` → GitHub URL

特に GitHub Pages の URL は、リポジトリ名とユーザー名/組織名で変わるので、確定後に置換してください。

---

## ブランチ戦略

シンプルに `main` ブランチだけで運用することを推奨します。理由:

- まだ実装はないので、`develop` ブランチは不要
- 仕様書は段階的に更新されるが、各バージョンはタグで管理可能
- 小規模プロジェクトでは、複雑なブランチ戦略は過剰

### タグ付け

各バージョンをリリースする際に Git タグを付けると、過去のバージョンを簡単に参照できます。

```bash
git tag -a v0.4 -m "CPDS Discussion Draft v0.4"
git push origin v0.4
```

GitHub の Releases として公開すれば、ダウンロード可能な ZIP も自動生成されます。

---

## Issue/PR テンプレート

`.github/ISSUE_TEMPLATE/` に以下のテンプレートを置くことを推奨します。

### bug-report.md

```markdown
---
name: 仕様の問題報告
about: 仕様書の矛盾、不明瞭な点、エラーを報告する
title: '[仕様] '
labels: 'spec-issue'
---

## 該当箇所

セクション番号、行数、または引用:

## 問題

何が問題か:

## 影響

この問題があるとどんな実害があるか:

## 改善提案(任意)

```

### design-question.md

```markdown
---
name: 設計判断への質問・議論
about: なぜこの設計なのか、別のアプローチはないか
title: '[設計] '
labels: 'design-discussion'
---

## 検討中の部分

どの設計判断について議論したいか:

## 現状の設計

CPDS では現在どうなっているか:

## 別のアプローチ

どんな代替案があり得るか:

## トレードオフ

各アプローチの長所・短所:

```

### new-use-case.md

```markdown
---
name: 新しいユースケースの提案
about: CPDS で扱うべき新しいシナリオを提案する
title: '[ユースケース] '
labels: 'use-case'
---

## シナリオ

どんな状況か、誰が関わるか:

## CPDS で何を解決するか

このユースケースで CPDS のどの機能が役立つか:

## 不足する機能

現状の CPDS では対応できない部分:

```

---

## メンテナンスの心構え

公開直後は、フィードバックが集中することがあります。

- すべての Issue にすぐ反応する必要はない
- 「読んだ」というリアクションだけでも、投稿者は安心する
- 答えに時間がかかる Issue は、ラベルだけ付けて「検討中」と伝える
- 議論の発展は、メンテナの応答速度よりも、コミュニティの質に依存する

無理せず、長期的に維持できるペースで運営することが、規格の信頼性につながります。
