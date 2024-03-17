# 職務経歴書



## スキル要約（自己PR)

- エンジニアとして、フロントエンド、バックエンド、インフラと全般的な業務に携わってきました。
システム全体を総合的に俯瞰し、なおかつビジネス的な観点も考慮しつつ最適な問題解決を常に追い求めています。
また、品質（パフォーマンス、保守性etc）と開発スピードの両立を常に心がけています。
- 携わる企業様のビジネスの成功を常に第一目標としており、過去にはHerokuからAWSへの全インフラの移行を一人で担当し、パフォーマンス、可用性等を維持したまま年間800万円のインフラコスト削減を達成しました。
- 技術のキャッチアップを得意としており、未経験の技術でも迅速にバリューを発揮できるよう全力で努めてまいります。
  
  
## スキル

基本的にすべて実業務で使用した技術だけを列挙しています。

### 言語
Ruby | Node.js | Python | JavaScript | TypeScript | Google Apps Script

### フレームワーク等
Ruby on Rails | Express.js | React | Next.js | jQuery | Serverless Framework

### RDB/NoSQL
MySQL | PostgreSQL | Redis | DynamoDB | MongoDB

### AWS
VPC | S3 | CloudFront | API Gateway | Lambda | ELB | EC2 | ECS | Fargate | Route53 | IAM | Cognito | RDS(MySQL|PostgreSQL) | Aurora | DynamoDB | ElastiCache(Redis) | SNS | SES | CloudWatch | EventBridge | CloudTrail  | KMS | Parameter Store | Client VPN | VPC Peering | CodePipeline | CodeBuild | CodeCommit | ECR

### Google Cloud
Firebase(Firestore|Firebase Authentication|CloudFunctions)

### SaaS/PaaS
Heroku | Vercel | GitHub | GitHub Actions | CircleCI | BugSnag | Sentry | Rollbar | NewRelic | Datadog | Pingdom

### その他
Docker | Docker-Compose | Vagrant | Redash | Terraform

## 主な業務経歴



