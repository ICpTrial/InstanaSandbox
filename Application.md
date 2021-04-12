## Applications

次に 各ホスト・ノードや Kubernertes/CloudFoundryなどで稼働する アプリケーションについて、見ていきます。
Instanaの右のメニューから、**Applications**のアイコンをクリックしてください。
![image](https://user-images.githubusercontent.com/22209835/114327991-3efac480-9b76-11eb-98a9-5bd536f758ac.png)

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
RobotShop を構成するマイクロサービス全体のダッシュボードが開きます。一番上には、ゴールデン・シグナル（コール数、応答性能、エラー率）およびその履歴が表示されています。  
下には関連する基盤で発生した基盤の問題と変更の履歴、各ゴールデンシグナルでのサービスのランキング、および処理時間が表示されています。
各ゴールデンシグナルでは、応答が悪化しているものやエラー数が多いサービスを確認できますので、注視が必要なものが分かります。  
![image](https://user-images.githubusercontent.com/22209835/114328371-58e8d700-9b77-11eb-8f87-efd864dd792c.png)
次に **Dependency**のタブを開きましょう。ここでは RobotShopを構成する様々なサービスの依存関係（コンテキスト）が可視化されています。動いている一つ一つの点が サービス間の要求です。  
Instanaは、これらの要求を解析することで、依存関係をダイナミックに可視化しています。
![image](https://user-images.githubusercontent.com/22209835/114328391-74ec7880-9b77-11eb-931e-dafc0529b079.png)
ひとつのサービスにカーソルを合わせて見ましょう。そのサービスと依存関係のあるサービスのみにフォーカスが当たります。
![image](https://user-images.githubusercontent.com/22209835/114328413-83d32b00-9b77-11eb-82cf-ceed09b80092.png)
左上の メニューを選択することで、応答性能が遅いサービスのアイコンを大きくしたり、要求数の大きいサービスを大きくしたり、わかりやすく可視化できますので、いろいろ触ってみてください。
![image](https://user-images.githubusercontent.com/22209835/114328451-a49b8080-9b77-11eb-8b8e-ee7c427bbd11.png)
