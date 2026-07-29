# Technology Stack

## Programming Languages
| 言語 | バージョン | 用途 |
|---|---|---|
| TypeScript | ~5.6.2 | アプリケーションコード、設定ファイル |
| JavaScript | - | ビルドスクリプト |
| Python | - | 翻訳管理スクリプト |

## Frameworks
| フレームワーク | バージョン | 用途 |
|---|---|---|
| Docusaurus | ^3.5.2 | 静的サイトジェネレーター |
| React | ^18.0.0 | UIフレームワーク |
| MDX | ^3.0.0 | Markdownコンテンツ拡張 |

## UI Libraries
| ライブラリ | バージョン | 用途 |
|---|---|---|
| @mui/icons-material | ^7.0.0 | Material UIアイコン |
| @mui/styled-engine | ^7.0.0 | スタイリングエンジン |
| @emotion/react | ^11.14.0 | CSS-in-JS |
| @emotion/styled | ^11.14.0 | Styled Components |

## Docusaurus Plugins
| プラグイン | バージョン | 用途 |
|---|---|---|
| @docusaurus/plugin-client-redirects | ^3.5.2 | URL旧パスからのリダイレクト |
| @docusaurus/plugin-ideal-image | ^3.5.2 | 画像最適化（レスポンシブ） |
| @docusaurus/preset-classic | ^3.5.2 | 標準プリセット（docs, blog, pages, theme） |

## Utilities
| ライブラリ | バージョン | 用途 |
|---|---|---|
| clsx | ^2.0.0 | クラス名結合 |
| prism-react-renderer | ^2.3.0 | コードシンタックスハイライト |
| react-split | ^2.0.0 | パネル分割UI |

## Build Tools
| ツール | バージョン | 用途 |
|---|---|---|
| npm | - | パッケージマネージャー |
| TypeScript Compiler (tsc) | ~5.6.2 | 型チェック（typecheck スクリプト） |

## Testing Tools
| ツール | バージョン | 用途 |
|---|---|---|
| @playwright/test | ^1.61.1 | ビジュアルリグレッションテスト |
| @types/jest | ^30.0.0 | テスト型定義（レガシー） |

## CI/CD
| ツール | バージョン | 用途 |
|---|---|---|
| GitHub Actions | - | CI/CDパイプライン |
| actions/checkout | v4 | リポジトリチェックアウト |
| actions/setup-node | v4 | Node.js環境セットアップ |
| actions/upload-pages-artifact | v3 | ビルド成果物アップロード |
| actions/deploy-pages | v4 | GitHub Pagesデプロイ |
| actions/upload-artifact | v4 | テスト結果アップロード |
| daun/playwright-report-summary | v3 | PRへのテスト結果投稿 |

## Runtime Requirements
| 要件 | 値 |
|---|---|
| Node.js | >=18.0 |
| npm | package-lock.json v3形式 |
