# feat/base-layout タスクリスト

## 作業概要

共通レイアウト（Header・Footer・BaseLayout）とUIテキスト定数（i18n）を実装する。

## タスク

- [x] `src/i18n/ui.ts` 作成
- [x] `src/layouts/BaseLayout.astro` 作成
- [x] `src/components/Header.astro` 作成（ナビ・テーマ切替）
- [x] `src/components/Footer.astro` 作成
- [x] `src/pages/index.astro` を BaseLayout 使用に更新
- [x] FOUC修正（`BaseLayout.astro` の `<head>` にインラインスクリプト追加）
- [x] `Footer.astro` の外部リンクを `rel="noopener noreferrer"` に変更
- [ ] 上記修正をコミットしてPRマージ

## 完了条件

- `pnpm check` がエラーなく通る
- `pnpm build` がエラーなく通る
- ダークモード切替がちらつきなく動作する
