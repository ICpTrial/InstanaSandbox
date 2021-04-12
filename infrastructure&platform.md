## ダッシュボード
Play with Instana を開くと、以下のような画面が表示されます。エージェントを追加構成することができない、変更ができないなどをのぞけば、実際のInstanaと同様の画面です。  
英語のガイドも右下に表示されていますので、そちらをやって頂いてもいいですが、一旦閉じておきましょう。  
![image](https://user-images.githubusercontent.com/22209835/114136663-0b395800-9946-11eb-922d-b9fba5781ee4.png)
  
左のメニューにあるように Instanaでは、Infrastructure から、Platform、アプリケーション さらには Web Site & Mobile Apps (エンドユーザー・モニタリング）まで多様な環境を見ていくことが可能です。
![image](https://user-images.githubusercontent.com/22209835/114136972-7aaf4780-9946-11eb-8049-dd72def3e636.png)

このサンドボック環境で Instana で、順に見ていきましょう。まず Infrastructure & Platform の足回りから見ていきます。  
なお、このサンドボックス環境は実際にバックエンドで動いていて、擬似的に問題も発生させている環境ですので、開いたタイミングによって 表示される内容は異なりますので、ご留意ください。

---

## Infrastructure 
インフラストラクチャでは、エージェントが導入されている各ホストノードが 一元化されて把握できるようになっています。  
エージェント導入時には、ゾーンを関連づけることができるので、クラウドのゾーンだけでなく、東京データセンター、大阪災体データセンターなど、自由に関連付けて管理することが可能です・
![image](https://user-images.githubusercontent.com/22209835/114137453-37a1a400-9947-11eb-9b00-7e66700eca23.png)
上の **Comparison Table** をクリックすると、一覧表示で、ホストや各種コンテナーをリストアップできます。再び **Map**に戻ります。
![image](https://user-images.githubusercontent.com/22209835/114139190-b0a1fb00-9949-11eb-917c-580192ddfffb.png)

色が付いているブロックがあれば、そこは問題が発生している環境です（環境のタイミングによって、存在するとはかぎりません）。例えば、上の黄色のブロックは TCP再送が永久に繰り返されてノード自体の問題が疑われるノードです。
![image](https://user-images.githubusercontent.com/22209835/114138096-168d8300-9948-11eb-9ce3-5b17856c369f.png)



**k8sdemo**は、Kubernetes環境のノードです。クリックすると、そのノードで検知されているテクノロジーのスタックが表示されます。　　
左にはそのノードの詳細が表示されます。ホスト名から gkeで稼働するKubernetesの WorkerNodeであることが分かります。
![image](https://user-images.githubusercontent.com/22209835/114138304-68cea400-9948-11eb-9692-e26f9c429d62.png)
ノード情報の下の方には、そのノードで稼働する各種サービスのスタックが表示されています。それそれリンクになっていますので、検知されたサービスのダッシュボードへと飛ぶことも可能です。
![image](https://user-images.githubusercontent.com/22209835/114138551-c4992d00-9948-11eb-92b3-fa60ffe25499.png)
ノード情報の上の方にある 緑色の **Open Dashboard** の画面を開きます。ノードのリソースの詳細情報が確認できます。  
CPUやメモリの利用量から、Open Files数、File Systemの情報、ネットワークのアクティビティなど、基盤的な情報を確認することができます。
![image](https://user-images.githubusercontent.com/22209835/114138732-032ee780-9949-11eb-8091-28005f6e4a71.png)
上の **Stack**タブをクリックすると、このノードで稼働している アプリケーションやKubernetesのスタックの情報が確認できます。
![image](https://user-images.githubusercontent.com/22209835/114139481-142c2880-994a-11eb-8bd1-541edfcc335a.png)

---
## Platform
つぎにアプリケーションが稼働するプラットフォームを見ていきましょう。KubernetesやCloudFoundry、この環境には表示されていませんが vSphere の情報も見ていくことが可能です。
![image](https://user-images.githubusercontent.com/22209835/114139901-8f8dda00-994a-11eb-9b09-bde2f587499c.png)
ひとつ定義されている public-demo-cluster が確認できます。右端のHealthはグリーンで大きな問題はないようですね。  
public-demo-cluster のリンクをクリックして、見ていきましょう。
![image](https://user-images.githubusercontent.com/22209835/114140147-dda2dd80-994a-11eb-9223-96d9965d9350.png)

各クラスター全体のダッシュボードが開きます。  
CPUやメモリーなどのリソース状況、利用状況上位のノードや名前空間のリストがあります。
![image](https://user-images.githubusercontent.com/22209835/114326924-f80ad000-9b71-11eb-9e7c-ed8fcf86d5c1.png)
先程と同様、メニューの **Stack**をクリックすると、このクラスターに関係する アプリケーションやInfrastructure の情報がリストされて表示されます。
![image](https://user-images.githubusercontent.com/22209835/114327073-7d8e8000-9b72-11eb-8b3b-c447edcb0f7e.png)
Kubernetesの各種リソースがタブとして整理されていますので、確認してみてください。  
とくに Pod のタブでは、リソースの Requests/Limitsの値をグラフィカルに表示することもできますので、どの名前空間のPodがリソースを消費する設定となっているかなど確認することができます。
![image](https://user-images.githubusercontent.com/22209835/114327147-d1996480-9b72-11eb-9f7e-c222c07bba7d.png)
気になる Podがあれば、その Podの情報をクリックすることで、Podのダッシュボードに移動し、実際のリソース利用状況などを確認できます。
![image](https://user-images.githubusercontent.com/22209835/114327227-23da8580-9b73-11eb-87eb-902bf9fe4d4b.png)

---
これで **Infrastructure & Platform** の確認は終わりです。  
様々な環境に関わるリソース情報が整理され、それぞれ関連付けられて、コンソールに統合されていることが理解頂けたと思います。  
次に [Application](https://github.com/ICpTrial/InstanaSandbox/blob/main/Application.md) を見ていきたいと思います。

