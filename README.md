<div align="center">

# サイト健康診断 — Site Health Check

**URLを入れるだけで、サイトの弱点がわかる。**

Webサイトを"患者"に見立てて、SEO・速度・セキュリティ・アクセシビリティを総合診断。
100点満点のスコアと優先度付きの**処方箋**を、その場で発行します。

[![Single HTML](https://img.shields.io/badge/single--file-HTML1-success?style=flat-square)](#)
[![No deps](https://img.shields.io/badge/dependencies-zero-blue?style=flat-square)](#)
[![Categories](https://img.shields.io/badge/categories-9-success?style=flat-square)](#)
[![Checks](https://img.shields.io/badge/checks-76+-success?style=flat-square)](#)
[![License](https://img.shields.io/badge/license-MIT-lightgrey?style=flat-square)](#license)

</div>

---

## なぜ作ったか

「自分のサイト、ちゃんと作れているのかな？」
そう思った時に開ける、**カルテのようなWebヘルスチェック**が欲しかった。

SEO専門ツールは多いものの、専門用語の壁が高く、何を直せばいいのか分かりにくい。
このツールは **非エンジニアでも自分のサイトの問題と直し方が一目でわかる** ことを最優先しました。

---

## 主な特長

### 診断の網羅性
- **9カテゴリ × 76項目** の静的HTML解析
- **採点対象7カテゴリ（100点満点）+ 参考2カテゴリ**
- SEO厳格化（構造化データ網羅率／見出し階層論理性／canonical妥当性／title整合性 等）

### 処方箋スタイルの改善アドバイス
- 最大15件の改善提案を**優先度付き**で表示（至急 / 通院 / 経過観察）
- 専門用語は **生活語に自動置換**（"meta description" → "検索結果での紹介文"）
- 番号付き処方箋レイアウト（点線罫線で診断書感を演出）

### 体験の質
- **5〜15秒**で診断完了（CORSプロキシ + DOMParser）
- **PDF保存**（`window.print()` 対応、印刷用CSS最適化済み）
- **複数URL一括診断**（最大5件、結果をタブで切替）
- **改善後の予想スコア**をワンクリックでシミュレーション
- **モバイル完全対応**（375pxから1280pxまで）
- **ライト / ダークテーマ**自動追従
- **キーボード操作**完全対応（Tab / Enter / Esc）

### 技術的な品質
- **単一HTMLファイル**（外部CSS/JS/画像なし、`SiteHealthCheck.html`をブラウザで開くだけ）
- **デザインシステム埋め込み**（OKLCHカラー、`@layer` カスケード、論理プロパティ採用）
- **アクセシビリティ AA準拠**（aria-live、コントラスト比、フォーカスリング）
- **prefers-reduced-motion 対応**
- **入力URLは保存されません**（プライバシー重視、ローカル処理のみ）

---

## クイックスタート

ダウンロードしてブラウザで開くだけ。

```sh
# 単一HTMLファイルを取得
curl -O https://raw.githubusercontent.com/<your-repo>/SiteHealthCheck/main/SiteHealthCheck.html

# ブラウザで開く（macOS）
open SiteHealthCheck.html

# Linux
xdg-open SiteHealthCheck.html

# Windows
start SiteHealthCheck.html
```

サーバ不要、ビルド不要、依存パッケージなし。
**`SiteHealthCheck.html` 1ファイルのみで完結します。**

---

## 使い方

1. ブラウザで `SiteHealthCheck.html` を開く
2. 診察したいサイトのURLを入力（例: `https://example.com`）
3. 「診断する」ボタンをクリック
4. **5〜15秒**で診断完了。総合スコア・カテゴリ別所見・処方箋が表示されます

### 複数URLを一括診断
入力画面の「複数URL（最大5件）を一括診断」をチェック → 改行区切りでURLを入力 → 結果はタブで切替

### 改善後の予想スコア
結果画面の「処方箋を実施したら？」ボタンをクリック → 全fail/warnを修正した想定でスコア再計算

### PDF保存
結果画面の「PDF保存」ボタンをクリック → ブラウザの印刷ダイアログから「PDFとして保存」

---

## 診断カテゴリ

| ID | カテゴリ | 配点 | 主な観点 |
|---|---|---:|---|
| C1 | **集客力（SEO）** | 25 | title・meta description・h1・見出し階層・canonical・構造化データ・lang・画像alt・robots |
| C2 | **体力（表示速度）** | 20 | HTMLサイズ・画像数・script数・lazy率・preconnect・WebP・width/height指定率・async/defer・DOM要素数・font-display |
| C3 | **防御力（セキュリティ）** | 20 | HTTPS・混在コンテンツ・CSP・referrer-policy・noopener充足率・SRI |
| C4 | **使いやすさ（アクセシビリティ）** | 15 | alt充足率・lang・label・見出し論理性・ランドマーク |
| C5 | **スマホでの見やすさ** | 10 | viewport・theme-color・apple-touch-icon |
| C6 | **信頼度** | 5 | 運営者情報・問い合わせ・プライバシー・公開更新日・著者・favicon・robots.txt・sitemap.xml |
| C9 | **コンテンツ品質** | 5 | 文字数・段落構造・画像/テキスト比率・平均文長・読了時間 |
| C7 | SNS共有（参考） | — | og:* / twitter:* メタタグ充足率 |
| C8 | HTML品質（参考） | — | DOCTYPE・charset・重複ID・廃止タグ・インラインJS |
| | **合計** | **100** | （+ 参考2カテゴリ） |

判定ラベル: **優秀**（90+）/ **良好**（70-89）/ **要改善**（50-69）/ **危険**（0-49）

---

## アーキテクチャ

```
┌─────────────────────────────────────────────────┐
│  SiteHealthCheck.html  (単一HTMLファイル)       │
├─────────────────────────────────────────────────┤
│                                                 │
│   ┌──────────────────────────────────────────┐  │
│   │ <style>                                  │  │
│   │   ar Design System (OKLCH / 6 accents)   │  │
│   │   App-specific styles (token-first)      │  │
│   │ </style>                                 │  │
│   └──────────────────────────────────────────┘  │
│                                                 │
│   ┌──────────────────────────────────────────┐  │
│   │ <body class="ar-root">                   │  │
│   │   #screen-input | #screen-scanning |     │  │
│   │   #screen-result | #screen-error         │  │
│   │ </body>                                  │  │
│   └──────────────────────────────────────────┘  │
│                                                 │
│   ┌──────────────────────────────────────────┐  │
│   │ <script>                                 │  │
│   │   ┌────────────────────────────────┐     │  │
│   │   │ fetchPage (CORSプロキシ3段)     │     │  │
│   │   │  ├ codetabs                    │     │  │
│   │   │  ├ allorigins                  │     │  │
│   │   │  └ thingproxy                  │     │  │
│   │   │ Promise.any でフェイルオーバー  │     │  │
│   │   └────────────────────────────────┘     │  │
│   │   ┌────────────────────────────────┐     │  │
│   │   │ DOMParser → 静的解析            │     │  │
│   │   │  ├ checkSEO (14項目)            │     │  │
│   │   │  ├ checkPerformance (12項目)    │     │  │
│   │   │  ├ checkSecurity (7項目)        │     │  │
│   │   │  ├ checkA11y (6項目)            │     │  │
│   │   │  ├ checkMobile (7項目)          │     │  │
│   │   │  ├ checkTrust (8項目)           │     │  │
│   │   │  ├ checkContent (5項目)         │     │  │
│   │   │  ├ checkSNS (11項目)            │     │  │
│   │   │  └ checkHTML (6項目)            │     │  │
│   │   └────────────────────────────────┘     │  │
│   │   ┌────────────────────────────────┐     │  │
│   │   │ calcScore → renderResult        │     │  │
│   │   │ 用語言い換え (TERM_MAP)          │     │  │
│   │   │ 状態遷移 (state machine)        │     │  │
│   │   └────────────────────────────────┘     │  │
│   │ </script>                                │  │
│   └──────────────────────────────────────────┘  │
│                                                 │
└─────────────────────────────────────────────────┘
```

### CORSプロキシ戦略
ブラウザ同一オリジン制約により、任意URLへの直接 `fetch` は拒否される。
3つの公開CORSプロキシを `Promise.any` で並列起動 → 最も早い成功を採用 → 全失敗時のみエラー。

```js
return Promise.any([
  fetch(`https://api.codetabs.com/v1/proxy?quest=${encoded}`),
  fetch(`https://api.allorigins.win/get?url=${encoded}`),
  fetch(`https://thingproxy.freeboard.io/fetch/${encoded}`),
]);
```

`/robots.txt` と `/sitemap.xml` の存在チェックも同じパターンで並列取得。

### スコア計算
```
カテゴリスコア = (pass×100 + warn×50) / (採点対象項目数) × 配点
総合スコア = 採点7カテゴリのスコア合計（端数四捨五入）
```

`info` / `na` は採点対象外（HTML静的解析で判定不能な項目に使用）。

---

## デザインシステム

UIは **ar Design System** を採用。
LocalCSV（HTML1ファイルCSVエディタ）から逆算した汎用デザインシステムで、`--ar-*` / `.ar-*` プレフィックスで他CSSと衝突しない設計。

主な原則:
- **Token first**: すべての色・余白・角丸・影は `var(--ar-*)` トークン経由
- **OKLCHカラー**: 知覚的に均一な色空間
- **論理プロパティ**: `inline-size` / `block-size` / `padding-inline` / `inset-block-start`
- **6アクセント切替可**: wakakusa（緑、デフォルト）/ ruri / beni / yamabuki / sumire / asagi
- **ライト・ダーク両対応**: `[data-theme]` 属性 or OS追従
- **影は装飾しない**: 階層を表すためだけに使用、色付き禁止
- **コンパクト密度**: 余白は `--ar-space-4`(8px) と `--ar-space-5`(12px) を中心
- **Material Symbols Outlined** 一貫採用（絵文字なし）

---

## 制限事項

静的HTML解析の限界として、以下は **取得できません**:

- 実測パフォーマンス指標（LCP / CLS / FCP / TBT）
- 検索順位・被リンク数
- HTTPS証明書の発行者・有効期限
- レンダリング後のJS実行結果
- 内部リンクの実際のリンク切れ
- 競合との比較

これらが必要な場合は、Google PageSpeed Insights API、Search Console API、有料SEOツール（Ahrefs / SEMrush）等との併用をご検討ください。

---

## ロードマップ

将来的な拡張候補（実装は要相談）:

- [ ] **PageSpeed Insights APIをオプション併用**（APIキー設定時のみLighthouseスコア取得）
- [ ] **HTTPS証明書検査**（SSL Labs API）
- [ ] **競合ベンチマーク**（業界平均との対比）
- [ ] **履歴保存**（localStorage で過去診断を時系列推移グラフ化）
- [ ] **モバイル/デスクトップ別診断**（User-Agent切替）
- [ ] **i18n対応**（英語UI切替）

---

## プライバシー

- 入力されたURLは **localStorageに保存されません**
- 診断はブラウザ内で完結（CORSプロキシ経由でのHTML取得を除く）
- アクセス解析・トラッキングなし
- Cookieなし

---

## 技術スタック

- **HTML5** / **Vanilla JavaScript (ES2020)** / **CSS3**
- **OKLCH カラースペース** + `light-dark()` 関数
- **CSS Cascade Layers** (`@layer`)
- **CSS Logical Properties**
- **Intl.DateTimeFormat** for 日付フォーマット
- **AbortController** for キャンセル対応
- **Material Symbols Outlined** (Google Fonts CDN)
- **Promise.any** for CORS プロキシフェイルオーバー

外部依存: Material Symbols Outlined フォント（CDN）のみ。それ以外は完全に self-contained。

---

## ブラウザ対応

| ブラウザ | 動作 |
|---|---|
| Chrome / Edge | 最新2バージョン ✓ |
| Safari | 最新2バージョン ✓ |
| Firefox | 最新2バージョン ✓ |
| モバイル Safari / Chrome | iOS 16+ / Android 10+ ✓ |
| Internet Explorer | ✗（ESM・OKLCH 等を使用） |

---

## License

MIT License — 自由に利用・改変・配布できます。

---

## Acknowledgments

- **ar Design System** — LocalCSVから派生した汎用デザインシステム
- **CORSプロキシ** — codetabs.com / allorigins.win / thingproxy.freeboard.io（公開プロキシサービス）
- **Material Symbols Outlined** — Google Fonts のアイコンフォント
- 診断ロジックの一部は **SEOチェッカー by studio corto** の静的解析パターンを参考にしました

---

<div align="center">

**Made with care for healthy websites.**

</div>
