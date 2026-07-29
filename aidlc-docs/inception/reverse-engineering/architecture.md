# System Architecture

## System Overview
FinOps Japan Community（finops-jp.github.io）の公式Webサイト。Docusaurus 3で構築された静的サイトで、GitHub Pagesにデプロイされている。FinOps Foundationの日本チャプターとして、FinOpsフレームワークの日本語ドキュメント、イベントブログ、スライド資料、メディア記事を提供する。

## Architecture Diagram

```
+-------------------+     +-------------------+     +-------------------+
|   Content (MD)    | --> |   Docusaurus 3    | --> |  GitHub Pages     |
|   blog/, docs/    |     |   Build (npm)     |     |  Static Hosting   |
+-------------------+     +-------------------+     +-------------------+
        |                          |
        v                          v
+-------------------+     +-------------------+
| Translation       |     | Visual Regression |
| Scripts (Python)  |     | Tests (Playwright)|
+-------------------+     +-------------------+
                                   |
                                   v
                          +-------------------+
                          | GitHub Actions    |
                          | CI/CD Pipeline    |
                          +-------------------+
```

## Component Descriptions

### Content Layer
- **Purpose**: マークダウンによるコンテンツ管理
- **Responsibilities**: FinOpsフレームワーク文書（docs/）、ブログ記事（blog/）、カスタムページ（src/pages/）
- **Content Types**: ドキュメント、ブログ、スライド資料ページ、メディア記事ページ
- **Type**: Content

### Application Layer (Docusaurus)
- **Purpose**: 静的サイト生成
- **Responsibilities**: ビルド、ルーティング、テーマ、プラグイン管理
- **Dependencies**: React 18, MDX 3, MUI Icons, Emotion CSS-in-JS
- **Plugins**: client-redirects, ideal-image
- **Type**: Application

### Testing Layer
- **Purpose**: ビジュアルリグレッションテスト
- **Responsibilities**: UIスナップショット比較、PR時の自動テスト実行
- **Dependencies**: Playwright (Chromium)
- **Type**: Quality Assurance

### Translation Layer
- **Purpose**: コンテンツ翻訳の自動化
- **Responsibilities**: 翻訳追跡、更新検出、AI翻訳
- **Dependencies**: Python scripts, glossary.json
- **Type**: Automation

### Infrastructure Layer
- **Purpose**: ホスティングとCI/CD
- **Responsibilities**: ビルド実行、デプロイ、テスト自動化
- **Dependencies**: GitHub Actions, GitHub Pages
- **Type**: Infrastructure

## Integration Points
- **External Services**: GitHub Pages（ホスティング）
- **External Links**: Connpass（イベント管理）、FinOps Foundation（本家サイト）
- **CI/CD Events**: push to main (deploy), pull_request (visual test)

## Key Design Decisions
- **日本語専用サイト**: i18n設定はja単一ロケール
- **静的サイト**: サーバーサイドロジックなし、全コンテンツは事前ビルド
- **Markdown-first**: docs/とblog/はMarkdownファイルで管理
- **カスタムページ**: slides、pressはReact/Markdownページとして実装
- **クライアントリダイレクト**: 旧URLからの移行対応をプラグインで処理
