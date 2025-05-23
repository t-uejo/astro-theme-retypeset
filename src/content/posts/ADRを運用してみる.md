---
title: ADRを運用するので具体例とテンプレを作成した話
published: 2025-04-28
# lang: 'ja'
tags: 
  - ADR
description: ADRとは、Architectural Decision Recordsの略で、設計の意図や背景を記録するためのもの。その目的とテンプレについて。
---

ADRとは、Architectural Decision Recordsの略で、設計の意図や背景を記録するためのもの。今回導入する目的や参考にした記事をここに記録しておく。

## 導入目的

以下を目的に導入した。1と2はソフトウェアデザインより引用。3についてはRAGやMCP連携する想定で書いている。

1. アーキテクチャ選択の背景を開発メンバー全員が認識する必要がある。
2. 保守やその後の追加開発で、アーキテクチャの見直しや、スペックの拡大、制限緩和、制限撤廃など仕様の見直しが発生した場合の履歴を残しておきたい。
3. ドキュメントをAIにコンテキストとして読み込ませることで、IaCやマニフェストファイル生成などのアウトプット品質を高めたい。

## テンプレート

一旦、以下のようなテンプレートとした。不採用案についても記載するようにしている。

```
# ADR-XXX: [タイトル]

## ステータス
提案中

## 背景
この決定が必要になった背景や状況を説明します。

## 決定内容と理由
![ここにアーキテクチャ図を入れる]()

1. 採用するアーキテクチャの決定内容を説明します
    - 決定した背景や理由を記載します

## 影響
- 各決定が及ぼす影響を説明します

## 比較・検討内容

1. 採用したアーキテクチャの採用案と不採用案を並べ、理由を記載します。

## 参照
- [関連するADRの参照リンク](./example.md)
- [参考記事リンク]()
- [公式ドキュメントリンク]()
```

## 今後の展開

- IaCのバイブコーディング（簡単に言うと、自然言語でコーディングする）を実現する際に利用する。
- ADR作成自体もAIを使って自然言語で行えるようにしたい。

## 作成したテンプレや具体例など

ADRのテンプレ、具体例、README（運用マニュアル的な内容を記載）を作成したので共有しておく。ADRの具体例はAIに作成してもらった。

- [adr-example](https://github.com/t-uejo/adr-example)

## AIを使う上での注意点

AIに読み込ませるため、以下の点には注意しておきたい。

- 利用する生成AIでは、データを学習に使用しない設定を有効にしておくこと。
- 業務仕様や固有名詞をインプットとして与える場合は事前にコンセンサスを取ること。

## 参考
- [ソフトウェアデザイン 2024年10月号](https://amzn.asia/d/e4dAiPl)
- [ADR-Toolsを使ってADR（Architecture Decision Record）を作る](https://okuzawats.com/blog/adr/)