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
