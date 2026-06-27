# 開発ガイドライン

## 1. セットアップ

```bash
# リポジトリをクローン
git clone https://github.com/melyuh/melyuh-blog.git
cd melyuh-blog

# Node.js / pnpm のバージョンをインストール
mise install

# 依存パッケージをインストール
pnpm install

# simple-git-hooks を有効化（package.json の prepare スクリプトが実行される）
pnpm prepare
```

## 2. 開発コマンド

| コマンド | 内容 |
|---|---|
| `pnpm dev` | 開発サーバーを起動 |
| `pnpm build` | 本番用静的ファイルを生成（+ Pagefindインデックス生成） |
| `pnpm preview` | ビルド結果をローカルでプレビュー |
| `pnpm lint` | Biomeでコードをチェック |
| `pnpm format` | Biomeでコードを整形 |
| `pnpm check` | TypeScript型チェック + Biome lint/format を一括実行 |

## 3. ディレクトリ構成

大枠のみ記載。詳細は実際のファイルシステムを参照すること。

```
melyuh-blog/
├── .claude/                # ドキュメント（CLAUDE.md + docs/）
├── .github/workflows/      # GitHub Actions
├── src/
│   ├── components/         # Astroコンポーネント
│   ├── content/
│   │   ├── blog/           # ブログ記事（.mdx）
│   │   └── works/          # WORKSエントリ（.md）
│   ├── layouts/            # ページレイアウト
│   ├── pages/              # ルーティング（HOME / BLOG / WORKS / PROFILE）
│   ├── styles/             # グローバルCSS
│   └── i18n/               # UIテキスト定数（多言語化対応用）
├── public/                 # 静的ファイル（favicon等）
└── infra/                  # Terraform（S3 + CloudFront）
```

## 4. コーディング規約

### 命名規則

| 対象 | 規則 | 例 |
|---|---|---|
| コンポーネントファイル | PascalCase | `BlogCard.astro` `Header.astro` |
| ページファイル | kebab-case | `index.astro` `[...slug].astro` |
| ブログ記事ファイル | `YYYY-MM-DD-title.mdx`（titleは英語のみ・URLスラッグになる） | `2026-06-26-astro-migration.mdx` |
| WORKSファイル | kebab-case | `melyuh-blog.md` |
| フロントマターフィールド | camelCase | `siteUrl` `githubUrl` |
| TypeScript変数・関数 | camelCase | `getBlogPosts()` |
| TypeScript型・インターフェース | PascalCase | `BlogPost` `WorksEntry` |

### コンポーネント設計

- 1ファイル1コンポーネント
- UIテキストは `src/i18n/` の定数ファイルから参照（コンポーネント内にベタ書きしない）

## 5. ブランチ戦略

```
main
└── feat/XXX  ← 機能ごとにブランチを切る
```

- **命名**: `feat/XXX`（例: `feat/blog-list-page`）
- **フロー**: `feat/XXX` ブランチを作成 → 実装 → PR作成 → mainにマージ → ブランチ削除
- mainへの直接pushは禁止

## 6. コミットメッセージ規約

[Conventional Commits](https://www.conventionalcommits.org/) に従う。概要は日本語で記載する。

```
<type>: <概要>
```

| type | 用途 |
|---|---|
| `feat` | 新機能の追加 |
| `fix` | バグ修正 |
| `docs` | ドキュメントのみの変更 |
| `style` | コードの意味に影響しない変更（整形等） |
| `refactor` | バグ修正でも機能追加でもないコード変更 |
| `chore` | ビルドプロセスや補助ツールの変更 |
| `content` | ブログ記事・WORKSエントリの追加・更新 |

例：
```
feat: BLOGページのカードグリッドを実装
fix: ダークモード切替後にスタイルが崩れる問題を修正
content: WSL環境構築の記事を追加
```

## 7. pre-commitフック

`simple-git-hooks` を使用する（設定ファイル不要でシンプル）。
コミット前に以下を自動実行する。エラーがある場合はコミット不可。

| チェック | 内容 |
|---|---|
| Biome lint | コードの品質チェック |
| Biome format | コードの整形チェック |
| TypeScript型チェック | 型エラーがないか確認 |

## 8. 記事の追加フロー

1. `feat/content-XXX` ブランチを作成
2. `src/content/blog/YYYY-MM-DD-title.mdx` を作成
3. フロントマターを記載（`title`・`date`・`tags` は必須）
4. 本文をMDXで執筆
5. `pnpm dev` で表示を確認
6. PRを作成してmainにマージ

## 9. WORKSエントリの追加フロー

1. `feat/works-XXX` ブランチを作成
2. `src/content/works/project-name.md` を作成
3. フロントマターを記載（`title`・`description`・`category`・`techs` は必須）
4. `pnpm dev` で表示を確認
5. PRを作成してmainにマージ

## 10. PR作成前チェックリスト

PRを作成する前に以下を確認すること。

- [ ] 変更内容に応じた `.claude/docs/` のドキュメントが更新されている
- [ ] `pnpm check` がエラーなく通る
- [ ] `pnpm build` がエラーなく通る
- [ ] `pnpm preview` で表示を目視確認した

## 11. デプロイフロー

mainブランチへのマージをトリガーにGitHub Actionsが自動実行する。手動デプロイは不要。

```
feat/XXX → PR → mainマージ → GitHub Actions自動起動 → S3アップロード → CloudFrontキャッシュ無効化
```

インフラ変更（`infra/` 配下）はTerraformを手動実行する。
