# Mermaidダイアグラムデモ

MkDocsのMermaidプラグインを使用して、様々な図表を作成できます。以下は代表的な例です。

## フローチャート

システムの処理フロー:

```mermaid
flowchart TD
    A[開始] --> B{ユーザー認証}
    B -->|成功| C[ダッシュボード表示]
    B -->|失敗| D[エラー表示]
    C --> E{データ取得}
    E -->|成功| F[データ表示]
    E -->|失敗| G[キャッシュから表示]
    D --> H[終了]
    F --> H
    G --> H
```

## シーケンス図

ユーザーとシステムの相互作用:

```mermaid
sequenceDiagram
    participant ユーザー
    participant Web
    participant API
    participant DB

    ユーザー->>Web: ページアクセス
    Web->>API: データ要求
    API->>DB: クエリ実行
    DB-->>API: 結果返却
    API-->>Web: JSON返却
    Web-->>ユーザー: ページ表示
```

## ガントチャート

プロジェクトスケジュール:

```mermaid
gantt
    title プロジェクト計画
    dateFormat YYYY-MM-DD

    section 設計
    要件定義           :des1, 2024-01-01, 30d
    基本設計           :des2, after des1, 30d

    section 開発
    バックエンド開発   :dev1, 2024-02-01, 60d
    フロントエンド開発 :dev2, 2024-02-15, 50d

    section テスト
    ユニットテスト     :test1, after dev1, 30d
    統合テスト         :test2, after test1, 20d

    section リリース
    リリース準備       :rel1, after test2, 10d
    本番リリース       :rel2, after rel1, 5d
```

## クラス図

オブジェクト指向設計:

```mermaid
classDiagram
    class User {
        -id: int
        -name: string
        -email: string
        +getId() int
        +getName() string
    }

    class Post {
        -id: int
        -title: string
        -content: string
        -authorId: int
        +getTitle() string
        +getAuthor() User
    }

    class Comment {
        -id: int
        -text: string
        -postId: int
        +getText() string
    }

    User "1" --> "*" Post: 作成
    Post "1" --> "*" Comment: 含む
```

## 状態図

アプリケーションの状態遷移:

```mermaid
stateDiagram-v2
    [*] --> Idle

    Idle --> Loading: ユーザー操作
    Loading --> Success: データ取得完了
    Loading --> Error: エラー発生

    Success --> Processing: 処理開始
    Processing --> Idle: 処理完了

    Error --> Retry: リトライ
    Retry --> Loading

    Idle --> [*]: 終了
```

## ER図

データベース設計:

```mermaid
erDiagram
    USERS ||--o{ POSTS : creates
    USERS ||--o{ COMMENTS : writes
    POSTS ||--o{ COMMENTS : has

    USERS {
        int id PK
        string name
        string email UK
        datetime created_at
    }

    POSTS {
        int id PK
        int user_id FK
        string title
        string content
        datetime created_at
    }

    COMMENTS {
        int id PK
        int post_id FK
        int user_id FK
        string text
        datetime created_at
    }
```

## パイチャート

機能別の開発時間配分:

```mermaid
pie title 開発時間配分
    "API開発" : 35
    "フロントエンド" : 30
    "テスト" : 20
    "ドキュメント" : 10
    "その他" : 5
```

## ビットマップガントチャート

複数プロジェクトの管理:

```mermaid
gitGraph
    commit id: "初回提交"
    commit id: "機能A実装"

    branch feature/user-auth
    checkout feature/user-auth
    commit id: "認証機能1"
    commit id: "認証機能2"

    checkout main
    commit id: "バージョンアップ"

    merge feature/user-auth
    commit id: "テスト完了"
```

## マインドマップ

プロジェクト計画の俯瞰:

```mermaid
mindmap
  root((Webアプリ開発))
    設計
      要件分析
      アーキテクチャ設計
      DB設計
    開発
      バックエンド
        API
        DB
      フロントエンド
        UI
        状態管理
    品質
      ユニットテスト
      統合テスト
      パフォーマンステスト
    運用
      ドキュメント作成
      本番デプロイ
      監視設定
```

## 利点

Mermaidプラグインを使用することで：

- **コード化**: 図表をマークダウンで管理できます
- **バージョン管理**: Gitで変更履歴を追跡できます
- **保守性**: 図表の修正が容易です
- **一貫性**: スタイルが統一されます
- **共有性**: ドキュメントに直接埋め込めます

詳細は[Mermaid公式サイト](https://mermaid.js.org/)を参照してください。
