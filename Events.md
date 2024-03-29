## Events  

最後に イベントをみていきましょう。  
Instanaは、サービスの正常性を管理するため、各センサーのゴールデン・シグナル（トランザクション数、応答性能、エラー率など）に、機械学習を適用しています。  
応答性能の急激な低下や悪化、エラー率の急増など、ユーザーに影響を与えている通常の振る舞いと異なる状況を検知し、自動的に”インシデント"としてイベントを生成します。これにより、単純なしきい値監視では検知できない問題も拾っていくことできます。  
また、イベント通知時には、これまで見てきたようにサービスの前後上下のサービスのコンテキストを理解していますので、関連コンポーネントで発生している問題もあわせ、通知をあげます。
それではみていきましょう。
___

1. Eventsを開きます。  
色がついているイベントはまだ解消されていない課題、グレーアウトされているイベントはすでに問題自体は解消されている課題です。　　
タイミングによっては、グレーの解消された課題しかない場合もありますので、その場合は そちらを見てみてください。
![image](https://user-images.githubusercontent.com/22209835/114342349-ad4f7f00-9b96-11eb-86f0-d501f9d6c273.png)
1. ここではわかりやすいよう、右上の**Last hour**などの表示時間のボタンをクリックし、時間を絞り込んでいます。  
一番上のトリガーとなっているイベントは eum-frontendサービスでのエラー数の急増です。その他、いくつかのサービスで、エラー数急増が検知されています。
![image](https://user-images.githubusercontent.com/22209835/114342274-885b0c00-9b96-11eb-9705-d593ee60f723.png)
1. 一番上の eum-frontendサービスのイベント通知を見ていきましょう。  
ここで、トリガーとなったイベント **Trigering Events**は、eum-frontendサービスでのエラー率急増です。
![image](https://user-images.githubusercontent.com/22209835/114342389-bd675e80-9b96-11eb-88cc-26c4f493b831.png)
1. スクロールダウンしていくと、トリガーとなったイベントだけでなく、あわせて関連するコンポーネントでのイベントの情報が、**Related Events**として、時系列で提示されています。
![image](https://user-images.githubusercontent.com/22209835/114342452-d3751f00-9b96-11eb-8999-81a7090018a6.png)
ここでは、dockerコンテナで稼働する**discount**サービスがオンライン→オフライン→オンラインとなっており、サービスが再起動されたことが推測されます。また、それが discountサービスで検知されてるエラー率の急増につながっていますので、これが原因となっていることが想定されます。 
1. discount サービスの リンクをクリックして、discount のダッシュボードを開きます。左下のInfrastructure Issues & Changes（基盤の問題と変更）を確認します。ここで変更が起きている領域をマウスで選択し、 View Events で詳細を確認しましょう。  
![image](https://user-images.githubusercontent.com/22209835/189817211-3e97fd34-016b-44eb-b0f5-2b54d8cf9fea.png)  
1. 発生した基盤的な変化が記録されていますので、こちらで時系列を追ってなにが起きていたかを確認することが可能です。各イベントを開くと、各サービスのメトリックやダッシュボードにアクセスすることが可能です。  
![image](https://user-images.githubusercontent.com/22209835/189817134-6b68a5d5-5816-46c8-9ef2-70b7f5c2b03b.png)

このように依存関係のある周辺サービスまで含めてイベントが通知されますので、エラー通知を受けて、各サーバーに入り、関連するサービスの状況をログから集めて調査を行う従来の監視の仕組みに比べ、よりスピーディに根本原因へとたどりつくことが期待されます。 
___
以上で、 Instanaのサンドボックを利用したハンズオンは終了です。お疲れさまでした。  
  
いかがでしたでしょうか？従来の基盤的なモニタリングと違い、実際の問題判別やアプリケーションの改善に繋げられるデータが多く可視化され、そして有機的に連携されていたのではないでしょうか？  
さらに一歩検証を進めて、ご自身のアプリケーション環境がどのように見えるかを試したい場合、[こちらのサイト](https://www.instana.com/getting-started-with-apm/)の**Free Trial**ボタンから２週間の無償PoCを申し込むことが可能です。ぜひ、試してみてください。
