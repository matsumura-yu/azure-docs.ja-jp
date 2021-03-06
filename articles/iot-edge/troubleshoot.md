---
title: Azure IoT Edge のトラブルシューティング | Microsoft Docs
description: Azure IoT Edge での一般的な問題を解決し、トラブルシューティング スキルについて説明します
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 06/26/2018
ms.topic: conceptual
ms.service: iot-edge
services: iot-edge
ms.openlocfilehash: a63a31c5ceb4298829f85627196fea5d7a38ca4b
ms.sourcegitcommit: 7b0778a1488e8fd70ee57e55bde783a69521c912
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2018
ms.locfileid: "49068504"
---
# <a name="common-issues-and-resolutions-for-azure-iot-edge"></a>Azure IoT Edge での一般的な問題と解決

お使いの環境で Azure IoT Edge の実行中に問題が発生した場合は、この記事を参考にしてトラブルシューティングと解決を行ってください。 

## <a name="standard-diagnostic-steps"></a>標準的な診断手順 

問題が発生したときは、コンテナーのログと、デバイスとの間でやり取りされたメッセージを調べて、お使いの IoT Edge デバイスの状態を詳しく把握します。 情報を収集するには、このセクションのコマンドとツールを使います。 

### <a name="check-the-status-of-the-iot-edge-security-manager-and-its-logs"></a>IoT Edge Security Manager の状態とそのログを確認します。

Linux の場合:
- IoT Edge Security Manager の状態を確認します。

   ```bash
   sudo systemctl status iotedge
   ```

- IoT Edge Security Manager のログを確認します。

    ```bash
    sudo journalctl -u iotedge -f
    ```

- IoT Edge Security Manager のログの詳細を確認します。

   - iotedge デーモンの設定を編集します。

      ```bash
      sudo systemctl edit iotedge.service
      ```
   
   - 次の行を更新します。
    
      ```
      [Service]
      Environment=IOTEDGE_LOG=edgelet=debug
      ```
    
   - IoT Edge セキュリティ デーモンを再起動します。
    
      ```bash
      sudo systemctl cat iotedge.service
      sudo systemctl daemon-reload
      sudo systemctl restart iotedge
      ```

Windows の場合:
- IoT Edge Security Manager の状態を確認します。

   ```powershell
   Get-Service iotedge
   ```

