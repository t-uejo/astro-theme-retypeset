---
title: Claude Codeでランディングページを作成してみた
published: 2025-06-08
# lang: 'ja'
tags: 
  - AI
  - Claude
description: Claude Codeを実際に試してランディングページを作成した体験談。セットアップから完成まで。
---

AnthropicからリリースされたClaude Codeを試してみた。Next.jsでランディングページを作成する過程で感じたことや気づいたポイントを記録しておく。

## Claude Codeとは

Claude Codeは、AIがコードを理解し、生成し、実際にプロジェクトを構築できるツールで、開発者の作業を大幅にサポートしてくれるターミナル型のAI。チャットベースでの指示により、コードの生成から実行、デバッグ、Git操作まで一連の開発作業を行うことができる。

## 環境セットアップ

### WSLのセットアップ

Windows環境ではWSL上のみのサポートのため、まずWSLを準備した。

```bash
wsl --install -d Ubuntu-24.04
```

### Node.jsのインストール

権限管理とバージョン管理の観点から、nvmを使用してNode.jsをインストールした。nvmを使うメリットは以下の通り：

1. **sudo不要**: ユーザー権限でNode.js管理
2. **バージョン管理**: 複数のNode.jsバージョンを簡単切り替え
3. **セキュリティ**: 管理者権限を使わないため安全
4. **開発効率**: 権限エラーを気にせず開発可能

```bash
# nvmのインストール
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash

# Node.jsのインストール
nvm install --lts
nvm use node
# -> Now using node v22.16.0 (npm v10.9.2)
```

### Claude Codeのインストール

```bash
npm install -g @anthropic-ai/claude-code
claude --version
```

インストール後、サブスクプランであるProプランを選択してセットアップを完了した。（これまでMaxプランのみだったが、Proプランでも利用できるようになっていた！）

## 実際の開発体験

### プロジェクトの開始

Claude Codeのセカンダリサイドバーでチャットとターミナルを切り替えながら作業を進めることができる。プロジェクトのディレクトリに移動してからclaudeコマンドを実行すると、そのディレクトリをベースに作業が開始される。

```
cd path-to-dir
claude
```

### 実装内容の指示

今回は以下のプロンプトでランディングページの作成を依頼した：

```
今からClaude Codeを受講生に教えるための講座を作成したい。そのためにランディングページを作成する。利用する技術はNext.js AppRouterにする。ページに必要なセクションを洗い出し、自分で考えて実装してください。

その際に利用するUIコンポーネントをHeroUIとして。また、TypeScriptを使用して。
```

### 開発プロセス

Claude Codeは以下のような流れで作業を進めた：

1. **要件分析**: ランディングページに必要なセクションの洗い出し
2. **技術選定**: Next.js App Router + HeroUI + TypeScriptの構成
3. **プロジェクト構築**: 必要なファイルとディレクトリ構造の作成
4. **実装**: 各コンポーネントの作成
5. **エラー対応**: 発生したエラーの自律的な解決

![](../../assets/claude-code-plan.png)
要件分析をして、タスクを整理してくれた。

### エラー対応での気づき

開発中にエラーが発生した際、Claude Codeは自律的にエラーログを読み込み、対応策を実行してくれた。ただし、以下の点で課題を感じた：

- **基礎知識の重要性**: エラーの原因や対処法を理解していないと、精神的な不安がある
- **時間のかかるケース**: 複雑なエラーに対しては従来の手動対応より時間がかかることもある

### デザインの改善

初期実装後、よりモダンなデザインへの改善を依頼：

```
よりもっとモダンで洗練されたデザインにしてください。グラデーションやアニメーションなども充実させてください。
```

Claude Codeはデザインの要求に対しても適切に対応し、視覚効果やアニメーションを追加した洗練されたデザインに変更してくれた。

### パッケージの移行対応

開発中にNextUIからHeroUIへの移行警告が表示された際も、Claude Codeに依頼することで適切にパッケージを移行してくれた。パッケージへの移行も自動的に対応できる点は非常に便利だった。

## 完成までの時間とコスト

総合的な作業時間は約1~2時間ほどで、基本的なランディングページを作成することができた。

そもそもProプランのため、料金はかかっていないが、仮にプランに加入していない場合のコストを確認したい。

そこで、非公式の[Claude Codeの使用料金を可視化するCLIツール「ccusage」](https://zenn.dev/ryoppippi/articles/6c9a8fe6629cd6)を使用した。

![](../../assets/claude-code-cost.png)


## 今後の展開

Claude Codeを使った開発は以下の点で可能性を感じた：

- **プロトタイプ作成の高速化**: アイデアを素早く形にできる
- **学習ツールとしての活用**: 実装パターンを学ぶのに適している  
- **デザインの試行錯誤**: 異なるデザインパターンを素早く試せる

## まとめ

Claude Codeは開発作業を大幅に効率化できるツールだが、基礎的な知識があることでより安心して使用できると感じた。

特にプロトタイプ作成やアイデアの具現化における0→1において威力を発揮するため、今後の開発作業に積極的に取り入れていきたい。

注意点として、安心できるというのは、あくまでコードには一つも手を加えずに作成できたという点で述べており、全く知識がないコードベースでは、セキュリティ的な問題点などを指摘できないため注意が必要だと思う。


## 参考資料

- [【Claude Code入門】初心者OK！誰でも爆速でアプリ開発ができる時代になりました - Youtube](https://youtu.be/6kBbbPDg12U?si=n6PxIpjnndZRMKTB)
- [Claude Code 公式ドキュメント](https://docs.anthropic.com/ja/docs/claude-code/overview)
- [Claude CodeをWindows上で使う方法 - Zenn](https://zenn.dev/acntechjp/articles/eb5d6c8e71bfb9)
- [nvm - Node Version Manager](https://github.com/nvm-sh/nvm)
- [Claude Pro（$20）プランでゼロから始めるClaude Code - Zenn](https://zenn.dev/asap/articles/700168965fdb7b)
- [Claude Codeの使用料金を可視化するCLIツール「ccusage」を作った - Zenn](https://zenn.dev/ryoppippi/articles/6c9a8fe6629cd6)
