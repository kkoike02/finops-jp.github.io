# Dependencies

## Vulnerability Summary (npm audit 実行結果)

**Total: 26 vulnerabilities**
- Critical: 0
- High: 5
- Moderate: 21
- Low: 0

## High Vulnerabilities

| # | パッケージ | バージョン | 脆弱性 | Advisory | 依存チェーン |
|---|---|---|---|---|---|
| 1 | fast-uri | 3.0.0 - 3.1.3 | ホスト混乱（リテラルバックスラッシュによるauthorityデリミタ偽装） | GHSA-v2hh-gcrm-f6hx | 直接依存（fix available via npm audit fix） |
| 2 | serialize-javascript | <=7.0.4 | RCE（RegExp.flags、Date.prototype.toISOString()経由） | GHSA-5c6j-r48x-rmvq | @docusaurus/core → @docusaurus/bundler → copy-webpack-plugin → serialize-javascript |
| 3 | serialize-javascript | <=7.0.4 | CPU枯渇DoS（crafted array-like objects） | GHSA-qj8w-gfj5-8c6v | @docusaurus/core → @docusaurus/bundler → css-minimizer-webpack-plugin → serialize-javascript |
| 4 | sharp | <0.35.0 | libvips継承脆弱性: CVE-2026-33327, CVE-2026-33328, CVE-2026-35590, CVE-2026-35591 | GHSA-f88m-g3jw-g9cj | @docusaurus/plugin-ideal-image → @docusaurus/lqip-loader → sharp |
| 5 | uuid | <11.1.1 | buf提供時のバッファ境界チェック欠如 | GHSA-w5hq-g745-h8pq | webpack-dev-server → sockjs → uuid |

## Moderate Vulnerabilities

| # | パッケージ | 脆弱性概要 | 依存チェーン |
|---|---|---|---|
| 1-21 | 複数（serialize-javascript間接依存による伝播） | Docusaurusの各プラグインが@docusaurus/coreに依存し、coreがserialize-javascript脆弱性を持つbundlerに依存 | @docusaurus/preset-classic → 各プラグイン → @docusaurus/core → @docusaurus/bundler |

### Moderate影響パッケージ一覧
以下のDocusaurusプラグインが間接的にserialize-javascript脆弱性の影響を受ける：
- @docusaurus/plugin-client-redirects
- @docusaurus/plugin-content-blog
- @docusaurus/plugin-content-docs
- @docusaurus/plugin-content-pages
- @docusaurus/plugin-css-cascade-layers
- @docusaurus/plugin-debug
- @docusaurus/plugin-google-analytics
- @docusaurus/plugin-google-gtag
- @docusaurus/plugin-google-tag-manager
- @docusaurus/plugin-ideal-image
- @docusaurus/plugin-sitemap
- @docusaurus/plugin-svgr
- @docusaurus/preset-classic
- @docusaurus/theme-classic
- @docusaurus/theme-search-algolia
- @docusaurus/lqip-loader
- copy-webpack-plugin
- css-minimizer-webpack-plugin
- sockjs
- webpack-dev-server

## Dependency Tree（脆弱性の伝播）

```
@docusaurus/core (^3.5.2)
├── @docusaurus/bundler
│   ├── copy-webpack-plugin → serialize-javascript (HIGH: RCE, DoS)
│   └── css-minimizer-webpack-plugin → serialize-javascript (HIGH: RCE, DoS)
├── webpack-dev-server → sockjs → uuid (MODERATE: buffer bounds)
└── fast-uri (HIGH: host confusion) [fix available]

@docusaurus/plugin-ideal-image
└── @docusaurus/lqip-loader → sharp (HIGH: libvips CVEs)
```

## Fix Strategy

| アクション | 対象 | リスク |
|---|---|---|
| `npm audit fix` | fast-uri | 低リスク — 非破壊的修正が可能 |
| No fix available | serialize-javascript | Docusaurus上流の対応待ち |
| No fix available | sharp | @docusaurus/plugin-ideal-imageの上流対応待ち |
| No fix available | uuid | webpack-dev-serverの上流対応待ち（dev依存） |

## 前回（backup-run1）からの改善点
- **Critical脆弱性**: 1件 → 0件（解消済み）
- **High脆弱性**: 12件 → 5件（改善）
- **総脆弱性数**: 54件 → 26件（半減）
- **主な改善**: shell-quote, lodash, minimatch, node-forge, ws, webpack等の脆弱性が解消
