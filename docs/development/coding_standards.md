# コーディング規約

## 目次

1. [はじめに](#はじめに)
2. [全般的な規則](#全般的な規則)
3. [命名規則](#命名規則)
4. [フォーマット](#フォーマット)
5. [コメント](#コメント)
6. [言語別規則](#言語別規則)

## はじめに

### 目的

このドキュメントは、プロジェクトにおけるコードの一貫性と可読性を保つためのガイドラインです。

### 適用範囲

- 本プロジェクトの全てのソースコード
- 設定ファイル
- ドキュメント

## 全般的な規則

### ファイル構成

- ファイルサイズは500行以下を目安とする
- UTF-8エンコーディングを使用する
- ファイル末尾に改行を入れる
- 行末の空白は削除する

### インデント

- スペース2個または4個（プロジェクトで統一）
- タブは使用しない

## 命名規則

### 基本原則

- 意味のある名前を付ける
- 略語は避ける（一般的なものを除く）
- 英語を使用する

### ケース規則

#### キャメルケース (camelCase)

```javascript
// 変数、関数
const userName = "John";
function getUserData() {}
```

#### パスカルケース (PascalCase)

```javascript
// クラス、コンポーネント
class UserProfile {}
```

#### スネークケース (snake_case)

```python
# Python変数、関数
user_name = 'John'
def get_user_data():
    pass
```

#### 定数

```javascript
// 大文字スネークケース
const MAX_RETRY_COUNT = 3;
const API_BASE_URL = "https://api.example.com";
```

## フォーマット

### 行の長さ

- 最大80-120文字（プロジェクトで統一）

### 空白行

- 関数と関数の間に1行
- 論理的なブロックの間に1行

### 括弧とスペース

```javascript
// Good
if (condition) {
  doSomething();
}

// Bad
if (condition) {
  doSomething();
}
```

## コメント

### 基本原則

- コードで表現できることはコメントしない
- **なぜ**そうしたかを書く（**何を**しているかではなく）

### ドキュメントコメント

```javascript
/**
 * ユーザー情報を取得する
 * @param {string} userId - ユーザーID
 * @returns {Promise<User>} ユーザーオブジェクト
 * @throws {Error} ユーザーが見つからない場合
 */
async function getUser(userId) {
  // 実装
}
```

### TODO コメント

```javascript
// TODO: キャッシュ機能を追加する (2024-01-15, @username)
// FIXME: エラーハンドリングを改善する
```

## 言語別規則

### JavaScript/TypeScript

- セミコロンを使用する
- シングルクォートを優先
- `const` を優先、次に `let`、`var` は使用しない
- アロー関数を活用する

```typescript
// Good
const users = ["Alice", "Bob"];
const getFirstUser = () => users[0];

// Bad
var users = ["Alice", "Bob"];
function getFirstUser() {
  return users[0];
}
```

### Python

- PEP 8 に従う
- インデントは4スペース
- 関数とクラスの定義の後に2行空ける

```python
def calculate_sum(numbers: list[int]) -> int:
    """数値リストの合計を計算する"""
    return sum(numbers)
```

### CSS/SCSS

- BEM記法を推奨
- プロパティはアルファベット順

```css
.block__element--modifier {
  background-color: #fff;
  color: #333;
  padding: 10px;
}
```

## Git コミットメッセージ

### フォーマット

```
<type>: <subject>

<body>

<footer>
```

### Type

- `feat`: 新機能
- `fix`: バグ修正
- `docs`: ドキュメント
- `style`: フォーマット
- `refactor`: リファクタリング
- `test`: テスト
- `chore`: 雑務

### 例

```
feat: ユーザー検索機能を追加

名前とメールアドレスで検索可能にした。
検索結果はページネーション対応。

Closes #123
```

## 参考資料

- Google Style Guide: https://google.github.io/styleguide/
- Airbnb JavaScript Style Guide: https://github.com/airbnb/javascript
- PEP 8: https://peps.python.org/pep-0008/
