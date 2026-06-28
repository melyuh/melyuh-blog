# 実装進捗

> **更新ルール**: セッション開始時にClaude が `git log main --oneline` を確認し、マージ済みの内容をこのファイルに反映してから実装を開始すること。

## 最終更新

2026-06-28

## 凡例

- ✅ 完了（mainにマージ済み）
- 🔧 実装中・レビュー待ち（ブランチ名を備考に記載）
- ⬜ 未着手

---

## 現在のブランチ・PR状況

| ブランチ | 状態 | 内容 |
|---|---|---|
| `feat/base-layout` | ✅ マージ済み | BaseLayout・Header・Footer・i18n実装 |
| `main`（直接作業中） | 🔧 未コミット | スタイル調整（アイコン・フォント・背景色・テーブル） |

## 次に着手する作業

1. スタイル調整をコミット・整理（できれば `feat/styling` ブランチへ）
2. コンテンツ管理（`src/content/config.ts`・サンプル記事）
3. BLOGページ実装
4. Mermaid対応（記事実装時に `rehype-mermaid` で対応）

---

## セットアップ

| 項目 | 状態 | 備考 |
|---|---|---|
| Astroプロジェクト初期化 | ✅ | TailwindCSS v4・MDX込み |
| mise / pnpm 設定 | ✅ | `.mise.toml` |
| Biome v2 | ✅ | `biome.json` |
| simple-git-hooks（pre-commit） | ✅ | `pnpm prepare` で有効化 |
| @astrojs/check + typescript | ✅ | `pnpm check` 用 |

---

## フロントエンド

### 共通

| 項目 | 状態 | ブランチ / PR | 備考 |
|---|---|---|---|
| `src/i18n/ui.ts`（UIテキスト定数） | ✅ | — | |
| `BaseLayout.astro` | 🔧 | main未コミット | Google Fonts・ファビコン追加 |
| `Header.astro`（ナビ・テーマ切替） | 🔧 | main未コミット | ロゴ画像切替（ライト/ダーク）追加 |
| `Footer.astro` | ✅ | — | |

### ページ

| ページ | 状態 | 備考 |
|---|---|---|
| HOME | ⬜ | ヒーロー・最新記事3件・注目WORKS・SNSリンク |
| BLOG（記事一覧） | ⬜ | カードグリッド・タグフィルター |
| 記事詳細 | ⬜ | TOC・関連記事・MDXレンダリング |
| WORKS | ⬜ | カードグリッド |
| PROFILE | ⬜ | 自己紹介・スキル・職歴 |

### コンテンツ管理

| 項目 | 状態 | 備考 |
|---|---|---|
| `src/content/config.ts` | ⬜ | blog・worksのスキーマ定義 |
| ブログ記事サンプル | ⬜ | 動作確認用 |
| WORKSエントリサンプル | ⬜ | 動作確認用 |

### 機能

| 機能 | 状態 | 備考 |
|---|---|---|
| OGP メタタグ | ⬜ | LinkedInシェア対応 |
| RSSフィード | ⬜ | `/rss.xml` |
| Pagefind 検索 | ⬜ | ビルド時インデックス生成 |
| ダーク/ライトモード | ✅ | |

---

## インフラ・CI/CD

| 項目 | 状態 | 備考 |
|---|---|---|
| Terraform（S3 + CloudFront） | ⬜ | `infra/` 配下 |
| GitHub Actions（build + deploy） | ⬜ | `.github/workflows/` |
| OIDC認証（GitHub → AWS） | ⬜ | IAMロール設定が必要 |

---

## 既知の課題・技術的負債

| 課題 | 該当箇所 | 優先度 |
|---|---|---|
| mainに直接コミットしているスタイル変更がある | `src/` 全体 | 低（個人ブログのため許容範囲） |
| Mermaid未対応 | 記事MDX | 低（コンテンツ実装時に対応） |
