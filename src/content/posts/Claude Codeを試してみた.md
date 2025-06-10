---
title: Claude Codeで初めてのVibe Codingを体験した話
published: 2025-06-08
# lang: 'ja'
tags: 
  - AI
  - Claude
description: Claude Codeを実際に試してランディングページを作成した体験談。セットアップから完成まで。
---

<abbr title="Anthropic">Anthropic</abbr>からリリースされた<mark>Claude Code</mark>を試してみた。<mark>Next.js</mark>でランディングページを作成する過程で感じたことや気づいたポイントを記録しておく。

## Claude Codeとは

Claude Codeは、<abbr title="Artificial Intelligence">AI</abbr>がコードを理解し、生成し、実際にプロジェクトを構築できるツールで、開発者の作業を大幅にサポートしてくれる<u>ターミナル型のAI開発環境</u>である。

チャットベースでの指示により、プロジェクト構築からコードの生成、ビルド実行、デバッグ、Git操作まで一連の開発作業を行うことができる。

## 作成したサイト

実際に作成したサイトはこちら。<mark>Vercel</mark>でデプロイした。

https://claude-code-landing.vercel.app/

## 環境セットアップ

### WSLのセットアップ

> [!IMPORTANT]
> Windows環境では<abbr title="Windows Subsystem for Linux">WSL</abbr>上のみのサポートとなっているため、まずWSLを準備する必要がある。

```bash
wsl --install -d Ubuntu-24.04
```

### Node.jsのインストール

権限管理とバージョン管理の観点から、nvmを使用してNode.jsをインストールした。nvmを使うメリットは以下の通りである。

> [!TIP]
> 1. **sudo不要**: ユーザー権限でNode.jsの管理が可能
> 2. **バージョン管理**: 複数のNode.jsバージョンの簡単切り替え
> 3. **セキュリティ**: 管理者権限を使わないため安全
> 4. **開発効率**: 権限エラーを気にせず開発が可能

WSL環境で以下のコマンドを実行し、<abbr title="Node Version Manager">nvm</abbr>をインストールした。

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

> [!NOTE]
> インストール後、サブスクリプションプランである<mark>Proプラン</mark>を選択してセットアップを完了した。これまでMaxプランのみだったが、Proプランでも利用できるようになっていた！

## 実際の開発体験

### プロジェクトの開始

ターミナルは<mark>Cursor</mark>上でUbuntu 24.04を立ち上げて使用した。

プロジェクトのディレクトリに移動してから`claude`コマンドを実行すると、そのディレクトリをベースとして作業が開始される。

```bash
cd path-to-dir
claude
```

Claude Codeが生成したコードや回答をCursorのコンテキストとして読み込ませることができるため、<u>非常にシームレスな開発体験</u>を得ることができた。

### 実装内容の指示

今回は以下のプロンプトでランディングページの作成を依頼した：

> Claude Codeを受講生に教えるための講座を作成したい。そのためのランディングページを作成する。利用する技術は<mark>Next.js App Router</mark>とする。ページに必要なセクションを洗い出し、自分で考えて実装してください。
>
> その際に利用する<abbr title="User Interface">UI</abbr>コンポーネントは<mark>HeroUI</mark>とする。また、<mark>TypeScript</mark>を使用してください。

### 開発プロセス

Claude Codeは以下のような流れで作業を進めた：

1. **要件分析**: ランディングページに必要なセクションの洗い出し
2. **技術選定**: Next.js App Router + HeroUI + TypeScriptの構成
3. **プロジェクト構築**: 必要なファイルとディレクトリ構造の作成
4. **実装**: 各コンポーネントの作成
5. **エラー対応**: 発生したエラーの自律的な解決

![Claude Codeによる要件分析とタスク整理の様子。プロジェクト構造の提案とセクション設計が表示されている](../../assets/claude-code-plan.png)

### エラー対応

開発中にエラーが発生した際、Claude Codeは<abbr title="autonomous - 人の手を借りずに自動的に">自律的</abbr>にエラーログを読み込み、対応策を考え、解決してくれた。

### デザインの改善

初期実装後、よりモダンなデザインへの改善を依頼した：