- [単発アルバイトマッチングサービスの開発・保守](https://github.com/atsushikaneko/skill-sheet?tab=readme-ov-file#%E5%8D%98%E7%99%BA%E3%82%A2%E3%83%AB%E3%83%90%E3%82%A4%E3%83%88%E3%83%9E%E3%83%83%E3%83%81%E3%83%B3%E3%82%B0%E3%82%B5%E3%83%BC%E3%83%93%E3%82%B9%E3%81%AE%E9%96%8B%E7%99%BA%E4%BF%9D%E5%AE%88)
- [クラウド会計サービスの開発・保守](https://github.com/atsushikaneko/skill-sheet?tab=readme-ov-file#%E3%82%AF%E3%83%A9%E3%82%A6%E3%83%89%E4%BC%9A%E8%A8%88%E3%82%B5%E3%83%BC%E3%83%93%E3%82%B9%E3%81%AE%E9%96%8B%E7%99%BA%E4%BF%9D%E5%AE%88)



## 単発アルバイトマッチングサービスの開発・保守

### 期間・規模
2022/1~現在
PO1名、開発メンバー1-5名、デザイナー1名


### 担当業務

HerokuからAWSへの全インフラの移行

### 課題

- インフラコストの高さ
  - 本プロジェクトでは創業初期の頃からインフラとしてHeroku Enterpriseを利用しており、非常にインフラコストが高くなっていました。(年間950万円)
- キャッシュフローへの負担
  - またHeroku Enterpriseは年間契約のみで、1年分のインフラコストを現金で先払いする必要がありキャッシュフローの観点からも大きな重荷になっていました。

### 解決策

HerokuからAWSへの全インフラの移行を提案し、実施しました。

### 成果

- Heroku Enterpriseで年間950万かかっていたインフラコストを、750万円削減し年間約200万円にすることができた。
- AWSは毎月利用分を後払い、尚且つクレカ支払いもできるのでキャッシュフローを大幅に改善することができた。
- コストは大幅に削減しつつ、パフォーマンス、可用性、セキュリティ等といった質の部分を維持（or 向上）することができた。
- これまで開発メンバーがHerokuで行っていた様々な作業（コンテナ上でのRailsコンソールの起動、任意のタイミングで作業ブランチをステージング環境にデプロイして動作確認をするなど）を、AWSへの移行後も問題なく行えるような形でできた。

### HerokuからAWSへの全インフラの移行の詳細

- ゴール
  - HerokuからAWS移行によるコストの大幅削減   
  - コストを大幅削減してもパフォーマンス、可用性、セキュリティ等を維持する
  - チームが慣れているHerokuからAWSにインフラが移行することで運用・開発の効率を落とさないこと(=運用の手間が増えて本末転倒にならないこと)
- 技術選定
  - ECS + Fargate
    - 選定理由
      - 可用性の高さ
        - ECSサービスは、ECSタスクがダウンしても指定の数のECSタスク数を維持するように、自動で新しいECSタスクを起動してくれる。EC2でも同じような要件は達成できるがECSはデフォルトの機能として提供されており特別な設定をせずにできる。またEC2インスタンスの起動よりECSタスクの起動のほうが速いため、仮にダウンタイムが生じても少なくて済む点も魅力的だった。
      - ECSタスク上でRailsコンソールを起動することができる
        - Herokuで運用時でコンテナ(正確にはdyno)にログインして、Railsコンソールを開いて本番DBを確認したりデータの更新することがあったので、AWS移行後も同様にコンテナ上でRailsコンソールが使える必要があったが、ECSはECS EXECという手段で同要件を達成できる。App Runnerは同要件が達成できなかったため採用しなかった。
      - キャッチアップがEKSと比較し容易であること
        - EKSも選択肢にありましたが、開発チームの新しいインフラへのキャッチアップのしやすさ、他のAWSのサービスの統合のしやすさ等を考慮しECSを採用した。（今後のマルチクラウドの想定がなかったのもEKSを選択したなかった理由の１つ)
      - 一貫性
        - ECS本番環境とローカル開発環境と同じDockerfileを使うことでローカルでは動作したが、本番では動作しないといった問題を避けることができる点が魅力的だった
  - Aurora
  - ElastiCache
  - Amazon SES
    - 選定理由
      - HerokuのときはHerokuアドオンとして提供されていたSendGridというサービスをメールサーバーとして使っていたが、コスト削減のためにSESに移行した。送信するメールの数が数十万件/月と多かったためSendGridでは約12万円/月くらいのプランに入っていたが、SESに移行することで5,000円/月まで削減することができた。
  - EventBridge
    - 選定理由
      - HerokuのときHerokuスケジューラという指定の時間にバッチ処理を実行する機能があったが、その機能の代替として採用。指定の時間にECSタスクを起動して指定のコマンドを実行するようにした。
  - CloudWatchメトリクス
  - CloudWatch Logs
  - CloudWatch Alarm
  - CodePipeline
  - CodeBuild
  - ECR
  - AWS Lambda
  - Github Actions

- 工夫したところ
  - ECS Fargateのスペック(vCPU数, メモリ)の最適化
    - はじめはHeroku運用時を参考にだいたいのスペックを決めて、あとは実際に運用しつつCloudWatchメトリクスのCPU利用率、メモリ利用率を見ながら、パフォーマンスに全く問題ない範囲で最も安くなるように調整した。
    - またトラフィックが多い時間は指定したCPU利用率、メモリ利用率を超えるとオートスケールするようにした
  - Staging環境におけるFargate Spotの利用
    - Staging環境は全てのECSタスクで通常のFargateではなくFargate Spotを利用するようにすることで、通常のFargateと比較して70%程度のコスト削減ができた。
    - Staging環境では仮にECSタスクが急に停止してもそこまで大きな問題ではない上に、実際に運用してみると週に1,2回程度しかFargate Spotの停止は発生していなかった。また仮に発生してもECSサービスによってすぐに新しいタスクが起動するため運用上支障が生じたことはなかった。
  - SESでユーザーのメール受信・開封・リンクのクリック等をトラッキングできるようにした
    - もともとHerokuではHerokuのアドオンであるSendGridをメールサーバとして利用していた。SendGridでは送信されたメールをユーザーが受信したか、開封したか等をトラッキングできる機能がデフォルトで提供されていて運用上、とても重宝していた。しかし、SESはデフォルトでは、そのような機能が提供されていなかったので、SNS、AWS Lambda、CloudWatch Logsと組み合わせることで追跡できるようにした。
  - AWSのアカウント上に存在した既存の不要なインフラの整理
    - 今回のAWS移行以前からもともと様々な用途（Redashのデプロイ等）でAWSを利用しており。不要なEC2インスタンス、EBS、EBSのスナップショット、NATゲートウェイ等が存在したため整理し削除した。また、Redashインスタンスのインスタンスタイプの最適化、Redashインスタンスで使っているEBSを必要最低限のサイズに入れ替える等を行った。
  - 拡張性のあるネットワーク
    - サブネットは、publicサブネット(IGW経由でインターネットと通信)、protectedサブネット(nat gateway経由でインターネットにアウトバウンド通信)、privateサブネット(インターネットと通信しない)を、東京リージョンの3箇所のAZに１つずつ作成した（合計9サブネット）。このような構成だと、だいたいのユースケースに対応でき、今後の拡張性を担保することができた。
  - 最小権限を意識
    - AWSの原則である最小権限を意識してインフラ構築を行った。例えば、ECSタスク、Aurora、ElastiCache などへは最低限の権限のみをもつIAMポリシーをアタッチし、ネットワークのセキュリティグループ、ネットワークACLも運用上必要なトラフィックのみ許可するような形で設定した。
  - CDパイプラインの工夫
    - Herokuで運用していたとき、開発チームでは任意のタイミングで作業ブランチをステージング環境にデプロイして動作確認を行っていたため同要件をAWSでも行えるようにする必要があった。CDパイプラインを全てAWS CodePipelineで行うのではなくイメージビルドだけGithubActionsで行うことで同要件を達成することができた。
  - 本番環境の移行作業の準備を徹底した
    - VercelとHerokuのメンテナンスモード => Heroku Postgresのバックアップ => バックアップのAuroraへのリストア => DNSサーバでドメインの解決先をHerokuからAWSのALBへの変更といった一連の流れを事前に2回ほど実際に全て通して行い手順書化し、ミスが発生しないようにした。また仮にどこかで不測の事態が発生してもHerokuの環境に戻せるような手順も事前に準備しておいた。深夜1時から実際の本番環境移行作業を開始し、問題なく朝5時くらいに完了することができた。
    - また、移行作業を行う時間帯にサービスを使うと思われる人（その時間帯に勤務がある人など）をRedashで抽出し、カスタマーサポートチームと連携し、ユーザーが移行作業中にWebアプリケーションが見れなくても問題が生じないないように手配した。
  - 運用体制の整備
    - アーキテクチャの仕様、各種設定、操作手順等を文書化してチーム内で共有しました。加えて、本番環境の移行に先駆けて、Staging環境を1ヶ月前にAWSに移行し、開発チームがAWSの運用に円滑に移行できるよう配慮しました。
- 反省点
   - 本番環境とStaging環境を同じアカウント内に作成してしまったので、本番環境だけでいくらかかっているかを確認するのに手間がかかってしまう。なのでアカウントを分けるべきだったと思っています。(アカウント自体を分けることで各環境のコストが明確になり、管理がしやすくなるメリットがあります。)


### その他の担当業務

以下長くなりますが、本プロジェクトにおけるその他の実績になります。

- 源泉徴収票PDFの発行機能の実装
- 労働関係の法律に関連する勤務制限機能の実装
- 求人掲載時の最低賃金のチェック機能 の実装
- ワーカーのスコアリング機能の実装
  - 勤務を直前で欠勤した際等にスコアが減点され、スコアが0になると一定期間利用停止になるようなユーザーの質を担保する機能です
- ユーザーブラックリスト機能の実装
- ユーザー退会機能の実装
- チャット機能の大幅アップデート
- ユーザー自動ログアウト機能の実装
- 各種メンテナンス
  - 本番環境のDBのバージョンアップ（postgres, redis）
  - Rubyのバージョンアップ（v2.6.3 => v2.7.7, v2.7.7 => v3.0.6）
  - Ruby on Railsのバージョンアップ（ v6.0 => v6.1, v6.1 => v7.0）
  - 各種ライブラリのバージョンアップ
- コスト削減の提案・実施
  - 不要なLINE通知の削減
    - 退会者、ブラックリストに入っているユーザー、すでに該当の日に勤務が決まってる人に新規求人掲載の通知が送信されないようにする
    - LINE通知はユーザーごとに1通あたり約2円するため上記改善により15万円/月程度のコスト削減になりました
  - Datadogのログの運用の改善によるコスト削減
    - 30万円/月程度のコスト削減になりました (詳細: https://qiita.com/snooow/items/45038ff9205db365d3fb )
- マーケティングチームのサポート
  - ユーザーのトラッキング機能の追加
  - Google Tag Managerの導入
  - 広告コンバージョンの集計
- Webアプリケーションのパフォーマンス改善
  - フロントからバックエンドへの不要なリクエストの削減・一元化
  - 逆に重い処理が含まれるGraphQL Fieldは、別リクエスト化することでLCPの改善
  - GraphQL Batch gemの導入によるGraphQLのパフォーマンス改善
  - ActiveRecordの「Lazy Loading」と「Eager Loading」という概念を利用して、DBへのアクセスを最適化
- インフラ、DBのパフォーマンスチューニング
  - pumaの並列数の最適化
  - サイズが大きくボトルネックになっているテーブルへのインデックスの追加
- Redashクエリ・ダッシュボード作成による業務の可視化・分析・効率化
  - 経営判断に使うデータの集計（月別応募者数・月別勤務数・月別新規登録数etc）
  - 行政機関に提出するデータの集計（有効求職者数・新規求職申込件数etc）
  - 運用効率化関連（勤務終了後に勤怠登録が完了していないユーザーが存在する店舗一覧を抽出etc）
- 開発環境の改善
  - docker-compose.yml の設定変更による開発環境の高速化・改善
    - コンテナ起動に時間がかかる問題の解決
    - DBが永続化できていない問題の解決（詳細: https://qiita.com/snooow/items/04a84193fb6c7076e86f ）
  - ローカルで自動テスト(Rspec)が落ちる問題の解決
  - Rubocopのメンテナンス
- GASによる業務効率化ツールの作成
  - 店舗へのユーザー出勤簿自動定期送信ツール
  - LINEオーディエンスの自動定期更新ツール
- その他
  - ソースコードの各種リファクタ
  - 各種バグ改修
  - 各種UIの改修・改善
  - コードレビュー
  - 外国人エンジニアとのブリッジ役
  - テクニカルサポート全般
  - 運営Admin画面の改善

---

## クラウド会計サービスの開発・保守

### 期間・規模

2021/8 - 2021/12

全体で開発80名以上
私が属していたチームは4名

### 担当業務

- 金融機関のWebサイトをクローリングし利用明細データをインポートする機能の調査・実装
  - 大手のクラウド会計サービスだったため、すでに数百を超える金融機関からデータをインポートする機能が存在しており、私が担当したのは新しい金融機関の追加でした。
  - 担当した金融機関は某クレジットカード会社で、APIが提供されていなかったためクローリングでデータを取得する機能を作成しました。
  - 金融機関のWebサイト上で、クラウド会計サービスで必要な数十種類のデータがどのページの、どの部分に存在するか調査しマッピング表を作成しました。
  - 他の金融機関のインポート機能を参考に機能の実装、自動テストの実装、Staging環境での動作確認、リリースを行いました。
    - 比較的大規模なシステムだったため、
- 金融機関のAPIから利用明細データをインポートする機能の調査・実装
  - APIが提供されている金融機関の場合は、クローリングではなくAPIで利用明細データをインポートしました。
  - 基本的な流れはクローリングの場合と同様です。API仕様書を確認しながら、クラウド会計ソフトで必要なデータとAPIのレスポンスデータをマッピングする表を作成し、実装を行いました。
- 各種テクニカルサポート
  - 金融機関からデータが正しくデータが取得できない等の問い合わせに対して調査を行い原因の特定し、ソースコードの修正等を行いました。

---
## 大手教育系BtoCサービスの開発・保守

2021/2 - 2021/7

### 期間・規模

2021/8 - 2021/12

PM １名
開発 5名

### 担当業務

- 各種APIの開発
- graphQLのパフォーマンス改善
  
---

## 複数ECモール一元管理システム（SaaS）の開発

### 期間・規模

2020/2 - 2021/1

- PM １名
- 開発 20名以上

### 担当業務

- 各種APIの開発
- ECモールから在庫データをインポートする機能の開発
- ECモールに商品を出品する機能の開発
- 手動E2Eテスト