- IoT Edge Security Manager のログを確認します。

   ```powershell
   # Displays logs from today, newest at the bottom.
 
   Get-WinEvent -ea SilentlyContinue `
   -FilterHashtable @{ProviderName= "iotedged";
     LogName = "application"; StartTime = [datetime]::Today} |
   select TimeCreated, Message |
   sort-object @{Expression="TimeCreated";Descending=$false} |
   format-table -autosize -wrap
   ```

### <a name="if-the-iot-edge-security-manager-is-not-running-verify-your-yaml-configuration-file"></a>IoT Edge Security Manager が実行されていない場合は、yaml 構成ファイルを確認してください。

> [!WARNING]
> YAML ファイルには、インデントとしてタブを含めることはできません。 代わりにスペース 2 つを使用してください。

Linux の場合:

   ```bash
   sudo nano /etc/iotedge/config.yaml
   ```

Windows の場合:

   ```cmd
   notepad C:\ProgramData\iotedge\config.yaml
   ```

### <a name="check-container-logs-for-issues"></a>コンテナーのログで問題を確認する

IoT Edge セキュリティ デーモンが実行されている場合は、コンテナーのログを参照して問題を検出します。 最初に展開済みのコンテナーを調べた後、IoT Edge ランタイムを構成するコンテナー (Edge エージェントと Edge ハブ) を調べます。 通常、Edge エージェントのログでは、各コンテナーのライフサイクルについての情報が提供されます。 Edge ハブのログでは、メッセージングとルーティングについての情報が提供されます。 

   ```cmd
   iotedge logs <container name>
   ```

### <a name="view-the-messages-going-through-the-edge-hub"></a>Edge ハブを経由するメッセージを確認します。

Edge ハブを経由するメッセージを確認し、edgeAgent および edgeHubランタイム コンテナーからの詳細なログからデバイスのプロパティの更新についての洞察を収集します。 これらのコンテナーで詳細ログを有効にするには、yaml 構成ファイルに`RuntimeLogLevel` を設定します。 ファイルを開くには:

Linux の場合:

   ```bash
   sudo nano /etc/iotedge/config.yaml
   ```

Windows の場合:

   ```cmd
   notepad C:\ProgramData\iotedge\config.yaml
   ```

既定では、`agent` 要素は次のようになります。

   ```yaml
   agent:
     name: edgeAgent
     type: docker
     env: {}
     config:
       image: mcr.microsoft.com/azureiotedge-agent:1.0
       auth: {}
   ```

`env: {}` を以下で置き換えます。

> [!WARNING]
> YAML ファイルには、インデントとしてタブを含めることはできません。 代わりにスペース 2 つを使用してください。

   ```yaml
   env:
     RuntimeLogLevel: debug
   ```

ファイルを保存し、IoT Edge Security Manager を再起動します。

IoT Hub デバイスと IoT Edge デバイスの間で送信されたメッセージを確認することもできます。 Visual Studio Code 用の [Azure IoT Toolkit](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit) 拡張機能を使ってメッセージを表示します。 詳しくは、「[Handy tool when you develop with Azure IoT](https://blogs.msdn.microsoft.com/iotdev/2017/09/01/handy-tool-when-you-develop-with-azure-iot/)」(Azure IoT で開発するときの便利なツール) をご覧ください。

### <a name="restart-containers"></a>コンテナーを再起動する
ログとメッセージの情報を調べた後は、コンテナーの再起動を試みることもできます。

```
iotedge restart <container name>
```

IoT Edge ランタイム コンテナーを再起動する:

```
iotedge restart edgeAgent && iotedge restart edgeHub
```

### <a name="restart-the-iot-edge-security-manager"></a>IoT Edge Security Manager を再起動する

問題がまだ解決しない場合は、IoT Edge Security Manager を再起動することができます。

Linux の場合:

   ```cmd
   sudo systemctl restart iotedge
   ```

Windows の場合:

   ```powershell
   Stop-Service iotedge -NoWait
   sleep 5
   Start-Service iotedge
   ```

## <a name="edge-agent-stops-after-about-a-minute"></a>約 1 分後に Edge エージェントが停止する

Edge エージェントが起動し、約 1 分間正常に実行した後、停止します。 ログでは、Edge エージェントが AMQP 経由で IoT Hub に接続を試み、約 30 秒後に WebSocket 経由の AMQP を使って接続しようとしたことが示されています。 それが失敗すると、Edge エージェントは終了します。 

Edge エージェント ログの例:

```output
2017-11-28 18:46:19 [INF] - Starting module management agent. 
2017-11-28 18:46:19 [INF] - Version - 1.0.7516610 (03c94f85d0833a861a43c669842f0817924911d5) 
2017-11-28 18:46:19 [INF] - Edge agent attempting to connect to IoT Hub via AMQP... 
2017-11-28 18:46:49 [INF] - Edge agent attempting to connect to IoT Hub via AMQP over WebSocket... 
```

### <a name="root-cause"></a>根本原因
ホスト ネットワークでのネットワーク構成のために、Edge エージェントはネットワークに到達できません。 エージェントは、最初に AMQP (ポート 5671) で接続を試みます。 それが失敗した場合は、WebSocket (ポート 443) を試します。

IoT Edge ランタイムは、各モジュールが通信するネットワークをセットアップします。 Linux では、このネットワークはブリッジ ネットワークです。 Windows では、NAT を使います。 この問題は、NAT ネットワークを使う Windows コンテナーを使っている Windows デバイスで、より多く見られます。 

### <a name="resolution"></a>解決策
このブリッジ/NAT ネットワークに割り当てられている IP アドレスにインターネットへのルートが存在することを確認します。 ホストでの VPN 構成が IoT Edge ネットワークをオーバーライドしている場合があります。 

## <a name="edge-hub-fails-to-start"></a>Edge ハブの起動が失敗する

Edge ハブの起動が失敗し、次のメッセージがログに出力されます。 

```output
One or more errors occurred. 
(Docker API responded with status code=InternalServerError, response=
{\"message\":\"driver failed programming external connectivity on endpoint edgeHub (6a82e5e994bab5187939049684fb64efe07606d2bb8a4cc5655b2a9bad5f8c80): 
Error starting userland proxy: Bind for 0.0.0.0:443 failed: port is already allocated\"}\n) 
```

### <a name="root-cause"></a>根本原因
ホスト コンピューター上の他のプロセスが、ポート 443 にバインドしています。 Edge ハブは、ゲートウェイ シナリオで使うためにポート 5671 と 443 をマップします。 別のプロセスがこのポートを既にバインドしている場合、このポート マッピングは失敗します。 

### <a name="resolution"></a>解決策
ポート 443 を使っているプロセスを探して停止します。 通常、このプロセスは Web サーバーです。

## <a name="edge-agent-cant-access-a-modules-image-403"></a>Edge エージェントがモジュールのイメージにアクセスできない (403)
コンテナーの実行が失敗し、Edge エージェントのログで 403 エラーが表示されます。 

### <a name="root-cause"></a>根本原因
Edge エージェントに、モジュールのイメージにアクセスするためのアクセス許可がありません。 

### <a name="resolution"></a>解決策
配置マニフェストで、レジストリの資格情報が正しく指定されていることを確認します。

## <a name="iot-edge-security-daemon-fails-with-an-invalid-hostname"></a>IoT Edge セキュリティ デーモンが無効なホスト名で失敗する

コマンド `sudo journalctl -u iotedge` が失敗して、次のメッセージが出力されます。 

```output
Error parsing user input data: invalid hostname. Hostname cannot be empty or greater than 64 characters
```

### <a name="root-cause"></a>根本原因
IoT Edge ランタイムは、64 文字未満のホスト名のみをサポートできます。 これは通常、物理マシンの場合は問題になりませんが、仮想マシン上にランタイムを設定するときに発生する場合があります。 特に、Azure でホストされる Windows 仮想マシンのために自動生成されるホスト名は長くなる傾向があります。 

### <a name="resolution"></a>解決策
このエラーが発生したときは、仮想マシンの DNS 名を構成し、setup コマンドでその DNS 名をホスト名として設定することで、エラーを解決できます。

1. Azure Portal で、目的の仮想マシンの概要ページに移動します。 
2. DNS 名の下の **[構成]** を選択します。 仮想マシンに既に構成済みの DNS 名がある場合は、新しいものを構成する必要はありません。 

   ![DNS 名を構成する](./media/troubleshoot/configure-dns.png)

3. **[DNS 名ラベル]** に値を指定し、**[保存]** を選択します。
4. 新しい DNS 名をコピーします。名前は **\<DNSnamelabel\>.\<vmlocation\>.cloudapp.azure.com** の形式である必要があります。
5. 仮想マシン内で、次のコマンドを使用して、実際の DNS 名によって IoT Edge ランタイムを設定します。

   - Linux の場合:

      ```bash
      sudo nano /etc/iotedge/config.yaml
      ```

   - Windows の場合:

      ```cmd
      notepad C:\ProgramData\iotedge\config.yaml
      ```

## <a name="stability-issues-on-resource-constrained-devices"></a>リソースに制約があるデバイスでの安定性の問題 
Raspberry Pi のようなリソースに制約があるデバイスを、特にゲートウェイとして使用した場合、安定性の問題が発生する可能性があります。 症状には、Edge ハブ モジュールのメモリ不足例外、ダウンストリームのデバイスの構成不能、数時間後のデバイスによるテレメトリ メッセージの送信停止が含まれます。

### <a name="root-cause"></a>根本原因
Edge ハブは Edge ランタイムの一部であり、既定ではパフォーマンス用に最適化されており、大きな塊のメモリを割り当てようとします。 これは制約がある Edge デバイスには適していないため、安定性の問題が発生する可能性があります。

### <a name="resolution"></a>解決策
Edge ハブに対して、環境変数 **OptimizeForPerformance** を**false** に設定します。 この作業を実行する 2 つの方法があります。

UI で: 

ポータルで、*[デバイスの詳細]*->*[モジュールの設定]*->*[Edge ランタイムの詳細設定を構成する]* に移動し、*Edge ハブ* に対して *false* が設定された *OptimizeForPerformance* という名前の環境変数を作成します。

![optimizeforperformance][img-optimize-for-perf]

**OR**

デプロイ マニフェストで:

```json
  "edgeHub": {
    "type": "docker",
    "settings": {
      "image": "mcr.microsoft.com/azureiotedge-hub:1.0",
      "createOptions": <snipped>
    },
    "env": {
      "OptimizeForPerformance": {
          "value": "false"
      }
    },
```
## <a name="cant-get-the-iot-edge-daemon-logs-on-windows"></a>Windows で IoT Edge デーモン ログを取得できません
Windows で `Get-WinEvent` の使用時に EventLogException が表示された場合、レジストリ エントリを確認してください。

### <a name="root-cause"></a>根本原因
`Get-WinEvent` PowerShell コマンドは、特定の `ProviderName` でログを見つけるとき、レジストリ エントリを利用します。

### <a name="resolution"></a>解決策
IoT Edge デーモンにレジストリ エントリを設定します。 次の内容の **iotedge.reg** ファイルを作成し、ダブルクリックするか `reg import iotedge.reg` コマンドを使用して Windows レジストリにインポートします。

```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\EventLog\Application\iotedged]
"CustomSource"=dword:00000001
"EventMessageFile"="C:\\ProgramData\\iotedge\\iotedged.exe"
"TypesSupported"=dword:00000007
```

## <a name="iot-edge-module-fails-to-send-a-message-to-the-edgehub-with-404-error"></a>IoT Edge モジュールが 404 エラーで edgeHub にメッセージを送信できない

カスタム IoT Edge モジュールは、404 `Module not found` エラーで edgeHub にメッセージを送信できません。 IoT Edge デーモンによって、次のメッセージがログに出力されます。 

```output
Error: Time:Thu Jun  4 19:44:58 2018 File:/usr/sdk/src/c/provisioning_client/adapters/hsm_client_http_edge.c Func:on_edge_hsm_http_recv Line:364 executing HTTP request fails, status=404, response_buffer={"message":"Module not found"}u, 04 ) 
```

### <a name="root-cause"></a>根本原因
IoT Edge デーモンでは、セキュリティ上の理由から、edgeHub に接続するすべてのモジュールのプロセス識別が強制されます。 モジュールによって送信されているすべてのメッセージが、モジュールのメイン プロセス ID から来たものであることが確認されます。 モジュールによって、最初に確立されたのと異なるプロセス ID からメッセージが送信されている場合、そのメッセージは 404 エラー メッセージで拒否されます。

### <a name="resolution"></a>解決策
カスタム IoT Edge モジュールによる edgeHub へのメッセージの送信で、常に同じプロセス ID が使用されるようにします。 たとえば、Docker ファイルで、`CMD` コマンドではなく `ENTRYPOINT` コマンドを使用するようにします。これは、`ENTRYPOINT` では単一のプロセス ID が使用されるのに対して、`CMD` ではモジュールに 1 つのプロセス ID が使用され、メイン プログラムを実行している bash コマンドには別のプロセス ID が使用されるためです。


## <a name="firewall-and-port-configuration-rules-for-iot-edge-deployment"></a>IoT Edge デプロイのファイアウォール規則とポート構成規則
Azure IoT Edge では、サポートされている IoT Hub プロトコルを使用した、オンプレミスの Edge サーバーから Azure クラウドへの通信が許可されています。[通信プロトコルの選択](../iot-hub/iot-hub-devguide-protocols.md)に関するページを参照してください。 セキュリティ強化のため、Azure IoT Edge と Azure IoT Hub の間の通信チャネルは常にアウトバウンドに構成されます。これは、[Services Assisted Communication パターン](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/)に基づいています。そうすることで、悪意のある者が探索する攻撃面が最小限に抑えられます。 インバウンド通信は、Azure IoT Hub が Azure IoT Edge サーバーにメッセージをプッシュダウンする必要がある特定のシナリオ (たとえば cloud-to-device メッセージング) でのみ必要です。それらの通信も、安全な TLS チャネルを使用して保護され、さらに X.509 証明書と TPM デバイス モジュールを使用して保護されます。 この通信の確立方法は、Azure IoT Edge セキュリティ マネージャーによって管理されます。[IoT Edge セキュリティ マネージャー](../iot-edge/iot-edge-security-manager.md)に関するページを参照してください。

IoT Edge は、Azure IoT Edge ランタイムとデプロイされたモジュールをセキュリティで保護するための強化された構成を提供しますが、依然として基になるマシンとネットワークの構成に依存しています。 そのため、Edge からクラウドへの安全な通信を実現するための適切なネットワーク規則およびファイアウォール規則が設定されていることを確認する必要があります。 Azure IoT Edge ランタイムがホストされている、基になるサーバーのファイアウォール規則を構成するときには、以下の設定をガイドラインとして使用できます。

|プロトコル|ポート|受信|送信|ガイダンス|
|--|--|--|--|--|
|MQTT|8883|ブロック (既定値)|ブロック (既定値)|<ul> <li>通信プロトコルとして MQTT を使用する場合は、送信 (アウトバウンド) をオープンになるように構成します。<li>MQTT での 1883 は、IoT Edge ではサポートされていません。 <li>受信 (インバウンド) 接続はブロックする必要があります。</ul>|
|AMQP|5671|ブロック (既定値)|オープン (既定値)|<ul> <li>IoT Edge の既定の通信プロトコル。 <li> Azure IoT Edge が他のサポートされているプロトコル用に構成されていない場合、または AMQP が望ましい通信プロトコルである場合は、オープンになるように構成する必要があります。<li>AMQP での 5672 は、IoT Edge ではサポートされていません。<li>IoT Hub でサポートされている別のプロトコルが Azure IoT Edge によって使用されている場合は、このポートをブロックします。<li>受信 (インバウンド) 接続はブロックする必要があります。</ul></ul>|
|HTTPS|443|ブロック (既定値)|オープン (既定値)|<ul> <li>443 で IoT Edge プロビジョニング用に送信 (アウトバウンド) がオープンになるように構成します。手動スクリプトまたは Azure IoT Device Provisioning Service (DPS) を使用する場合は、こうする必要があります。 <li>受信 (インバウンド) 接続が以下の特定のシナリオだけでオープンになるようにする必要があります。 <ul> <li>  メソッド要求を送信することがあるリーフ デバイスを備えた透過的なゲートウェイがある場合。 この場合、ポート 443 は、IoT Hub に接続したり Azure IoT Edge を通じて IoT Hub サービスを提供したりするために外部ネットワークに対してオープンにする必要はありません。 そのため、受信規則は内部ネットワークからのオープンな受信 (インバウンド) だけに制限することができます。 <li> Client to Device (C2D) シナリオの場合。</ul><li>HTTP での 80 は、IoT Edge ではサポートされていません。<li>企業内で非 HTTP プロトコル (AMQP、MQTT など) を構成できない場合は、メッセージを WebSockets 経由で送信できます。 その場合、ポート 443 は WebSocket 通信のために使用されます。</ul>|


## <a name="next-steps"></a>次の手順
IoT Edge プラットフォームのバグを発見したと思われる場合は、 改善を続けられるように[問題を報告](https://github.com/Azure/iotedge/issues)してください。 

<!-- Images -->
[img-optimize-for-perf]: ./media/troubleshoot/OptimizeForPerformanceFalse.png
