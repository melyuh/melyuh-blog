# CLAUDE.md

## プロジェクト概要

**melyuh-blog** はAstroで構築する個人技術ブログ兼ポートフォリオサイト。
「書類選考を突破するための技術的証拠」として機能させることを主目的とする。
AWS S3 + CloudFrontで静的配信し、Terraformでインフラを管理する。

## ドキュメント

**セッション開始時や実装を始める前** に以下を必ず読むこと。

1. [要件定義](.claude/docs/01-requirements.md) — 何を作るか・なぜ作るか
2. [アーキテクチャ設計](.claude/docs/02-architecture.md) — 技術スタック・デプロイ構成
3. [機能設計](.claude/docs/03-features.md) — 各ページの詳細仕様
4. [開発ガイドライン](.claude/docs/04-dev.md) — 規約・コマンド・フロー

## クイックスタート

```bash
mise install   # Node.js / pnpm のバージョンをインストール
pnpm install   # 依存パッケージをインストール
pnpm dev       # 開発サーバーを起動
```

## ドキュメント更新ルール

機能変更・アーキテクチャ変更・開発フロー変更を行った際は、実装と同時に対応するドキュメントを必ず更新すること。

| 変更の種類 | 更新対象 |
|---|---|
| 要件・目標・ページ構成の変更 | 01-requirements.md |
| 技術スタック・デプロイ構成の変更 | 02-architecture.md |
| 機能仕様・フロントマターの変更 | 03-features.md |
| コマンド・規約・フローの変更 | 04-dev.md |
| 制約・セッションルール・クイックスタートの変更 | CLAUDE.md |

## 主要な制約

- mainへの直接pushは禁止。必ず `feat/XXX` ブランチ → PR → マージのフローを守る
- UIテキストは `src/i18n/` から参照。コンポーネント内にベタ書きしない
- `infra/` 配下の `*.tfvars` と `*.tfstate` は `.gitignore`（機密情報のため）
- デプロイはGitHub Actionsが自動実行。手動デプロイは不要
