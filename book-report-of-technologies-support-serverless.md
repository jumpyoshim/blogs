# 概要

- 著作： **「サーバーレスを支える技術」**
- 著者： **Aki @nekoruri**
- 著者経歴：秋葉原生まれ大手町育ちの歌って踊れる江戸っ子フルスタックインフラエンジニア/クラウド/セキュリティ/技術系同人誌/SFC 徳田村井研/WIDE/アニメ/声優/宇宙/ニコ厨/ステマ/ねこ大好き

# 目的

サーバレスアーキテクチャを知る

# 要約

サーバーレスアーキテクチャは FaaS や BaaS を組み込んだアプリケーション設計である。これは費用対効果が高く、高速なスケールも可能である。特にイベントドリブンなシステムアーキテクチャの構築に向く。FaaS や BaaS は AWS, GCP, Azure, IBM Cloud などのパブリッククラウドによって提供されている。

# 感想

サーバーレスアーキテクチャのメリットとして主張されている、運用コスト・複雑さ・エンジニアリングリードタイムの削減を享受できるように設計・開発・運用をできるようになりたい。

# 次のアクション

- [Hello! Elasticsearch](https://medium.com/hello-elasticsearch)
- [Classmethod 連載](https://dev.classmethod.jp/server-side/elasticsearch-getting-started-01/)

# 質問

- サーバーレスとは何か
- サーバーレスを採用する理由は何か
- メリットとデメリット
- サーバーレスはどんな用途で使われるか
- FaaS と Functional SaaS の違い

# 回答

## サーバーレスとは何か

- コンピューティングリソースをサービスとして利用すること。開発者は物理的なサーバーを考えたり管理したりする必要がない。

> developers no longer have to think that much about them. Computing resources get used as services without having to manage around physical capacities or limits.

by 「[Why The Future Of Software And Apps Is Serverless](https://readwrite.com/2012/10/15/why-the-future-of-software-and-apps-is-serverless/)」

- 「サーバという単位を意識しない」という考え方。サーバの抽象化。
- サーバーレスアーキテクチャは FaaS や BaaS を組み込んだアプリケーション設計

> Serverless architectures are application designs that incorporate third-party “Backend as a Service” (BaaS) services, and/or that include custom code run in managed, ephemeral containers on a “Functions as a Service” (FaaS) platform

by 「[Serverless Architectures](https://martinfowler.com/articles/serverless.html)」

## サーバーレスを採用する理由は何か

- 費用対効果、高速なスケール、ビジネスに注力できる

> One reason is affordability, another is the ability to scale quickly, and a third is not having to worry about things that aren’t strategic to their businesses

by 「[Why The Future Of Software And Apps Is Serverless](https://readwrite.com/2012/10/15/why-the-future-of-software-and-apps-is-serverless/)」

- 運用コスト・複雑さ・エンジニアリングリードタイムの削減

> Serverless architectures may benefit from significantly reduced operational cost, complexity, and engineering lead time

by 「[Serverless Architectures](https://martinfowler.com/articles/serverless.html)」

## メリットとデメリット

- メリット
  - 費用対効果
  - 高速なスケール
  - ビジネスに注力できる
  - 運用コスト・複雑さ・エンジニアリングリードタイムの削減
- デメリット
  - ベンダーロック
  - 比較的未熟なサポート

## サーバーレスはどんな用途で使われるか

- Web API
  - サーバーレスは一般的な CRUD ではなく CQRS の方が相性が良い
  - ex.) Command: DyanmoDB, Query: ElasticSearch, DynamoDB
- ストリーミング
  - 非同期ジョブ
  - 自動化
  - ログの集計・処理
- バッチ
  - 時間のかかる複雑な集計処理: AWS Step Functions, AWS Fargate

## FaaS と Functional SaaS の違い

- FaaS はいくつかの制約を受け入れた小さなコード（関数）をスケーラブルに実行できる環境。
  - ex.) AWS Lambda, Azure Functions, Google Cloud Functions...
- Functional SaaS はメール送受信や認証など何らかの具体的な機能を提供するサービス。BaaS とも呼ばれる。
  - ex.) Firebase, AWS SQS / SNS, Cognito
