# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## プロジェクト概要

[astro-theme-retypeset](https://github.com/radishzzz/astro-theme-retypeset) をベースにした個人ブログ「uejo.dev」。主に日本語で執筆し、英語もサポート。

## コマンド

```bash
pnpm dev          # 型チェック + 開発サーバー起動
pnpm build        # 型チェック + ビルド + 圧縮 + LQIP生成
pnpm preview      # 本番ビルドのプレビュー
pnpm lint         # ESLint 実行
pnpm lint:fix     # ESLint 自動修正
pnpm new-post     # 新規ブログ記事のスキャフォールド
pnpm apply-lqip   # 低品質画像プレースホルダー（LQIP）生成
pnpm format-posts # 既存記事の一括フォーマット
```

コミット前にlint-staged（ESLint）が自動実行される。

## アーキテクチャ

**`src/config.ts`** — サイト全体の設定ファイル。サイトメタデータ・ロケール・カラーテーマ・コメントシステム・アナリティクス・フッターなどを管理。サイト全体の変更はここを編集する。

**`src/content.config.ts`** — コンテンツコレクションのスキーマ定義。記事には `title`（文字列）と `published`（日付）が必須。

**`src/content/posts/`** — Markdown/MDX形式のブログ記事。フロントマターのフィールド：
```yaml
title: string          # 必須
published: date        # 必須
description: string
updated: date
tags: string[]
draft: boolean         # デフォルト: false
pin: number            # 0〜99、デフォルト: 0
toc: boolean
lang: locale           # 例: "en", "ja"
abbrlink: string       # カスタムスラッグ
```

**`src/i18n/`** — 11言語（de, en, es, fr, ja, ko, pl, pt, ru, zh, zh-tw）の翻訳文字列。デフォルトロケールは `ja`。

**`src/plugins/`** — Markdown処理用のカスタム remark/rehype プラグイン（数式・ディレクティブ・アドモニション・GitHubカード）。

**`src/pages/`** — Astroのファイルベースルーティング。RSSフィード・OG画像生成・タグページ・Aboutページを含む。

**`uno.config.ts`** — UnoCSS設定。OKLCHカラーパレット・CJKタイポグラフィ・カスタムフォントファミリーを定義。

## 記事の記法

記事を作成・編集する際は `/proofread` コマンドを使用すること。ルールの実体は `.claude/rules/blog-proofreading-rule.md` で管理している。
