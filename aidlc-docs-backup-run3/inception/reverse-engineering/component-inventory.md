# Component Inventory

## Application Packages
| パッケージ | 種別 | 説明 |
|---|---|---|
| f2jc-website (v2.0.0) | npm | Docusaurus静的サイト（メインアプリケーション） |

## Source Components (src/)
| コンポーネント | パス | 説明 |
|---|---|---|
| HomepageFeatures | src/components/HomepageFeatures/ | トップページの特徴セクション |
| Index Page | src/pages/index.tsx | トップページ |
| Slides Page | src/pages/slides.tsx | スライド資料一覧ページ |
| Press Page | src/pages/press.md | メディア記事一覧ページ |
| Utilities | src/utils/ | カラー、Prismテーマ、JSユーティリティ |
| Data | src/data/ | イベント、特徴、スライドデータ |
| Custom CSS | src/css/custom.css | カスタムスタイル |

## Content Components (docs/)
| セクション | パス | 説明 |
|---|---|---|
| Introduction | docs/introduction/ | FinOps入門（what-is-finops.md） |
| Framework | docs/framework/ | フレームワーク全体（原則、ペルソナ、フェーズ、成熟度、ドメイン、スコープ） |
| Capabilities | docs/framework/capabilities/ | FinOpsケイパビリティ詳細 |
| Domains | docs/framework/domains/ | FinOpsドメイン詳細 |
| Personas | docs/framework/personas/ | ペルソナ定義 |
| Assets | docs/assets/ | 用語集、画像 |
| About | docs/about/ | サイト概要 |

## Blog Components (blog/)
| 記事 | 日付 | 説明 |
|---|---|---|
| japan-finops-meetup-1 | 2023-11-22 | 第1回Japan FinOps Meetup |
| japan-finops-meetup-2 | 2024-07-30 | 第2回Japan FinOps Meetup |
| japan-finops-meetup-3 | 2024-11-15 | 第3回Japan FinOps Meetup |

## Infrastructure Components (.github/workflows/)
| ワークフロー | ファイル | 説明 |
|---|---|---|
| GitHub Pages Deploy | gh-pages.yaml | main pushでビルド＆デプロイ |
| Visual Regression Test | visual-test.yaml | PR時のビジュアルリグレッションテスト |
| Auto Translate | auto-translate.yaml | 翻訳自動化 |
| Check Translation Status | check-translation-status.yaml | 翻訳ステータスチェック |
| Check Updates | check-updates.yaml | 更新チェック |

## Shared/Automation Scripts (scripts/)
| スクリプト | 言語 | 説明 |
|---|---|---|
| ai-translator.py | Python | AI翻訳スクリプト |
| translation-tracker.py | Python | 翻訳追跡スクリプト |
| update-detector.py | Python | 更新検出スクリプト |
| glossary.json | JSON | 翻訳用語集 |

## Test Components (tests/)
| テスト | パス | 説明 |
|---|---|---|
| Visual Regression | tests/visual/visual-regression.spec.ts | Playwright ビジュアルスナップショットテスト |
| Unit Test (legacy) | src/utils/__tests__/jsUtils.test.ts | JSユーティリティテスト（型定義のみ） |

## Total Count Summary
| カテゴリ | 件数 |
|---|---|
| Application (npm) | 1 |
| Source Components | 7 |
| Content Sections | 7 |
| Blog Posts | 3 |
| Infrastructure (Workflows) | 5 |
| Automation Scripts | 3 |
| Test Suites | 2 |
