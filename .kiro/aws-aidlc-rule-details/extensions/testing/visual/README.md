# Visual Regression Testing Extension — 設定ファイル構成

## 概要

Visual Regression Testing Extensionは、以下の設定ファイル群で構成されています。
AI-DLCワークフロー内でオプトインされると、各ステージでビジュアル差分検出が強制適用されます。

---

## 設定ファイル一覧

### AI-DLC Extension（Kiro側の仕組み）

| ファイル | パス | 役割 |
|---|---|---|
| **opt-in質問** | `.kiro/aws-aidlc-rule-details/extensions/testing/visual/visual-regression.opt-in.md` | ワークフロー開始時にKiroが自動スキャンし、Requirements Analysisで「有効にしますか？」と質問するためのテンプレート |
| **ルール本体** | `.kiro/aws-aidlc-rule-details/extensions/testing/visual/visual-regression.md` | ユーザーが「Yes」と回答した後にKiroが読み込む4つのルール（VISUAL-01〜04）。各ステージで強制適用される |
| **steeringルール** | `.kiro/steering/project-rules.md` | Build and Testステージで残存脆弱性を全件リスト化する必須ルール（Visual Regression直接ではないが関連） |

### Playwright設定（テスト実行基盤）

| ファイル | パス | 役割 |
|---|---|---|
| **Playwright設定** | `playwright.config.ts` | テストディレクトリ（`./tests/visual`）、スナップショット保存先（`./tests/visual/snapshots`）、webServer自動起動（`npm run serve`, port 3000）、ブラウザ（chromium）を定義 |
| **テストスクリプト** | `tests/visual/visual-regression.spec.ts` | 5つのテストケース（トップ、ドキュメント、フレームワーク、ブログ、ナビゲーション）。各ページのスクリーンショットを撮影しベースラインと比較 |
| **ベースライン画像** | `tests/visual/snapshots/visual-regression.spec.ts-snapshots/*.png` | 比較基準となるスクリーンショット画像（5枚）。`npm run test:visual:update`で更新 |

### npmスクリプト（package.json）

| スクリプト名 | コマンド | 用途 |
|---|---|---|
| `test:visual` | `npx playwright test` | ベースラインとの比較テスト実行 |
| `test:visual:update` | `npx playwright test --update-snapshots` | ベースラインスクリーンショットの更新 |

### GitHub Actions（CI/CD）

| ファイル | パス | 役割 |
|---|---|---|
| **ワークフロー** | `.github/workflows/visual-test.yaml` | PR作成時に自動実行。ビルド→テスト→結果をPRコメントに投稿→diff画像をArtifactとしてアップロード |

### .gitignore

| 追記内容 | 目的 |
|---|---|
| `/test-results/` | テスト実行時の一時ファイル（diff画像等）を除外 |
| `/playwright-report/` | HTMLレポートを除外 |

---

## ファイル間の関係

```
Kiro起動
  │
  ├─ .kiro/aws-aidlc-rule-details/extensions/testing/visual/
  │    ├─ visual-regression.opt-in.md  ← Kiroが自動スキャン
  │    └─ visual-regression.md         ← Yes回答時に読み込み
  │
  ├─ playwright.config.ts             ← テスト実行時の設定
  │    └─ webServer: npm run serve    ← ローカルサーバー自動起動
  │
  ├─ tests/visual/
  │    ├─ visual-regression.spec.ts   ← テストケース定義
  │    └─ snapshots/                  ← ベースライン画像保存先
  │
  ├─ .github/workflows/visual-test.yaml ← PR時に自動実行
  │    ├─ npm run build
  │    ├─ npx playwright test
  │    ├─ Artifact upload (diff画像)
  │    └─ PR comment (結果サマリー)
  │
  └─ package.json
       ├─ devDependencies: @playwright/test
       └─ scripts: test:visual, test:visual:update
```

---

## 各ルール（VISUAL-01〜04）と対応する設定ファイル

| ルール | 内容 | 対応する設定 |
|---|---|---|
| VISUAL-01 | Playwright設定必須 | `playwright.config.ts`、`package.json`のdevDependenciesとscripts |
| VISUAL-02 | 変更前ベースライン撮影 | `npm run test:visual:update` → `tests/visual/snapshots/`に保存 |
| VISUAL-03 | 変更後比較テスト | `npm run test:visual` → 差分検出時に`test-results/`にdiff画像生成 |
| VISUAL-04 | 主要ページカバレッジ | `tests/visual/visual-regression.spec.ts`で5ページ定義 |
