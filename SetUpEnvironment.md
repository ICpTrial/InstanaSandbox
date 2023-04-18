
この環境準備の手順は IBM社員にしか実行することができません。

1. Instana環境の払出し
    1. *TechZone* の環境から [Instana - self deploy on VSI](https://techzone.ibm.com/resource/61a67d13193bdb0018e6ce89) を払い出します

1. Instana監視環境の払出し
    1. *TechZone*　の環境から [IBM RedHat Openshift Kubernetes Service （ROKS Classic）](https://techzone.ibm.com/my/reservations/create/63dba55ccdd28a00178ba0cc ) を最小構成で払い出します
    3. 払い出されたら、OpenShift環境にCLIでログインし、以下のコマンドで Instana Agentを導入するための 名前空間を作成し、SCCの設定を行います
      ```
      oc new-project instana-agent  
      oc adm policy add-scc-to-user privileged -z instana-agent
      ```
    1. Instana-Agent Operator を Operatorカタログから導入ます
    1. Instana-Agent Operatorが正常に導入できたら、Instana Agent のインスタンスを作成します。YAML定義には作成した先ほど作成した Instana環境から必要な情報を確認し指定てください。
    1. 正常に導入できれば、以下の通り、inststana-agent 名前空間で podが `Running` ステータスで稼働します。
    
      ```
      ~ $ oc get pods -n instana-agent
      NAME                  READY   STATUS    RESTARTS   AGE　　　　
      instana-agent-597w9   1/1     Running   0          172m　　　　
      instana-agent-w925g   1/1     Running   0          172m　　　　
      instana-agent-xbcx4   1/1     Running   0          172m　　　　
      ```
      
    1. 以下のコマンドで、Agent のPod のログを参照し、正常に Instana バックエンドに接続できたことを確認します
      ```
      oc logs -f instana-agent-xxxxx -n instana-agent
      ```

1. Node.js などの環境の AutoTraceを有効化するために、 Instana Autotrace Webhookを helmで導入し構成します。
   ```
    helm install --create-namespace --namespace instana-autotrace-webhook instana-autotrace-webhook \
    >   --repo https://agents.instana.io/helm instana-autotrace-webhook \
    >   --set webhook.imagePullCredentials.password=qxxxxxxxxxxxxxxxw \
    >   --set openshift.enabled=true
    NAME: instana-autotrace-webhook
    LAST DEPLOYED: Mon Apr 17 18:02:11 2023
    NAMESPACE: instana-autotrace-webhook
    STATUS: deployed
    REVISION: 1
    TEST SUITE: None
    NOTES:
    The Instana AutoTrace WebHook is installed.

    It will automatically instrument:
      - Node.js, .NET Core, Ruby & Python applications via LD_PRELOAD

    Logs for the Instana AutoTrace WebHook are available via:

    kubectl logs -l app.kubernetes.io/name=instana-autotrace-webhook -n instana-autotrace-webhook
    ```
    ※ Instana Autotrace Webhookは、すでに稼働しているアプリケーションには有効とならないため、すでに稼働しているアプリケーションに対してInstana AutoTrace を設定するためには、Podを再起動してください。

1. Quote of The Day アプリケーションの払出し
    1. 監視対象のアプリケーションとして、払い出されたOpenShift環境に HELMで Quote of The Day を払出します
      * host の情報は環境によって異なるため、払い出した環境の情報を設定します
      * rokcCluster=true を定義します

    ```
    helm install qotd-chart qotd/qotd \
    >   --set host=itzroks-3100008gyq-cx7n24-4b4a324f027aea19c5cbc0c3275c4656-0000.us-south.containers.appdomain.cloud　\
    >   --set roksCluster=true 
    >   --create-namespace --namespace qotd
    NAME: qotd-chart
    LAST DEPLOYED: Mon Apr 17 16:28:50 2023
    NAMESPACE: qotd
    STATUS: deployed
    REVISION: 1
    TEST SUITE: None
    NOTES:
    The QotD application code is running in the qotd namespace.  The route
    can be used to access the main application UI is

    http://qotd-web-qotd.itzroks-3100008gyq-cx7n24-4b4a324f027aea19c5cbc0c3275c4656-0000.us-south.containers.appdomain.cloud ; echo

    The Load Generator and Anomaly Generator are deployed to the qotd-load namespace,
    and can be accessed with

    http://qotd-usecase-qotd-load.itzroks-3100008gyq-cx7n24-4b4a324f027aea19c5cbc0c3275c4656-0000.us-south.containers.appdomain.cloud
    
    
    Happy quoting!
    ```
 
 1. Instana Automation Webhook　が　正常に稼働ししていることを、Pod のログから確認します。
    ```
    ~ $ oc get pods -n instana-autotrace-webhook
    NAME                                         READY   STATUS    RESTARTS   AGE
    instana-autotrace-webhook-5687b477d7-h9zk5   1/1     Running   0          14h
    ~ $ oc logs -f instana-autotrace-webhook-5687b477d7-h9zk5 -n instana-autotrace-webhook
    ・・・ (略）　
    09:02:24.056 INFO  |- o.s.b.a.e.web.EndpointLinksResolver: Exposing 1 endpoint(s) beneath base path '/actuator'
    09:02:25.813 INFO  |- o.s.b.w.e.netty.NettyWebServer: Netty started on port 42650
    09:02:25.898 INFO  |- c.i.k.a.w.AutotraceMutatingWebhookApplication: Started AutotraceMutatingWebhookApplication in 8.042 seconds (process running for 10.327)
    09:02:45.059 INFO  |- DefaultPodSpecTransformation: Configuration is use libinstana init
    09:02:45.093 INFO  |- DefaultPodSpecTransformation: Configuration is use autotrace nodejs
    09:02:45.336 INFO  |- [AdmissionReview 57935dc9-1eb2-4ce9-8adb-58ea0f9f8ec3] Applied transformation DefaultDeploymentTransformation to the Deployment 'calico-typha/calico-system'
    09:02:45.867 INFO  |- DefaultPodSpecTransformation: Configuration is use libinstana init
    09:02:45.868 INFO  |- DefaultPodSpecTransformation: Configuration is use autotrace nodejs
    09:02:46.622 INFO  |- [AdmissionReview f8ae1f92-5d1b-47c0-84e3-3d5a86975335] Applied transformation DefaultDaemonSetTransformation to the DaemonSet 'calico-node/calico-system'
    09:02:47.091 INFO  |- DefaultPodSpecTransformation: Configuration is use libinstana init
    09:02:47.091 INFO  |- DefaultPodSpecTransformation: Configuration is use autotrace nodejs
    09:02:47.106 INFO  |- [AdmissionReview 60ad7d06-dc3c-4530-a8ee-dbf83e40318d] Applied transformation DefaultDeploymentTransformation to the Deployment 'calico-kube-controllers/calico-system'
    09:04:25.921 INFO  |- DefaultPodSpecTransformation: Configuration is use libinstana init
    09:04:25.925 INFO  |- DefaultPodSpecTransformation: Configuration is use autotrace nodejs
    09:04:25.951 INFO  |- [AdmissionReview 55e6ae9c-5133-4e58-88d8-d12adcf907d3] Applied transformation DefaultPodTransformation to the Pod 'qotd-author-f44cb87ff-xxxxx'
    09:04:33.153 INFO  |- DefaultPodSpecTransformation: Configuration is use libinstana init
    09:04:33.162 INFO  |- DefaultPodSpecTransformation: Configuration is use autotrace nodejs
    （略）
    ```