> よりモダンで洗練されたデザインにしてください。グラデーションやアニメーションなども充実させてください。

Claude Codeはデザインの要求に対しても適切に対応し、CSSアニメーションや視覚効果を追加した洗練されたデザインに変更してくれた。

### パッケージの移行対応

<abbr title="User Interface">UI</abbr>ライブラリについて、Claude CodeにHeroUIから<mark>NextUI</mark>への移行を依頼してみた。

問題なく適切にパッケージを移行してくれた。<u>パッケージ移行も自動的に対応できる点</u>は非常に便利だった。

## 完成までの時間とコスト

総合的な作業時間は約<mark>1〜2時間</mark>ほどで、基本的なランディングページを作成することができた。

今回はProプランのため料金はかかっていないが、仮にプランに加入していない場合のコストを確認したいと思った。

そこで、非公式の[Claude Codeの使用料金を可視化する<abbr title="Command Line Interface">CLI</abbr>ツール「ccusage」](https://zenn.dev/ryoppippi/articles/6c9a8fe6629cd6)を使用した。

![Claude Codeの使用料金画面。API使用量とコストが詳細に表示されている](../../assets/claude-code-cost.png)

---

## 今後の展開

Claude Codeを使った開発は以下の点で可能性を感じた：

> [!TIP]
> - **プロトタイプ作成の高速化**: アイデアを素早く形にできる
> - **学習ツールとしての活用**: 実装パターンを学ぶのに適している  
> - **デザインの試行錯誤**: 異なるデザインパターンを素早く試せる

## まとめと考察

今回は、Claude Codeを使って初めて<u>Vibe Coding（直感的で流れるような開発体験）</u>を試してみた。微妙な余白の調整なども的確に汲み取ってくれ、バグを伝えれば<abbr title="autonomous - 人の手を借りずに自動的に">自律的に</abbr>対応してくれる点が印象的だった。

この体験を通じて、<u>**コーディングは<abbr title="Artificial Intelligence">AI</abbr>、人間がレビュー**という開発体制</u>がすぐそこに来ていることを実感した。

Claude Codeは特にプロトタイプ作成やアイデアの具現化における<abbr title="zero to one - アイデアから初期実装まで">0→1のフェーズ</abbr>において威力を発揮するため、まずは個人開発で積極的に取り入れていきたい。

ただし注意点もある。全く知識がないコードベースやフレームワークでは、セキュリティ上の問題点などを<abbr title="identify - 発見・特定すること">指摘できない</abbr>ため、本番リリースする際には十分な検証が必要だ。

今回はあまり馴染みのないNext.jsを使用したが、内部で何が行われているのかが分からない状況は<u>精神的に不安</u>を感じた。ここで<u>基礎知識の重要性</u>を改めて実感することとなった。

結論として、<abbr title="Artificial Intelligence">AI</abbr>が生成したコードを<abbr title="integration and review - 統合と検証">統合・レビュー</abbr>する立場にある人間には、<abbr title="従来より高度な検証・評価能力">従来以上に高いレビュー力</abbr>が求められるのではないだろうか。<u>基礎知識と豊富な経験の重要性</u>は、<abbr title="Artificial Intelligence">AI</abbr>時代においても変わらないということを強く実感した。

## 参考動画

<iframe src="https://www.youtube.com/embed/6kBbbPDg12U?si=n6PxIpjnndZRMKTB" title="【Claude Code入門】初心者OK！誰でも爆速でアプリ開発ができる時代になりました" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## 参考資料

- [Claude Code 公式ドキュメント](https://docs.anthropic.com/ja/docs/claude-code/overview)
- [Claude CodeをWindows上で使う方法 - Zenn](https://zenn.dev/acntechjp/articles/eb5d6c8e71bfb9)
- [nvm - Node Version Manager](https://github.com/nvm-sh/nvm)
- [Claude Pro（$20）プランでゼロから始めるClaude Code - Zenn](https://zenn.dev/asap/articles/700168965fdb7b)
- [Claude Codeの使用料金を可視化するCLIツール「ccusage」を作った - Zenn](https://zenn.dev/ryoppippi/articles/6c9a8fe6629cd6)
