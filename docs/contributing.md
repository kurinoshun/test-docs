# ドキュメント投稿ガイド

このガイドでは、チームでドキュメントを管理・追加するための手順を説明します。

---

## 全体フロー

```
1. リポジトリをクローン（初回のみ）
        ↓
2. ブランチを作成
        ↓
3. docs/ 配下に .md ファイルを追加・編集
        ↓
4. ローカルで確認（任意）
        ↓
5. commit & push
        ↓
6. Pull Request を作成 → レビュー → マージ
        ↓
7. デプロイ（gh-deploy）
```

---

## 1. 初回セットアップ

### リポジトリのクローン

```bash
git clone https://github.com/kurinoshun/test-docs.git
cd test-docs
```

### MkDocs のインストール（ローカル確認する場合）

```bash
pipx install mkdocs
pipx inject mkdocs mkdocs-material
```

---

## 2. ブランチの作成

直接 `main` ブランチには commit せず、作業ブランチを作成してください。

```bash
git switch -c docs/your-topic
```

ブランチ名の例:

- `docs/api-reference`
- `docs/onboarding`
- `docs/fix-typo`

---

## 3. ドキュメントの追加・編集

### フォルダ構成のルール

`docs/` 配下にトピックごとにフォルダを作成してください。
フォルダ名・ファイル名は**英語・小文字・ハイフン区切り**にしてください（URLに使われるため）。

```
docs/
├── index.md               # トップページ
├── contributing.md        # このファイル
├── development/           # 開発関連
│   ├── intro.md
│   └── coding_standards.md
├── design/                # 設計関連（例）
│   └── architecture.md
└── api/                   # API関連（例）
    └── reference.md
```

### ファイルの追加

```bash
# フォルダがなければ作成
mkdir docs/design

# ファイルを作成
touch docs/design/architecture.md
```

### ファイルの先頭に H1 見出しを書く

MkDocs はファイルの `# 見出し`（H1）をページタイトルとして使用します。

```markdown
# アーキテクチャ概要

ここに内容を書く。
```

> **注意**: ファイルを追加するだけでサイドバーに自動反映されます。`mkdocs.yml` の編集は不要です。

---

## 4. ローカルで確認（任意）

```bash
mkdocs serve
```

ブラウザで `http://localhost:8000` を開いて表示を確認します。
ファイルを保存するたびにホットリロードされます。

---

## 5. commit & push

```bash
git add docs/design/architecture.md
git commit -m "docs: アーキテクチャ概要を追加"
git push origin docs/your-topic
```

### コミットメッセージの規則

| プレフィックス | 用途                     |
| -------------- | ------------------------ |
| `docs: `       | ドキュメントの追加・更新 |
| `fix: `        | 誤字・リンク修正         |
| `chore: `      | 設定ファイルの変更       |

---

## 6. Pull Request の作成

1. GitHub のリポジトリページを開く
2. `Compare & pull request` をクリック
3. 変更内容を説明して PR を作成
4. レビュアーをアサイン → レビュー・承認後にマージ

---

## 7. デプロイ

`main` ブランチにマージされたら、デプロイを実行します。

```bash
git switch main
git pull origin main
mkdocs gh-deploy
```

公開 URL:

```
https://kurinoshun.github.io/test-docs/
```

---

## よくある質問

### mkdocs.yml を毎回編集する必要がありますか？

不要です。`docs/` 配下にファイルを追加するだけで自動的にサイドバーに表示されます。

### サイドバーの表示順を変えたい場合は？

`mkdocs.yml` に `nav` セクションを追加することで順序や表示名を制御できます。通常は不要です。

### 画像を使いたい場合は？

`docs/images/` フォルダに画像を配置して参照してください。

```markdown
![説明](../images/example.png)
```
