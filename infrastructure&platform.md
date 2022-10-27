## ダッシュボード
Play with Instana を開くと、以下のような画面が表示されます。  
エージェントを追加構成することができない、変更ができないなどをのぞけば、実際のInstanaと同様の画面です。  
製品ではコンソールは日本語で提供されています（日本語だけでなく、英語、中国語（繁体、簡体）など数カ国語で提供されています）。  
英語のガイド(Get Started)が左下に表示されていますので、そちらをやって頂いてもいいですが、一旦閉じておきましょう。  
![image](https://user-images.githubusercontent.com/22209835/114136663-0b395800-9946-11eb-922d-b9fba5781ee4.png)
  
左のメニューにあるように Instanaでは、Infrastructure から、Platform、アプリケーション さらには Web Site & Mobile Apps (エンドユーザー・モニタリング）まで多様な環境を見ていくことが可能です。
![image](https://user-images.githubusercontent.com/22209835/114136972-7aaf4780-9946-11eb-8049-dd72def3e636.png)

このサンドボック環境で IBM Instana Observability を、順に見ていきましょう。  
まず 取得した各種メトリックが統合されている Infrastructure & Platform の足回りから見ていきます。  
なお、このサンドボックス環境は実際にバックエンドで動いていて、擬似的に問題も発生させている環境ですので、開いたタイミングによって 表示される内容や発生するエラーは異なりますので、ご留意ください。

---

## Infrastructure 
1. インフラストラクチャでは、エージェントが導入されている各ホスト・ノードが 一元化されて把握できるようになっています。  
エージェントには、ゾーンを関連づけ、カスタマイズすることもできるので、クラウドのゾーンだけでなく、東京データセンター、大阪災体データセンターなど、自由に関連付けて管理することが可能です。
　　<img width="1909" alt="image" src="https://user-images.githubusercontent.com/22209835/189789923-e0d18859-31e8-44e3-b1d2-9f5f1572c46c.png">

1. 上の **Comparison Table** をクリックすると、一覧表示で、ホストや各種コンテナーをリストアップできます。再び **Map**に戻ります。　　
　　<img width="1908" alt="image" src="https://user-images.githubusercontent.com/22209835/189789980-88622203-64c3-4b16-a518-27c03932e659.png">

1. 色が付いているブロックがあれば、そこは問題が発生している環境です（環境のタイミングによって、存在するとはかぎりません）。例えば、上の黄色のブロックは TCP再送が永久に繰り返されてノード自体の問題が疑われるノードです。
  ![image](https://user-images.githubusercontent.com/22209835/114138096-168d8300-9948-11eb-9ce3-5b17856c369f.png)



1. **hmadison** や **k8sdemo** は、Kubernetes環境のノードです。クリックすると、そのノードで検知されているテクノロジーのスタックが表示されます。  
左にはそのノードの詳細が表示されます。ホスト名から分かるように gkeで稼働するKubernetesの WorkerNodeです。
![image](https://user-images.githubusercontent.com/22209835/114138304-68cea400-9948-11eb-9692-e26f9c429d62.png)
1. ノード情報の下の方には、そのノードで稼働する各種サービスのスタックが表示されています。それそれリンクになっていますので、検知されたサービスのダッシュボードへと飛ぶことも可能です。
![image](https://user-images.githubusercontent.com/22209835/114138551-c4992d00-9948-11eb-92b3-fa60ffe25499.png)
1. ノード情報の上の方にある 緑色の **Open Dashboard** の画面を開きます。ノードのリソースの詳細情報が確認できます。  
CPUやメモリの利用量から、Open Files数、File Systemの情報、ネットワークのアクティビティなど、基盤的な情報を確認することができます。メトリックは１秒単位の高精細なデータで、スパイクを見逃しません。
![image](https://user-images.githubusercontent.com/22209835/114138732-032ee780-9949-11eb-8091-28005f6e4a71.png)
1. 上の **Stack**タブをクリックすると、このノードで稼働している アプリケーションやKubernetesのスタックの情報が確認できます。
![image](https://user-images.githubusercontent.com/22209835/114139481-142c2880-994a-11eb-8bd1-541edfcc335a.png)

---
## Platform
1. つぎにアプリケーションが稼働するプラットフォームを見ていきましょう。KubernetesやCloudFoundry、この環境には表示されていませんが vSphereや PowerVM の情報も見ていくことが可能です。
![image](https://user-images.githubusercontent.com/22209835/114139901-8f8dda00-994a-11eb-9b09-bde2f587499c.png)
1. ひとつ定義されている public-demo-cluster が確認できます。右端のHealthはグリーンで大きな問題はないようですね。  
public-demo-cluster のリンクをクリックして、見ていきましょう。
![image](https://user-images.githubusercontent.com/22209835/114140147-dda2dd80-994a-11eb-9223-96d9965d9350.png)

1. 各クラスター全体のダッシュボードが開きます。  
CPUやメモリーなどのリソース状況、利用状況上位のノードや名前空間のリストがあります。
![image](https://user-images.githubusercontent.com/22209835/114326924-f80ad000-9b71-11eb-9e7c-ed8fcf86d5c1.png)
1. 先程と同様、メニューの **Stack**をクリックすると、このクラスターに関係する アプリケーションやInfrastructure の情報がリストされて表示されます。
![image](https://user-images.githubusercontent.com/22209835/114327073-7d8e8000-9b72-11eb-8b3b-c447edcb0f7e.png)
1. Kubernetesの各種リソースがタブとして整理されていますので、確認してみてください。  
とくに Pod のタブでは、リソースの Requests/Limitsの値をグラフィカルに表示することもできますので、どの名前空間のPodがリソースを消費する設定となっているかなど確認することができます。
![image](https://user-images.githubusercontent.com/22209835/114327147-d1996480-9b72-11eb-9f7e-c222c07bba7d.png)
1. 気になる Podがあれば、その Podの情報をクリックすることで、Podのダッシュボードに移動し、実際のリソース利用状況などを確認できます。
![image](https://user-images.githubusercontent.com/22209835/114327227-23da8580-9b73-11eb-87eb-902bf9fe4d4b.png)

---
【参考】  
このPlayWithInstanaのサンドボックス環境には含まれていませんが、製品版では Open Betaのステータスで Kubernetesの各コンテナの出力するログ・メッセージをInstanaで集約表示する Kubernetes Logging 機能を提供しています。
クラスター、名前空間、Pod、コンテナーの各レベルにおいて、ログ・メッセージを表示することが可能です。また解析機能を使って、サービスごとにまとめて表示するなど、Kubernetes/OpenShift環境での問題判別が加速する機能ですね。GAして早くお届けできることを楽しみにしています。
<img width="2043" alt="image" src="https://user-images.githubusercontent.com/22209835/189812350-526eac91-67ff-44f6-9c50-b1b5e2105c88.png">
<img width="1993" alt="image" src="https://user-images.githubusercontent.com/22209835/189812434-586521f3-cd69-451f-a656-0eef6595dc6a.png">

---
これで **Infrastructure & Platform** の確認は終わりです。  
様々な環境に関わるリソース情報が整理され、それぞれ関連付けられて、コンソールに統合されていることが理解頂けたと思います。  
次にトレースとログの解析結果を可視化している [Application](https://github.com/ICpTrial/InstanaSandbox/blob/main/Applications.md) を見ていきたいと思います。

