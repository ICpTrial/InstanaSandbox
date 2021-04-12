## WebSites & Mobile Apps

Instana では、ブラウザやモバイル・アプリケーションなど、エンドユーザー側の振る舞いを理解するための、エンドユーザー・モニタリングの機能も提供しています。  
ブラウザアプリケーション（Web画面）の場合は、JavaScriptのエージェントをコードのヘッダーに埋め込みます（くわしくは[こちら](https://www.instana.com/docs/website_monitoring/#installation)）。  
モバイル・アプリケーションの場合は、各環境向けのエージェントが用意されています。（くわしくは[こちら](https://www.instana.com/docs/mobile_app_monitoring/)）  

---
### WebSitesのダッシュボード
1. Instanaの画面から、**WebSites&MobileApps**を開いて、見ていきましょう。  
なおこのサンドボックスの環境には、モバイル・アプリケーションのアプリケーションは用意されていませんので、ここではWebSiteのみをみていきます。    
![image](https://user-images.githubusercontent.com/22209835/114339724-d9680180-9b90-11eb-86d7-de14ab79ecab.png)
1. 定義されている **robotshop**を開きます。
![image](https://user-images.githubusercontent.com/22209835/114354250-eb559e80-9ba8-11eb-9258-502fe5675bd3.png)
WebSitesモニタリングでは、各ブラウザに埋め込まれたエージェントから、直接Instanaのインスタンスにパフォーマンス状況が送信されてます。
[注] このサンドボックスでは、Instanaの機能をお見せするために個別ユーザーを特定できる情報まで送信していますが、デフォルトでは 個人を特定できる情報は送信されません。UserAPIを使用するよう管理者の構成が必要となります。  
WebSitesモニタリングで送信される情報については、[こちら](https://www.instana.com/docs/website_monitoring/faq/#what-are-you-doing-with-the-user-data-transmitted-to-instana)をご確認ください。

1. RoboShop のサイトのパフォーマンスのオーバービューが表示されます。ページビュー数やJavaScriptのエラー、ページのロード時間などが表示されています。
![image](https://user-images.githubusercontent.com/22209835/114340185-f5b86e00-9b91-11eb-8c4a-7fb958791cc8.png)
1. **Speed**のタブには、Webサイトの応答性能の詳細情報が表示されています。
![image](https://user-images.githubusercontent.com/22209835/114340337-4def7000-9b92-11eb-8783-3f5affec7814.png)
1. **Resources**のタブには、RobotShopサイトが読み込んでいる外部リソースのパフォーマンスが表示されています。
![image](https://user-images.githubusercontent.com/22209835/114340420-7d05e180-9b92-11eb-939b-b7bfd449c8be.png)
1. その他のタブについて、確認してみてください。またタブの上のフィルターを利用すると、ブラウザーの種類やOSで情報を絞り込むことが可能です。

### WebSitesの問題判別
1. **Summary**のページに戻ります。
Applicatiosnのページと同様、エラーにフォーカスを当てて、詳細を確認します。
![image](https://user-images.githubusercontent.com/22209835/114340607-ef76c180-9b92-11eb-8cf2-34c057a1b5df.png)
1. ここでは、問題が一つだけのようですので、そこをクリックして、詳細画面を確認します。
![image](https://user-images.githubusercontent.com/22209835/114340638-fdc4dd80-9b92-11eb-86da-953437a86baf.png)
1. 問題が発生している JavaScript Ratings にフォーカスがあたっていますので、確認します。  
![image](https://user-images.githubusercontent.com/22209835/114340769-411f4c00-9b93-11eb-9877-478cf78ced2f.png)
1. ratings の JavaScriptのどの行で どんなエラーが返されているかが分かります。ここでは 1-5が許される値に6が入力され、エラーとなっていることが分かります。
![image](https://user-images.githubusercontent.com/22209835/114340851-6f9d2700-9b93-11eb-9d46-9ed484493d71.png)

1. なお、ブラウザから呼び出している Backendサービスがある場合には、以下のように **View Backend Trace**のボタンがあります。
![image](https://user-images.githubusercontent.com/22209835/114341027-ca368300-9b93-11eb-96fb-8c3a374317e0.png)
1. これをクリックすると、先程見てきたサーバー側の解析画面に飛ぶことができます。
![image](https://user-images.githubusercontent.com/22209835/114341141-07027a00-9b94-11eb-92c0-2462f7c4b04e.png)

---
ここまでで、**WebSites&MobileApps**のハンズオンは終了です。最後は、[Events](https://github.com/ICpTrial/InstanaSandbox/blob/main/Events.md)を見ていきましょう。


