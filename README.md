# IBM Observability with Instana 

IBM Observability with Instana は、アプリケーションの可観測性を提供する IBM の 新しい アプリケーション・パフォーマンス管理基盤です。
「監視 Monitoring」 が 受け身/消極的なニュアンスで語られるに比し、「可観測性 Observability」 は、パフォーマンスとサービスの改善を行うために、システムの内部の状態を、外部から取得できるデータによって対象を積極的に理解していく言葉です。

![image](https://user-images.githubusercontent.com/22209835/114111888-14aacc00-9916-11eb-85ff-22667a629775.png)

### 監視構成の自動化
IBM Observability with Instana （以降 Instana と略）は、（できる限り）ゼロ構成で クラウド・ネイティブ環境を自動的に可視化する 次世代の可観測性基盤を提供します。
Instana は、各ノードに１つのエージェントが導入されます。このエージェントがそのノードで稼働するテクノロジーを自動的に把握し、そのテクノロジーに対応したセンサーを動的にロード、構成して、モニタリングを開始します。

Instanaは 180を超えるテクノロジーに対応したセンサーをInstanaは提供しています（センサーのリストは[こちら](https://www.instana.com/supported-technologies/))。
これらには LinuxやKubernetesといった基盤から、JavaやNode.js など多様なランタイム、商用ミドルウェア、オープンソース・ミドルウェアなどが含まれます。IBM買収後は、主要なIBMミドルウェア製品、Power環境（AIXおよびiSeries）、z/OS環境 への対応も強化させています。
対応した各種センサーには、これまでのユーザー・フィードバックに基づいて設定された 各テクノロジーの監視項目のデフォルト設定が組み込まれ、OutOfBoxで クラウド・ネイティブ環境のモニタリングを開始することが可能です。
Kubernetes環境のうような継続的にアプリケーションが変化していくような環境であっても、Instanaエージェントはつねにテクノロジー状況の変化も確認しているため、システム管理者が変更を行わなくても、変化に追随していくことが可能です。

### コンテキストの提供
各テクノロジーのセンサーは、対応するランタイムにおいて 全要求をトレースし、各コンテナー間の依存関係のリアルタイムで解析し可視化します。これにより、リリースによって変化するアプリケーションの依存関係や、動的に変化する アプリケーションの構成（インスタンス数の変化など）にも追随していくことが可能です。また、このアプリケーションの依存関係は、クラスターやリージョン（データセンター）またがった構成、クラウドや仮想化環境をまたがった構成であっても可視化することが可能であり、稼働するアプリケーションを、統合的に管理していくことが可能です。Intanaのトレーシング機能は、サンプリングではなく、全要求トレースである点が、他社APM製品との大きな差異です。

### AI/MLによるインシデント通知
各サービスのモニタリングには、ゴールデン・シグナルに対して 機械学習を適用して監視を行っています。これにより応答性能の変化など 単純なしきい値監視では拾うことができない、通常とは異なる振る舞いを インシデントとして拾うことが可能になっています。またAIにより、季節性（日次や週次での周期性）を理解した上で、動的なサービスレベル監視を設定することも可能です。インシデントの通知を上げる際には、上で述べたようにそのサービスが稼働するアプリケーションのコンテキストを理解していますので、前後上下関連コンポーネントでのイベントもあわせて整理して通知することが可能です。これにより、問題判別、課題解決への時間を短縮していくことが可能です。

---
## Observability を構成する3つの要素

CNCF の TAG_Obserability(※Technical Advisory Group)では、Observability を構成する プライマリー・シグナルとして、以下の３つをあげています。
* メトリック
* トレース
* ログ

<img width="629" alt="image" src="https://user-images.githubusercontent.com/22209835/171099082-dd4d6b2a-427d-4261-a6ba-94f3ed489bc6.png">

Instana も、これらの主要な３つのシグナルにもとづいて、アプリケーションの稼働状況を明らかにしていきます。

---

## ハンズオン環境の準備
このハンズオンでは、Instana のデモ環境である **Play with Instana** を利用して、実際に稼働する Instana の環境を確認していきます。
Play with Instanaは、グローバル環境で日本語設定に切り替えられない点や構成の変更などができない点を除けば、実際の製品そのものです。

[Play with Instana](https://www.instana.com/getting-started-with-apm/) をクリックしますと、以下の画面が開きますので、紫の**Play with**のボタンをクリックします。  
メール・アドレスを入力して、Play with Instana を開始してください。  
![image](https://user-images.githubusercontent.com/22209835/114133781-8cdab700-9941-11eb-93f8-0c1e6ec5656a.png)

環境が開いて、準備できたら、[こちらからStep By Stepのハンズオン](https://github.com/ICpTrial/InstanaSandbox/blob/main/infrastructure%26platform.md)を開始しましょう。

|章|ハンズオンリンク|備考
--|--|--
|1|[Infrastructure & Platform](https://github.com/ICpTrial/InstanaSandbox/blob/main/infrastructure%26platform.md)|基盤およびKubernetes/CloudFoundryなどプラットフォーム|
|2|[Applications](https://github.com/ICpTrial/InstanaSandbox/blob/main/Applications.md)|マイクロサービス・アプリケーション稼働状況の可視化|
|3|[WebSites & MobileApps](https://github.com/ICpTrial/InstanaSandbox/blob/main/WebSites%26MobileApps.md)|エンドユーザー・挙動の理解|
|4|[Events](https://github.com/ICpTrial/InstanaSandbox/blob/main/Events.md)|AIおよび機械学習により通知されたイベントからの問題判別|
