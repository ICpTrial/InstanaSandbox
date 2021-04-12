## Applications

次に 各ホスト・ノードや Kubernertes/CloudFoundryなどで稼働する アプリケーションについて、見ていきます。
Instanaの右のメニューから、**Applications**のアイコンをクリックしてください。
![image](https://user-images.githubusercontent.com/22209835/114327991-3efac480-9b76-11eb-98a9-5bd536f758ac.png)

---
### マイクロサービスの可視化

**Applications**と **Services**の２つのタブがありますが、まずは**Services**から見ていきます。  
ここには、Instanaのエージェントが検知したアプリケーション・サービスがリストされています。  
各行に、個々のサービスのテクノロジーやそのタイプ（HTTPやDATABASE, MESSAGINGなど）、および 各サービスのゴールデン・シグナル（コール数、応答性能、エラー率）が表示されています。  
![image](https://user-images.githubusercontent.com/22209835/114327943-1672ca80-9b76-11eb-8d12-07546767428d.png)

これらのゴールデン・シグナルに対して、機械学習を適用していますので、コール数の急減や応答性能の遅延、エラー率の急増といったイベントを検知して、ヘルス状況を表示しています。  
![image](https://user-images.githubusercontent.com/22209835/114327953-212d5f80-9b76-11eb-95d0-15725d6e37d0.png)
これらの問題の解析は、いったん後にして、もう少し画面を見ていきましょう。

つぎに **Applications**のタブを開きましょう。
さきほどの Services タブは、テクノロジーのリストであり、業務ユーザーにとっては意味をなしません。検知されたテクノロージを、ユーザーにとって意味のある体系に整理するビューが**Applications**です。  
たとえば、Payment Serviceに特化したダッシュボードや、フロントエンド含めRobotShop全体のサービスを確認するビューです。また、DB管理者には、稼働するDatabaseすべてを含むビューが必要かもしません。  
このアプリケーション・タブは、ユーザーにとって管理しやすいよう、自由に編集が可能です。
![image](https://user-images.githubusercontent.com/22209835/114328104-8d0fc800-9b76-11eb-8d67-ee44778b3a52.png)

**robot-shop with frontend**のApplicaionsビューをクリックしましょう。  
RobotShop を構成するマイクロサービス全体の**Summary**のダッシュボードが開きます。一番上には、ゴールデン・シグナル（コール数、応答性能、エラー率）およびその履歴が表示されています。  
下には関連する基盤で発生した基盤の問題と変更の履歴、各ゴールデンシグナルでのサービスのランキング、および処理時間が表示されています。
各ゴールデンシグナルでは、応答が悪化しているものやエラー数が多いサービスを確認できますので、注視が必要なものが分かります。  
![image](https://user-images.githubusercontent.com/22209835/114328371-58e8d700-9b77-11eb-8f87-efd864dd792c.png)
次に **Dependency**のタブを開きましょう。ここでは RobotShopを構成する様々なサービスの依存関係（コンテキスト）が可視化されています。動いている一つ一つの点が サービス間の要求です。  
Instanaは、これらの要求を解析することで、依存関係をダイナミックに可視化しています。もし色が付いているサービスがあれば、それは問題が発生しているサービスです。
![image](https://user-images.githubusercontent.com/22209835/114328391-74ec7880-9b77-11eb-931e-dafc0529b079.png)
ひとつのサービスにカーソルを合わせて見ましょう。そのサービスと依存関係のあるサービスのみにフォーカスが当たります。
![image](https://user-images.githubusercontent.com/22209835/114328413-83d32b00-9b77-11eb-82cf-ceed09b80092.png)
左上の メニューを選択することで、応答性能が遅いサービスのアイコンを大きくしたり、要求数の大きいサービスを大きくしたり、わかりやすく可視化できますので、いろいろ触ってみてください。　　
![image](https://user-images.githubusercontent.com/22209835/114328451-a49b8080-9b77-11eb-8b8e-ee7c427bbd11.png)
たとえば、Databaseのサービスを選んで、サービスのダッシュボードに移動してみましょう。  
どれでもいいですが、以下の例では、**cities**という MySQLのサービスを開きます。
![image](https://user-images.githubusercontent.com/22209835/114330307-62c10900-9b7c-11eb-846f-d84a3547b5a9.png)
開くと、citiesサービスの詳細が表示されています。右下には、応答時間がかかっているSQLが順に表示されています。
![image](https://user-images.githubusercontent.com/22209835/114330341-73717f00-9b7c-11eb-981b-2dacf702c549.png)
 
---
### アプリケーションの問題切り分け

**Summary**のダッシュボードに戻ります。
エラーとなっているコールがありますので、ここを確認していきましょう。  
![image](https://user-images.githubusercontent.com/22209835/114329793-3e186180-9b7b-11eb-9dd4-cd363cd1ee1a.png)
中央の エラーコール率のグラフの山を選択して、**View in Analyze**で解析画面で確認していきます。  
タイミングによって、起きているエラーは異なりますので、みなさんの画面で確認しているエラーを選択して開いて下さい。
![image](https://user-images.githubusercontent.com/22209835/114329771-2e008200-9b7b-11eb-8da1-58dab02b41c3.png)
アプリケーションを理解していれば、より具体的にアクションが採れるかもしれませんが、ここでは、一番エラー数の多い上の **eum-frontend**を選択します。  
タイミングによって、起きているエラーは異なりますので、環境に応じて 一番多いエラーを選択して開いて下さい。
![image](https://user-images.githubusercontent.com/22209835/114329840-5c7e5d00-9b7b-11eb-9926-f7f1f0cc29c1.png)
ここでは、エラーを返している **eum-frontend**の要求がリストされています。  
軒並み応答性能が5000ミリ秒を超えてエラーとなっているようですね。これらについて詳細を確認していきましょう。  
一番上のエラー要求をクリックして、要求の中身をみていきます。
![image](https://user-images.githubusercontent.com/22209835/114329872-699b4c00-9b7b-11eb-9e26-f49bb8836b59.png)
この `GET /zh_cn/shop`要求の詳細がわかります。中身を確認しながらスクロールダウンしてください。
![image](https://user-images.githubusercontent.com/22209835/114329913-7c158580-9b7b-11eb-8843-5767842cbb98.png)
タイムラインのビューでは、この要求に関連して実行された マイクロサービスの呼び出し関係が可視化されています。
![image](https://user-images.githubusercontent.com/22209835/114329938-8e8fbf00-9b7b-11eb-82b4-b0b2e79366ce.png)
さらにコールのビューまでいくと、各マイクロサービスの呼び出しの依存関係 呼び出し元と呼び出し先が確認できます。
![image](https://user-images.githubusercontent.com/22209835/114329959-a0716200-9b7b-11eb-8eaa-bd8b8fe06ecf.png)
マイクロサービスの一番下で、DATABASE（MySQLサービス）への CONNECT要求が5000ミリ秒でタイム・アウトし、エラーなっているのが分かります。
右のペーンには、エラーの内容と、問題が発生したコードのスタックトレースが表示されています。
![image](https://user-images.githubusercontent.com/22209835/114329998-b2eb9b80-9b7b-11eb-9412-ecda686ca624.png)
問題となっている MySQLサービスをクリックすると、当該時間帯に Offlineが検知されているのが分かります。
![image](https://user-images.githubusercontent.com/22209835/114330035-c8f95c00-9b7b-11eb-9618-9da6e087cea4.png)
このようなかたちで、エラー応答となったマイクロサービスの依存関係を解析した上で、問題の根本原因の分析へと絞り込んでいくことが可能です。

---
ここまでで、サーバー側のマイクロサービスの挙動を理解するための**Applications**の確認は終了です。  
次に、ブラウザやモバイル・アプリケーションなど、エンドユーザー側の挙動をみる [WebSites & Mobile](https://github.com/ICpTrial/InstanaSandbox/blob/main/WebSites%26Mobile)をみていきます。
