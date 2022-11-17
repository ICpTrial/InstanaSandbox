## Applications

### 調査対象時間の設定
説明の都合上、 **2022年9月12日13時〜14時** で 起きた事象を 事後に確認するというシナリオ で、ハンズオンを実施していきます。  
Instana画面の操作方法は同じですので、任意の時間を選んでハンズオンを実施して頂いてもOKですが、このハンズオン環境自体が日々更新されているので、状況によってはエラーがない時間帯などもあります。

1. まずは一旦 説明通りに 触ってみたいという方は、右上の スコープを設定する画面で、**2022/09/12 13:00 - 2022/09/12 14:00** に設定してください。
<img width="1040" alt="image" src="https://user-images.githubusercontent.com/22209835/202365172-a5ae6827-c2af-4b42-98fe-bf5ce6e1296f.png">
調査時間が設定できますので、実際のユーザーから 問い合わせがあった場合などにも、時間を条件にして 調査対象データを絞り込むために使うことができます。  
なお、今回のように1ヶ月以上前のデータに遡ることもできますが、一度に表示できるデータは１ヶ月までです。また、古いデータは データ保持ポリシーに従って、少しづつ丸められていきます。

### アプリケーション
実際に 各Linuxノードや AIXノード、Kubernertesなどで稼働する アプリケーションについて見ていきます。
このデモ環境では設定を変更できないため、自分でアプリケーションの設定はできませんので、事前に定義された アプリケーションを見ていきます。
  
このハンズオン・シナリオで利用するアプリケーションは、Kubernetes上で稼働している RobotShop という 以下のようなインターネットショッピング・サイトです（この環境には直接アクセスできません）。  
製品デモ用サンプルですので、GitHub (https://github.com/instana/robot-shop) から入手して、自分の環境に導入することも可能です。
![image](https://user-images.githubusercontent.com/22209835/202367914-fa3e2079-f05f-418f-a696-a47717a8059d.png)

Instanaの左のメニューから、**Applications**のアイコンをクリックしてください。
![image](https://user-images.githubusercontent.com/22209835/114327991-3efac480-9b76-11eb-98a9-5bd536f758ac.png)

---
### サービス と アプリケーション

1. **Applications**と **Services**の２つのタブがありますが、まずは**Services**から見ていきます。  
ここには、Instanaのエージェントが検知したアプリケーション・サービスがリストされています。
Instanaにおけるサービス は、ある機能を提供するミドルウェアなどのコンポーネントに相当します。　　
従来型環境においては、環境変数の設定により 同じ技術であっても プロセスごとに表示することも可能です。
各行に、個々のサービスのテクノロジーやそのタイプ（HTTPやDATABASE, MESSAGINGなど）、および 各サービスのゴールデン・シグナル（コール数、応答性能、エラー率）が表示されています。  
<img width="1909" alt="image" src="https://user-images.githubusercontent.com/22209835/202366795-b5ef1004-a414-40cc-b825-be456f897dbd.png">

1. これらのゴールデン・シグナルに対して、メトリックの変化率を見ており、コール数の急減や応答性能の遅延、エラー率の急増といったイベントを検知して、ヘルス状況を表示しています。  
これらの問題の解析は、いったん後にして、もう少し画面を見ていきましょう。
<img width="1919" alt="image" src="https://user-images.githubusercontent.com/22209835/202366931-f49e12f8-f4cb-4e2b-a6d0-c8226af842e4.png">

1. つぎに **Applications**のタブを開きましょう。
さきほどの Services タブは、テクノロジーのリストであり、業務ユーザーにとっては意味をなしません。検知されたテクノロージを、ユーザーにとって意味のある体系に整理するビューが**Applications**です。  
たとえば、特定のサービスに特化したダッシュボードや、フロントエンド含めシステム全体のサービスを確認するビューです。また、DB管理者には、稼働するDatabaseすべてを含むビューが必要かもしません。  
特定のノードで稼働するアプリケーション、特定の名前空間で稼働するアプリケーション、特定のサービスの下流にあるアプリケーションなど、このアプリケーション・タブは、ユーザーにとって管理しやすいよう、自由に定義・編集が可能です。
![image](https://user-images.githubusercontent.com/22209835/114328104-8d0fc800-9b76-11eb-8d67-ee44778b3a52.png)

### アプリケーション・パフォーマンスの把握

1. **robot-shop with frontend**のApplicaionsビューをクリックしましょう。  
RobotShop を構成するマイクロサービス全体の**Summary**のダッシュボードが開きます。
上段には、指定された 13時〜14時の間の ゴールデン・シグナル（コール数、エラー数/率、応答性能）およびその履歴が表示されています。 
<img width="1835" alt="image" src="https://user-images.githubusercontent.com/22209835/202369130-886d565a-9230-4245-8dff-528c5adb003a.png">
下には関連する基盤で発生した基盤の問題と変更の履歴、各ゴールデンシグナルでのサービスのランキング、および処理時間が表示されています。
<img width="1831" alt="image" src="https://user-images.githubusercontent.com/22209835/202369338-1504f14c-edbe-4998-b5fe-3abbbe50a0e9.png">
下段中央の トップ・サービスでは、応答が悪化しているサービスやエラー数が多いサービスを確認できますので、特に注視が必要なものが分かります。  
Latency(応答性能）、Calls（コール数）、Erroneous Calls（エラー数）を選択し表示を切り替えてみてください。
1. 次に **Dependency**のタブを開きましょう。  
ここでは RobotShopを構成する様々なサービスの依存関係（コンテキスト）が可視化されています。
細かい機能がひとつひとつのサービスとして稼働していますので、従来型の環境に比べて依存関係が複雑になります。動いている一つ一つの点が サービス間の要求です。  
Instanaは、これらの要求を解析することで、依存関係をダイナミックに可視化しています。もし色が付いているサービスがあれば、それは問題が発生しているサービスです。
<img width="1830" alt="image" src="https://user-images.githubusercontent.com/22209835/202371365-da27166a-c897-49c5-94f5-fabcb7edb525.png">
1. ひとつのサービス **discount** にカーソルを合わせて見ましょう。そのサービスと依存関係のあるサービスのみにフォーカスが当たります。
<img width="1829" alt="image" src="https://user-images.githubusercontent.com/22209835/202371686-d2f83968-1cef-42fb-b69b-fb3a8c4a1aee.png">
1. 左上の メニューを選択することで、応答性能が遅いサービスのアイコンを大きくしたり、要求数の大きいサービスを大きくしたり、依存関係の表示を変更したりきますので、いろいろ触ってみてください。　　
<img width="1829" alt="image" src="https://user-images.githubusercontent.com/22209835/202372452-c24c98ff-9348-48dd-83cf-5ba8739d20b2.png">
1. 次依存関係ビューから サービスにドリルダウンしてみます。ここでは **shipping**サービスを開いてみましょう。
<img width="812" alt="image" src="https://user-images.githubusercontent.com/22209835/202373248-a9a0cb9a-5df4-4152-a028-7190bc686989.png"

### 個別サービスの状況の把握

1. **Shipping**サービスのダッシュボードに遷移してきました。ここでは、システム全体の中で、この**Shipping**サービスに関わるデータだけが抽出されています。
     上段は先ほどと同様 指定された時間での 要求数と、発生したエラーの数、応答性能です。
     下段の中央が、今度はkono **Shipping**サービスを構成する エンドポイントごとの集計です。この**Shipping**は SpringBootのアプリケーション・サーバーですので、HTTP要求のPATHごとにエンドポイントが表示されています。
<img width="1839" alt="image" src="https://user-images.githubusercontent.com/22209835/202373384-b6b9c499-5dac-41b2-bb3a-33c38e203175.png">

![image](https://user-images.githubusercontent.com/22209835/114330307-62c10900-9b7c-11eb-846f-d84a3547b5a9.png)
1. 開くと、citiesサービスの詳細が表示されています。右下には、応答時間がかかっているSQLが順に表示されています。
![image](https://user-images.githubusercontent.com/22209835/114330341-73717f00-9b7c-11eb-981b-2dacf702c549.png)
 
---
### アプリケーションの問題切り分け

1. **Summary**のダッシュボードに戻ります。
エラーとなっているコールがありますので、ここを確認していきましょう。  
もしエラーがない状況でしたら、右上のボタンで表示時間を１時間や６時間、１２時間などに広げてみてください。  
![image](https://user-images.githubusercontent.com/22209835/114329793-3e186180-9b7b-11eb-9dd4-cd363cd1ee1a.png)
1. 中央のエラーコール率のグラフの山をマウスで選択して、**View in Analyze**で解析画面で確認していきます。  
タイミングによって、起きているエラーは異なりますので、みなさんの画面で確認しているエラーを選択して開いて下さい。
![image](https://user-images.githubusercontent.com/22209835/114329771-2e008200-9b7b-11eb-8da1-58dab02b41c3.png)
1. アプリケーションを理解していれば、より具体的にアクションが採れるかもしれませんが、ここでは、一番エラー数の多い上の **eum-frontend**を選択します。  
タイミングによって起きているエラーは異なりますので、環境に応じて 一番多いエラーを選択して開いて下さい。
![image](https://user-images.githubusercontent.com/22209835/114329840-5c7e5d00-9b7b-11eb-9926-f7f1f0cc29c1.png)
1. ここでは、エラーを返している **eum-frontend**の要求がリストされています。  
軒並み応答性能が5000ミリ秒を超えてエラーとなっているようですね。これらについて詳細を確認していきましょう。  
一番上のエラー要求をクリックして、要求の中身をみていきます。
![image](https://user-images.githubusercontent.com/22209835/114329872-699b4c00-9b7b-11eb-9e26-f49bb8836b59.png)
1. この `GET /zh_cn/shop`要求の詳細がわかります。中身を確認しながらスクロールダウンしてください。
![image](https://user-images.githubusercontent.com/22209835/114329913-7c158580-9b7b-11eb-8843-5767842cbb98.png)
1. タイムラインのビューでは、この要求に関連して実行された マイクロサービスの呼び出し関係が可視化されています。
![image](https://user-images.githubusercontent.com/22209835/114329938-8e8fbf00-9b7b-11eb-82b4-b0b2e79366ce.png)
1. さらにスクロールダウンしていくと、コールのビューでは、各マイクロサービスの呼び出しの依存関係 呼び出し元と呼び出し先が確認できます。
![image](https://user-images.githubusercontent.com/22209835/114329959-a0716200-9b7b-11eb-8eaa-bd8b8fe06ecf.png)
1. マイクロサービスの一番下で、DATABASE（MySQLサービス）への CONNECT要求が5000ミリ秒でタイム・アウトし、エラーなっているのが分かります。
右のペーンには、エラーの内容と、問題が発生したコードのスタックトレースが表示されています。
![image](https://user-images.githubusercontent.com/22209835/114329998-b2eb9b80-9b7b-11eb-9412-ecda686ca624.png)
1. 問題となっている MySQLサービスをクリックすると、当該時間帯に Offlineが検知されているのが分かります。
![image](https://user-images.githubusercontent.com/22209835/114330035-c8f95c00-9b7b-11eb-9618-9da6e087cea4.png)
このようなかたちで、エラー応答となったマイクロサービスの依存関係を解析した上で、問題の根本原因の分析へと絞り込んでいくことが可能です。

---
ここまでで、サーバー側のマイクロサービスの挙動を理解するための**Applications**の確認は終了です。  
次に、ブラウザやモバイル・アプリケーションなど、エンドユーザー側の挙動をみる [WebSites & MobileApps](https://github.com/ICpTrial/InstanaSandbox/blob/main/WebSites%26MobileApps.md)をみていきます。
