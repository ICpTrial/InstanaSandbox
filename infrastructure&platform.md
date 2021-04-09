### ダッシュボード
Play with Instana を開くと、以下のような画面が表示されます。エージェントを追加構成することができない、変更ができないなどをのぞけば、実際のInstanaと同様の画面です。  
英語のガイドも右下に表示されていますので、そちらをやって頂いてもいいですが、一旦閉じておきましょう。  
![image](https://user-images.githubusercontent.com/22209835/114136663-0b395800-9946-11eb-922d-b9fba5781ee4.png)
  
左のメニューにあるように Instanaでは、Infrastructure から、Platform、アプリケーション さらには Web Site & Mobile Apps (エンドユーザー・モニタリング）まで多様な環境を見ていくことが可能です。
![image](https://user-images.githubusercontent.com/22209835/114136972-7aaf4780-9946-11eb-8049-dd72def3e636.png)

このサンドボック環境で Instana で、順に見ていきましょう。まず Infrastructure & Platform の足回りから見ていきます。  
なお、このサンドボックス環境は実際にバックエンドで動いていて、擬似的に問題も発生させている環境ですので、開いたタイミングによって 表示される内容は異なりますので、ご留意ください。

---

### Infrastructure 
インフラストラクチャでは、エージェントが導入されている各ホストノードが 一元化されて把握できるようになっています。  
エージェント導入時には、ゾーンを関連づけることができるので、クラウドのゾーンだけでなく、東京データセンター、大阪災体データセンターなど、自由に関連付けて管理することが可能です・
![image](https://user-images.githubusercontent.com/22209835/114137453-37a1a400-9947-11eb-9b00-7e66700eca23.png)
上の **Comparison Table** をクリックすると、一覧表示で、ホストや各種コンテナーをリストアップできます。再び **Map**に戻ります。
![image](https://user-images.githubusercontent.com/22209835/114139190-b0a1fb00-9949-11eb-917c-580192ddfffb.png)

色が付いているブロックがあれば、そこは問題が発生している環境です。例えば、上の黄色のブロックは TCP再送が永久に繰り返されてノード自体の問題が疑われるノードです。
![image](https://user-images.githubusercontent.com/22209835/114138096-168d8300-9948-11eb-9ce3-5b17856c369f.png)



**k8sdemo**は、Kubernetes環境のノードです。クリックすると、そのノードで検知されているテクノロジーのスタックが表示されます。　　
左にはそのノードの詳細が表示されます。ホスト名から gkeで稼働するKubernetesの WorkerNodeであることが分かります。
![image](https://user-images.githubusercontent.com/22209835/114138304-68cea400-9948-11eb-9692-e26f9c429d62.png)
ノード情報の下の方には、そのノードで稼働する各種サービスのスタックが表示されています。それそれリンクになっていますので、検知されたサービスのダッシュボードへと飛ぶことも可能です。
![image](https://user-images.githubusercontent.com/22209835/114138551-c4992d00-9948-11eb-92b3-fa60ffe25499.png)
ノード情報の上の方にある 緑色の **Open Dashboard** の画面を開きます。ノードのリソースの詳細情報が確認できます。  
CPUやメモリの利用量から、Open Files数、File Systemの情報、ネットワークのアクティビティなど、基盤的な情報を確認することができます。
![image](https://user-images.githubusercontent.com/22209835/114138732-032ee780-9949-11eb-8091-28005f6e4a71.png)



---
