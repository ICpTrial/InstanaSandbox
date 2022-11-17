## Applications

### 0. サンプル・アプリケーション
実際に 各Linuxノードや AIXノード、Kubernertesなどで稼働する アプリケーションについて見ていきます。
このデモ環境では設定を変更できないため、自分でアプリケーションの設定はできませんので、事前に定義された アプリケーションを見ていきます。

このハンズオン・シナリオで利用するアプリケーションは、Kubernetes上で稼働している RobotShop という 以下のようなインターネットショッピング・サイトです（この環境には直接アクセスできません）。  
製品デモ用サンプルですので、GitHub (https://github.com/instana/robot-shop) から入手して、自分の環境に導入することも可能です。
　　![image](https://user-images.githubusercontent.com/22209835/202367914-fa3e2079-f05f-418f-a696-a47717a8059d.png)
  
---

### 1. 調査対象時間の設定
説明の都合上、 **2022年9月12日13時〜14時** での状況を 事後に確認するというシナリオ で、ハンズオンを実施していきます。  
Instana画面の操作方法は同じですので、任意の時間を選んでハンズオンを実施して頂いてもOKですが、このハンズオン環境自体が日々更新されているので、状況によってはエラーがない時間帯などもあります。

1. まずは一旦 説明通りに 触ってみたいという方は、右上の スコープを設定する画面で、**2022/09/12 13:00 - 2022/09/12 14:00** に設定してください。
　　<img width="1040" alt="image" src="https://user-images.githubusercontent.com/22209835/202365172-a5ae6827-c2af-4b42-98fe-bf5ce6e1296f.png">
調査時間が設定できますので、実際のユーザーから 問い合わせがあった場合などにも、時間を条件にして 調査対象データを絞り込むために使うことができます。  
なお、今回のように1ヶ月以上前のデータに遡ることもできますが、一度に表示できるデータは１ヶ月までです。また、古いデータは データ保持ポリシーに従って、少しづつ丸められていきます。

---
### 2. サービス と アプリケーション
1. Instanaの左のメニューから、**Applications**のアイコンをクリックしてください。
　　![image](https://user-images.githubusercontent.com/22209835/114327991-3efac480-9b76-11eb-98a9-5bd536f758ac.png)
1. **Applications**と **Services**の２つのタブがありますが、まずは**Services**から見ていきます。  
ここには、Instanaのエージェントが検知したアプリケーション・サービスがリストされています。  
Instanaにおけるサービス は、ある機能を提供するミドルウェアなどのコンポーネントに相当します。従来型環境においては、環境変数の設定により 同じ技術であっても プロセスごとに表示することも可能です。  
各行に、個々のサービスのテクノロジーやそのタイプ（HTTPやDATABASE, MESSAGINGなど）、および 各サービスのゴールデン・シグナル（コール数、応答性能、エラー率）が表示されています。
    <img width="1909" alt="image" src="https://user-images.githubusercontent.com/22209835/202366795-b5ef1004-a414-40cc-b825-be456f897dbd.png">
1. これらのゴールデン・シグナルに対して、メトリックの変化率を見ており、コール数の急減や応答性能の遅延、エラー率の急増といったイベントを検知して、ヘルス状況を表示しています。  
これらの問題の解析は、いったん後にして、もう少し画面を見ていきましょう。
    <img width="1919" alt="image" src="https://user-images.githubusercontent.com/22209835/202366931-f49e12f8-f4cb-4e2b-a6d0-c8226af842e4.png">
1. つぎに **Applications**のタブを開きましょう。
さきほどの Services タブは、テクノロジーのリストであり、業務ユーザーにとっては意味をなしません。検知されたテクノロージを、ユーザーにとって意味のある体系に整理するビューが**Applications**です。  
特定のノードで稼働するアプリケーション、特定の名前空間で稼働するアプリケーション、特定のサービスの下流にあるアプリケーションなど、このアプリケーション・タブは、ユーザーにとって管理しやすいよう、自由に定義・編集が可能です。たとえば、システム全体のサービスや特定環境（本番、テスト、災対など）に特化したものなどを定義できます。DB管理者には、稼働するDatabaseすべてを含むビューが必要かもしません。  
    ![image](https://user-images.githubusercontent.com/22209835/114328104-8d0fc800-9b76-11eb-8d67-ee44778b3a52.png)

### 3. アプリケーション・パフォーマンスの把握

1. Applicaions のリストの中から、**robot-shop with frontend**をクリックしましょう。  
RobotShop を構成するマイクロサービス全体の**Summary**のダッシュボードが開きます。  
上段には、指定した 13時〜14時の間の ゴールデン・シグナル（コール数、エラー数/率、応答性能）およびその履歴が表示されています。 
    <img width="1835" alt="image" src="https://user-images.githubusercontent.com/22209835/202369130-886d565a-9230-4245-8dff-528c5adb003a.png">  
下には関連する基盤で発生した基盤の問題と変更の履歴、各ゴールデンシグナルでのサービスのランキング、および処理時間が表示されています。
下段中央の トップ・サービスでは、応答が悪化しているサービスやエラー数が多いサービスを確認できますので、特に注視が必要なものが分かります。  
Latency(応答性能）、Calls（コール数）、Erroneous Calls（エラー数）を選択し表示を切り替えてみてください。
    <img width="1831" alt="image" src="https://user-images.githubusercontent.com/22209835/202369338-1504f14c-edbe-4998-b5fe-3abbbe50a0e9.png">

1. 次に **Dependency**のタブを開きましょう。  
ここでは RobotShopを構成する様々なサービスの依存関係（コンテキスト）が可視化されています。
この環境では細かい機能がマイクロサービスとしてひとつひとつ稼働していますので、従来型の環境に比べて依存関係が複雑になります。動いている一つ一つの点が サービス間の要求です。  
Instanaは、これらの要求を解析することで、依存関係をダイナミックに可視化しています。もし色が付いているサービスがあれば、それは問題が発生しているサービスです。
    <img width="1830" alt="image" src="https://user-images.githubusercontent.com/22209835/202371365-da27166a-c897-49c5-94f5-fabcb7edb525.png">
1. ひとつのサービス **discount** にカーソルを合わせて見ましょう。そのサービスと依存関係のあるサービスのみにフォーカスが当たります。
    <img width="1829" alt="image" src="https://user-images.githubusercontent.com/22209835/202371686-d2f83968-1cef-42fb-b69b-fb3a8c4a1aee.png">
1. 左上の None と表示されている メニューを選択することで、応答性能が遅いサービス(Max Latency)のアイコンを大きくしたり、要求数の大きいサービス(Incoming Calls)を大きくしたり、依存関係の表示を変更したりきますので、いろいろ触ってみてください。　　
    <img width="1829" alt="image" src="https://user-images.githubusercontent.com/22209835/202372452-c24c98ff-9348-48dd-83cf-5ba8739d20b2.png">
1. 次依存関係ビューから サービスにドリルダウンしてみます。  
ここでは左側にある **shipping**サービスを クリックして **Go to Dashboard** を選びます。
    <img width="812" alt="image" src="https://user-images.githubusercontent.com/22209835/202373248-a9a0cb9a-5df4-4152-a028-7190bc686989.png"> 

### 4. 個別サービスの状況の把握
1. **Shipping**サービスのダッシュボードに遷移してきました。  ここでは、システム全体の中で、この**Shipping**サービスに関わるデータだけが抽出されています。
     上段は先ほどと同様 指定された時間での 要求数と、発生したエラーの数、応答性能です。  
     下段の中央が、この **Shipping**サービスを構成する エンドポイントごとの集計です。 この**Shipping**は SpringBootのアプリケーション・サーバーですので、HTTP要求のPATHごとにエンドポイントが表示されています。
    <img width="1839" alt="image" src="https://user-images.githubusercontent.com/22209835/202373384-b6b9c499-5dac-41b2-bb3a-33c38e203175.png">

1. この画面で Flowのタブを開きましょう。
サービスレベルの Flow タブでは、このサービスが呼び出している または このサービスを呼び出している 周辺サービスの状況を確認できます。  
この **Shipping** は **cart** と **cities** という２つのサービスを呼び出しているようですね。各サービスの 処理数、応答性能、エラー率も確認できます。
    <img width="1910" alt="image" src="https://user-images.githubusercontent.com/22209835/202381748-b5226390-653c-40f8-ac35-596e05ac3d99.png">
1. 特定エンドポイントの処理数や応答性能を確認するため、一旦 **Shipping**の Summary のページに戻り、下段中央 Top Endpoints の **GET /cities** のリンクを開きます。 
    <img width="1837" alt="image" src="https://user-images.githubusercontent.com/22209835/202391960-f889aa9f-f109-489e-9f1d-04d95c0ce3f6.png">
1. この **GET /cities** のみの処理数、エラー数、応答性能が表示されます
    <img width="1832" alt="image" src="https://user-images.githubusercontent.com/22209835/202392372-147dd250-e5d6-4ba6-8dd2-d9ab51825850.png">
1. このエンドポイントの **flow**タブを開くと、この処理の中で アクセスされている データベースのテーブル名が表示されます
    <img width="956" alt="image" src="https://user-images.githubusercontent.com/22209835/202383877-d85ca285-0e2f-4d82-acd7-e964e96bf8b4.png"> 
1. 呼ばれている **cities** のリンクをクリックして、**cities** のデータベース・テーブルのエンドポイントを開きます。  
※ このサービスは データベース名とテーブル名が同じなので分かりづらいですが、いまはエンドポイント（テーブル）レベルの ダッシュボードが開かれています。  
この下段右側には、このテーブルにアクセスしている SQLが 応答性能順、コール数順 に表示されています。
    <img width="1843" alt="image" src="https://user-images.githubusercontent.com/22209835/202384207-60184c86-42a4-4190-97a3-b4c000c36912.png">
1. この **cities** で **flow**タブを開くと、この cities テーブルを呼んでいる 処理が分かります。
    <img width="963" alt="image" src="https://user-images.githubusercontent.com/22209835/202384843-a24df207-b3ff-4bb7-abdd-13da1d854d74.png">
1. タイトル行にあるリンク から、一つ上のサービスレベル（データベース・レベル）の **cities** を開いてみてください。  
下段中央の Top Endpointsから、この **cities**データベースには **codes**とがあり、 **codes**の方が 非常に応答性能が良いことが分かります。
    <img width="964" alt="image" src="https://user-images.githubusercontent.com/22209835/202385351-f260e934-a01e-41a8-a049-1048e23e6996.png">

このように、さまざまなコンポーネントが リンクで柔軟につながっており、リンクを辿ることで、サービスやエンドポイント それぞれで 状況を把握いただくことが可能です。


### 4. 解析画面の利用
1. Instanaでは、多様な形で絞り込みを行い、要求を解析するための 解析画面 があります。メニューから 虫眼鏡アイコンの **Analytics**を選択ください。
    <img width="1903" alt="image" src="https://user-images.githubusercontent.com/22209835/202394607-1a2439e5-41e5-4b60-bf58-f27c5da30d4f.png">
1. ここでは、先ほどの**robotshop with frontend** に含まれる **catalgoue-demo**サービスの状況を、Endpoint Name ごとに確認します。 
   以下を参考に フィルターを設定してみてください。 Application>Name = Robotshop with Frontend **AND** Service>Name = catalogue-demo  
   グルーピング設定 Endpoint>Name
    <img width="1234" alt="image" src="https://user-images.githubusercontent.com/22209835/202397444-c4054f23-d13b-4cb2-8b7d-f14bc10bf76a.png">
1. 以下のように 出力が行われると思います。
    <img width="1825" alt="image" src="https://user-images.githubusercontent.com/22209835/202398538-030fba55-94d2-46ac-9936-2baf43e177f9.png">
1. 一番上の グループ GET /prodyct/{sku} 展開します。
　　　　　　　 <img width="1809" alt="image" src="https://user-images.githubusercontent.com/22209835/202398931-9ec43935-8bb8-411e-ad6c-dae34b1fe0ea.png">
1. さらに 左のフィルターで応答性能が 500ミリ秒を超えているものに絞り込みます。 （注：機能をご理解いただくためにやっているので、あまり解析自体には深い意味はありません。遅い応答を探しているくらいに理解ください。）
    <img width="1818" alt="image" src="https://user-images.githubusercontent.com/22209835/202399471-3fe0c089-f0bf-4ab7-b747-35fdbe19a5ba.png">
1. 絞り込まれた要求のなかで、赤になっているのは エラーとして返された応答、緑は正常応答です。問題判別は次の節でみるので、一旦、正常系応答を開いてみます。　　
処理のタイムラインで、どこで処理に時間がかかっているかが分かります。
    <img width="1835" alt="image" src="https://user-images.githubusercontent.com/22209835/202400364-e2ecc3b3-c12c-4951-ba29-4d9d0e25b38d.png">  
1. さらにページの下の方に遷移すると、どこのサービスのどこのエンド・ポイントでの処理で時間がかかっているか分かります。
    <img width="938" alt="image" src="https://user-images.githubusercontent.com/22209835/202400677-19a51c9b-58e0-4833-b662-2453669f3306.png">
**cart**から呼び出された**catalogue-demo**の処理に多くの時間がかかっていることが分かります。そこから呼び出された処理は短時間で終わっていますので、処理が遅かった理由を探すためには、この**catalogude-demo**でcommand を発行するまでに、なにをやっていたかを調べる形になります。正常時でエラーも出ていない場合は、Instanaではさらなる深堀りは難しいので、別途業務ログなどをより深く掘り下げて調べる必要があります。

---
### 5. エラーとなった要求の状況把握
1. いまいちど、4で調べた フィルター条件に戻り、今度はエラーとなっていた 要求を確認してみます。
    <img width="1600" alt="image" src="https://user-images.githubusercontent.com/22209835/202402599-4701410f-f944-456c-8aae-43f608d86379.png">
1. 同じように タイムラインが表示されますが、エラーとなった要求には 赤い！のマークがついています。
    <img width="1606" alt="image" src="https://user-images.githubusercontent.com/22209835/202402925-72f0bac3-30a9-4e02-bdd3-51b128f50b10.png">
1. ページを下に下り、どこのサービスのどこのエンド・ポイントでの処理で時間がかかっているか分かります。
このシーケンス図を見ていくと、一番下の 赤色の逆三角マーク にフォーカスを当てると　”Error occured during fetching discount from DB: Unable to acquire JDBC Connection”とエラー・メッセージが出ており、最後の **discountdb** に 接続 CONNECT しようとしてエラーとなったことが分かります。また、それを契機に呼び出し元に、それぞれエラーを返していることが分かります。　　
    <img width="1282" alt="image" src="https://user-images.githubusercontent.com/22209835/202403995-524b6d5d-fe03-4c6f-ad28-cd858772187f.png">
1. 実際には、原因追及のために、このdiscountdbが なぜ接続を受け付けなかったか調査することになり、**discountdb** をクリックして、 Infrastructure Issue＆Changes でなにかリリースなどしていないかなど確認することになります。ここになにも出ていない場合には、ミドルウェア側のログの調査が必要になります。
    <img width="1830" alt="image" src="https://user-images.githubusercontent.com/22209835/202405087-26e60797-22be-4950-b06f-cc5e07a73b88.png">

### 6. その他のエラー要求の特定方法
1. 先ほどは 解析画面のなかで、(事前に設定していた）時間の絞り込みと、アプリケーションとサービスを絞り込んで、応答が遅くエラーとなっていた処理を見つけました。  
実際は これまで見てきたダッシュボードの上段中央に、エラーが発生している要求を示すグラフがあったので、各サービス、各エンドポイントにおいて、エラーの要求を早期に見つけることができます。　　
エラーを示すグラフに フォーカスを当てて 虫眼鏡マークを選択することで、エラーとなった要求の解析画面に飛びます。  
ここでは 指定時間後半にある エラー要求をみてみましょう。  
    <img width="1833" alt="image" src="https://user-images.githubusercontent.com/22209835/202406846-7593a2a5-a5fe-4043-8925-7437b33a3df0.png">
1. エラー画面にフォーカスを当てて飛んだ場合には、自動的に Call>Erroneous is true(エラーとなった要求）のフィルターが設定されており、エラー要求だけを探すことが可能です（自分で設定もできます）。
    <img width="973" alt="image" src="https://user-images.githubusercontent.com/22209835/202408137-36a1de85-c55c-4269-b986-08b589e48652.png">
1. ここでは **ratings** サービスで発生したエラーをみてみましょう。一番上のリンクを開きます。
    <img width="1604" alt="image" src="https://user-images.githubusercontent.com/22209835/202407387-231afb49-ef18-4b20-900e-b1b89733095a.png">
1. このエラー要求の呼び出しシーケンスが確認できます。
    <img width="1836" alt="image" src="https://user-images.githubusercontent.com/22209835/202408435-b95d510d-0357-402e-8506-f588ef1cbfc6.png">
1. ページを下にくだり、要求の解析画面をみると、GET /find/RD-10 という要求の処理中に、NullPointerExceptionが返されていることが分かります。状況は分かりましたので、ここからの根本原因追及は業務ログを追うことになります。
    <img width="1500" alt="image" src="https://user-images.githubusercontent.com/22209835/202409159-c5368c6c-1d2f-4b05-9209-3fab2bbf71f1.png">

ここまでで、サーバー側のマイクロサービスの挙動を理解するための**Applications**の確認は終了です。  
次に、ブラウザやモバイル・アプリケーションなど、エンドユーザー側の挙動をみる [WebSites & MobileApps](https://github.com/ICpTrial/InstanaSandbox/blob/main/WebSites%26MobileApps.md)をみていきます。
