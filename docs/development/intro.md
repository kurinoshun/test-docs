# MkDocs 導入・設定手順（GitHub Pages 公開）

本ドキュメントは、社内開発ドキュメントを **MkDocs + GitHub Pages** で管理・公開するための初期導入から公開までの手順をまとめたものです。

---

## 対象環境

- Windows 10 / 11
- WSL（Ubuntu）
- GitHub（Public / Private どちらも可）

---

## 1. 全体構成

```
開発者PC（Windows + WSL）
└ MkDocs（pipx）
    ↓
GitHub Repository
├ main ブランチ（Markdown管理）
└ gh-pages ブランチ（静的HTML）
    ↓
GitHub Pages（公開サイト）
```

---

## 2. 前提条件

- GitHub アカウント
- Git が利用できること
- WSL（Ubuntu）が利用できること

### Python バージョン確認（WSL）

```bash
python3 --version
```

**推奨**: Python 3.8 以上

---

## 3. pipx のインストール（推奨）

MkDocs は CLI ツールのため、`pipx` を使用してインストールします。

```bash
sudo apt update
sudo apt install -y pipx
pipx ensurepath
```

> **注意**: インストール後、ターミナルを再起動してください。

---

## 4. MkDocs のインストール

```bash
pipx install mkdocs
pipx inject mkdocs mkdocs-material
```

### 確認

```bash
mkdocs --version
```

---

## 5. MkDocs プロジェクト作成

```bash
mkdocs new test-docs
cd test-docs
```

### 生成される構成

```
test-docs/
├── docs/
│   └── index.md
├── mkdocs.yml
└── README.md
```

---

## 6. 基本設定（日本語 + Material テーマ）

`mkdocs.yml` を以下のように設定します。

```yaml
site_name: 社内開発ドキュメント

theme:
  name: material
  language: ja

nav:
  - ホーム: index.md
```

---

## 7. ローカル確認

```bash
mkdocs serve
```

### ブラウザで確認

```
http://localhost:8000
```

---

## 8. GitHub リポジトリ作成

1. GitHub にログイン
2. 新規リポジトリ作成
   - **Repository name**: `test-docs`
   - **README**: 作成しない
   - **Public / Private**: 用途に応じて選択

---

## 9. GitHub へ push

```bash
git init
git add .
git commit -m "init mkdocs project"
git branch -M main
git remote add origin https://github.com/<user>/test-docs.git
git push -u origin main
```

> **注意**: `<user>` は自分の GitHub ユーザー名に置き換えてください。

---

## 10. GitHub Pages 公開（初回）

### Personal Access Token（PAT）を使用

1. GitHub Settings → Developer settings → Personal access tokens → Tokens (classic)
2. **Generate new token**
3. 設定項目：
   - **Repository access**: Only select repositories
   - **Permissions**:
     - **Contents**: Read and write

### デプロイ実行

```bash
mkdocs gh-deploy
```

### 成功すると

- `gh-pages` ブランチが作成される
- GitHub Pages が自動的に有効化される

### 公開 URL

```
https://<user>.github.io/test-docs/
```

---

## 11. 日常運用フロー

### ドキュメント編集

```bash
# docs/ 配下の .md ファイルを編集
vim docs/index.md
```

### ローカル確認

```bash
mkdocs serve
```

### GitHub へ反映

```bash
git add .
git commit -m "update documentation"
git push origin main
```

### GitHub Pages へデプロイ

```bash
mkdocs gh-deploy
```

---

## トラブルシューティング

### `mkdocs` コマンドが見つからない

```bash
pipx ensurepath
# ターミナル再起動
```

### デプロイ時に認証エラー

- Personal Access Token（PAT）の権限を確認
- `git remote -v` で URL を確認（HTTPS / SSH）

### GitHub Pages が表示されない

1. リポジトリ Settings → Pages
2. Source が `gh-pages` ブランチになっているか確認

---

## 参考リンク

- [MkDocs 公式ドキュメント](https://www.mkdocs.org/)
- [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)
- [GitHub Pages ドキュメント](https://docs.github.com/ja/pages)

---

**作成日**: 2026-02-10  
**更新日**:
