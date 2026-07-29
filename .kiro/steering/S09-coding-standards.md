# コーディング規約

## 目的
既存コードベースとの統一性を維持する。

## ルール

### TypeScript/JavaScript
- ファイル命名: kebab-case（例: `user-profile.tsx`）
- コンポーネント命名: PascalCase（例: `UserProfile`）
- 関数命名: camelCase（例: `getUserProfile`）
- 定数命名: UPPER_SNAKE_CASE（例: `MAX_RETRY_COUNT`）
- 型/インターフェース命名: PascalCase（例: `UserProfile`, `IUserService`）

### import順序
1. Node.js標準モジュール
2. 外部ライブラリ（npm packages）
3. 内部モジュール（絶対パス）
4. 相対パスモジュール
5. 型定義（type imports）

各グループ間は空行で区切る。

### コメント
- 関数/コンポーネントには JSDoc/TSDoc コメントを付与
- 複雑なロジックにはインラインコメントで意図を説明
- TODOコメントには担当者と期限を付記: `// TODO(name): 説明 - 期限`

### エラーハンドリング
- try-catchは具体的なエラー型でcatchする
- エラーメッセージは日本語で、ユーザー向けとログ向けを分離
- 非同期処理のエラーは必ずハンドリングする

### Docusaurus固有ルール（このプロジェクト用）
- ブログ記事: `blog/YYYY-MM-DD-slug/index.md` の構造
- ドキュメント: `docs/` 配下にカテゴリディレクトリで整理
- 静的アセット: `static/` 配下に配置
- コンポーネント: `src/components/` 配下にPascalCaseディレクトリ
