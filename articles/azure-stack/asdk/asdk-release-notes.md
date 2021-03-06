---
title: Microsoft Azure Stack Development Kit のリリース ノート | Microsoft Docs
description: Azure Stack Development Kit の機能強化、修正、既知の問題。
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/18/2018
ms.author: sethm
ms.reviewer: misainat
ms.openlocfilehash: 378617e331a5539fca3d993410325ef187816137
ms.sourcegitcommit: 707bb4016e365723bc4ce59f32f3713edd387b39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2018
ms.locfileid: "49430308"
---
# <a name="azure-stack-development-kit-release-notes"></a>Azure Stack Development Kit のリリース ノート  
この記事では、Azure Stack Development Kit の機能強化、修正、既知の問題に関する情報を提供します。 実行しているバージョンが不明な場合は、[ポータルを使用して確認](.\.\azure-stack-updates.md#determine-the-current-version)できます。

> [![RSS](./media/asdk-release-notes/feed-icon-14x14.png)](https://docs.microsoft.com/api/search/rss?search=Azure+Stack+Development+Kit+release+notes&locale=en-us#) [フィード](https://docs.microsoft.com/api/search/rss?search=Azure+Stack+Development+Kit+release+notes&locale=en-us#)をサブスクライブして、ASDK の新着情報を常に把握するようにしてください。

## <a name="build-11808097"></a>ビルド 1.1808.0.97

### <a name="new-features"></a>新機能
このビルドには、Azure Stack に対する次の機能強化と修正が含まれています。  

<!--  2712869   | IS  ASDK -->  
- **Azure Stack syslog クライアント (一般提供)** このクライアントを使用すると、Azure Stack インフラストラクチャに関連する監査ログ、アラート、およびセキュリティログを、Azure Stack の外部にある Syslog サーバーまたはセキュリティ情報イベント管理 (SIEM) ソフトウェアに転送できます。 Syslog のクライアントは、syslog サーバーがリッスンするポートを指定できるようになりました。

このリリースでは、syslog クライアントは、一般利用可能であり、運用環境のために使用できます。

詳細については、「[Azure Stack の Syslog 転送](../azure-stack-integrate-security.md)」を参照してください。

### <a name="fixed-issues"></a>修正された問題

<!-- 2702741 - IS ASDK --> 動的割り当てメソッドを使用してデプロイされているパブリック IP の固定された問題は、停止-割り当て解除が発行された後も保持される保証はありませんでした。 これらは保存されるようになりました。

<!-- 3078022 - IS ASDK --> 
- VM が 1808 の前に停止‐割り当て解除された場合、これは 1808 の更新後に再割り当てできませんでした。  この問題は 1809 で修正されています。 ここの状態にあり開始できなかったインスタンスは、この修正によって 1809 で開始できます。 また、修正プログラムにより、この問題は再発しないようになります。

- **さまざまな修正** - パフォーマンス、安定性、セキュリティ、Azure Stack で使用されるオペレーティング システムが修正されました。


### <a name="changes"></a>変更点

<!-- 1697698  | IS, ASDK --> 
- *クイック スタート チュートリアル*。ユーザー ポータルのダッシュボードにあるこのチュートリアルに、オンラインの Azure Stack ドキュメントにある関連する記事へのリンクが掲載されています。

<!-- 2515955   | IS ,ASDK--> 
- *[その他のサービス]* が *[すべてのサービス]* に置き換えられました (Azure Stack の管理者ポータルとユーザー ポータル)。 *[すべてのサービス]* は、Azure portal の場合と同じように Azure Stack ポータル内を移動するために使用できるようになりました。

<!--  TBD – IS, ASDK --> 
- *Basic A* の仮想マシン サイズは、ポータルを介して[仮想マシン スケール セット (VMSS) を作成する](../azure-stack-compute-add-scalesets.md)ものとしては廃止されました。 このサイズの VMSS を作成するには、PowerShell またはテンプレートをご使用ください。 

### <a name="known-issues"></a>既知の問題

#### <a name="portal"></a>ポータル  

<!-- 1697698  | IS, ASDK --> 
- *クイック スタート チュートリアル*。ユーザー ポータルのダッシュボードにあるこのチュートリアルに、オンラインの Azure Stack ドキュメントにある関連する記事へのリンクが掲載されています。

<!-- 2515955   | IS ,ASDK--> 
- *[その他のサービス]* が *[すべてのサービス]* に置き換えられました (Azure Stack の管理者ポータルとユーザー ポータル)。 *[すべてのサービス]* は、Azure portal の場合と同じように Azure Stack ポータル内を移動するために使用できるようになりました。

<!--  TBD – IS, ASDK --> 
- *Basic A* の仮想マシン サイズは、ポータルを介して[仮想マシン スケール セット (VMSS) を作成する](../azure-stack-compute-add-scalesets.md)ものとしては廃止されました。 このサイズの VMSS を作成するには、PowerShell またはテンプレートをご使用ください。

#### <a name="health-and-monitoring"></a>正常性と監視

<!-- 1264761 - IS ASDK -->  
- 以下の詳細情報の*正常性コントローラー* コンポーネントのアラートが表示されることがあります:  

   アラート #1:
   - 名前: インフラストラクチャ ロールの異常
   - 重大度: 警告
   - コンポーネント: 正常性コントローラー
   - 説明: 正常性コントローラーのハートビート スキャナーは使用できません。 これは、正常性レポートとメトリックに影響する可能性があります。  

  アラート #2:
   - 名前: インフラストラクチャ ロールの異常
   - 重大度: 警告
   - コンポーネント: 正常性コントローラー
   - 説明: 正常性コントローラーの障害スキャナーは使用できません。 これは、正常性レポートとメトリックに影響する可能性があります。

  どちらのアラートも無視しても問題ありません。時間が経過すると、自動的に閉じられます。  

<!-- 2368581 - IS. ASDK --> 
- Azure Stack オペレーターで、メモリ不足のアラートを受信し、テナント仮想マシンが*ファブリック VM の作成エラー*でデプロイできなかった場合、Azure Stack スタンプに使用できるメモリが不足している可能性があります。 ワークロードに使用できる容量の詳細については、[Azure Stack Capacity Planner](https://gallery.technet.microsoft.com/Azure-Stack-Capacity-24ccd822) に関するページを参照してください。


#### <a name="compute"></a>コンピューティング  

<!-- 3099544 – IS, ASDK --> 
- Azure Stack ポータルを使用して新しい仮想マシン (VM) を作成し、VM サイズを選択するときに、[米国ドル/月] 列に **[利用不可]** のメッセージが表示されます。 VM 価格の列の表示は、Azure Stack ではサポートされておらず、この列は表示されるべきではありません。

<!-- 3090289 – IS, ASDK --> 
- 更新プログラム 1808 の適用後、Managed Disks を使用した VM をデプロイするときに、次の問題が発生する可能性があります。

   1. 1808 更新の前に作成したサブスクリプションの場合、Managed Disks を使用した VM をデプロイすると、内部エラー メッセージが出て失敗することがあります。 このエラーを解決するには、サブスクリプションごとに次の手順に従ってください。
      1. テナント ポータルで、**[サブスクリプション]** に移動して、サブスクリプションを検索します。 **[リソース プロバイダー]** をクリックし、**[Microsoft.Compute]** をクリックした後、**[再登録]** をクリックします。
      2. 同じサブスクリプションで、**[アクセス制御 (IAM)]** に移動し、**[Azure Stack – マネージド ディスク]** がリストに含まれていることを確認します。
   2. マルチテナント環境を構成した場合、ゲスト ディレクトリに関連付けられているサブスクリプションで VM をデプロイすると、内部エラー メッセージが出て失敗することがあります。 このエラーを解決するには、次の手順に従ってください。
      1. [1808 Azure Stack 修正プログラム](https://support.microsoft.com/help/4468920)を適用します。
      2. [この記事](../azure-stack-enable-multitenancy.md#registering-azure-stack-with-the-guest-directory)にある手順に従って、各ゲスト ディレクトリを構成します。

<!-- 2869209 – IS, ASDK --> 
- [**Add-AzsPlatformImage** コマンドレット](https://docs.microsoft.com/powershell/module/azs.compute.admin/add-azsplatformimage?view=azurestackps-1.4.0)を使用する場合は、ディスクのアップロード先のストレージ アカウント URI として **-OsUri** パラメーターを使用する必要があります。 ディスクのローカル パスを使用した場合、次のエラーが出てコマンドレットが失敗します: *長時間実行処理が状態 '失敗' で失敗しました*。 

<!--  2966665 – IS, ASDK --> 
- SSD データ ディスクを Premium サイズのマネージド ディスク仮想マシン(DS、DSv2、Fs、Fs_V2) にアタッチすると、次のエラーが出て失敗します: "*仮想マシン 'vmname' のディスクを更新できませんでした。エラー: ストレージ アカウントの種類 'Premium_LRS' は VM サイズ 'Standard_DS/Ds_V2/FS/Fs_v2' ではサポートされないため、要求された操作は実行できません*"

   この問題を回避するには、*Premium_LRS ディスク*の代わりに *Standard_LRS* データ ディスクをご使用ください。 *Standard_LRS* データ ディスクを使用しても、IOPS または課金コストは変わりません。  

<!--  2795678 – IS, ASDK --> 
- ポータルを使用して Premium VM サイズ (DS、Ds_v2、FS、FSv2) の仮想マシン (VM) を作成すると、VM は Standard ストレージ アカウントで作成されます。 Standard ストレージ アカウントで作成しても、機能、IOPS、課金に影響はありません。 

   次の警告は無視してかまいません: *Premium ディスクをサポートしているサイズで Standard ディスクを使用することが選択されました。これはオペレーティング システムのパフォーマンスに影響を与える可能性があるため、お勧めできません。代わりに Premium ストレージ (SSD) の使用を検討してください。*

<!-- 2967447 - IS, ASDK --> 
- 仮想マシン スケール セット (VMSS) の作成エクスペリエンスでは、デプロイのオプションとして CentOS-based 7.2 が提供されます。 このイメージは Azure Stack では使用できないため、デプロイ用に別の OS を選択するか、またはデプロイする前にオペレーターが Marketplace からダウンロードしておいた別の CentOS イメージを指定する ARM テンプレートをご使用ください。

<!-- TBD -  IS ASDK --> 
- 仮想マシン スケール セットのスケーリング設定は、ポータルで使用できません。 回避策として、[Azure PowerShell](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-manage-powershell#change-the-capacity-of-a-scale-set) を使用できます。 PowerShell のバージョンの違いにより、`-VMScaleSetName` パラメーターの代わりに `-Name` を使用する必要があります。

<!-- TBD -  IS ASDK --> 
- Azure Stack ユーザー ポータルで仮想マシンを作成するときに、ポータルでは、D シリーズ VM に接続できるデータ ディスクの数に誤った値が表示されます。 サポートされているすべての D シリーズ VM は、Azure の構成と同数のデータ ディスクに対応できます。

<!-- TBD -  IS ASDK --> 
- VM イメージの作成に失敗した場合に、失敗したのに削除できない項目が、VM イメージのコンピューティング ブレードに追加される可能性があります。

  この問題を回避するには、Hyper-V (New-VHD -Path C:\dummy.vhd -Fixed -SizeBytes 1 GB) で作成できるダミーの VHD で新しい VM イメージを作成します。 このプロセスによって、失敗した項目の削除を妨げている問題が修正されます。 その後、ダミーのイメージを作成してから 15 分経つと、正常に削除できます。

  次に、前に失敗した VM イメージのダウンロードを再試行できます。

<!-- TBD -  IS ASDK --> 
- VM の展開で拡張機能のプロビジョニングに時間がかかりすぎる場合、ユーザーは、プロセスを停止して VM の割り当て解除または削除を試みるのではなく、プロビジョニングをタイムアウトさせる必要があります。  

<!-- 1662991 - IS ASDK --> 
- Linux の VM 診断は、Azure Stack でサポートされていません。 VM 診断を有効にして Linux VM を展開すると、展開が失敗します。 診断設定で Linux VM の基本メトリックを有効にした場合も、展開が失敗します。

<!-- 2724961- IS ASDK --> 
- サブスクリプション設定で **Microsoft.Insight** リソース プロバイダーを登録し、ゲスト OS 診断を有効にした Windows VM を作成すると、VM の概要ページにある CPU 使用率グラフにメトリック データを表示できなくなります。
 
  VM の CPU 使用率グラフを表示するには、**メトリック** ブレードに移動して、サポートされているすべての Windows VM ゲスト メトリックを表示します。

 

#### <a name="networking"></a>ネットワーク
<!-- 1766332 - IS, ASDK --> 
- **[ネットワーク]** で、**[Create VPN Gateway]\(VPN ゲートウェイの作成\)** をクリックして VPN 接続を設定する場合、VPN の種類として **[ポリシー ベース]** が表示されます。 このオプションを選択しないでください。 Azure Stack では **[ルート ベース]** オプションのみがサポートされています。

<!-- 1902460 -  IS ASDK --> 
- Azure Stack では、IP アドレスごとに 1 つの "*ローカル ネットワーク ゲートウェイ*" がサポートされます。 これは、テナントのすべてのサブスクリプションに当てはまります。 最初のローカル ネットワーク ゲートウェイ接続を作成した後に、続いて同じ IP アドレスでローカル ネットワーク ゲートウェイ リソースを作成しようとすると、ブロックされます。

<!-- 16309153 -  IS ASDK --> 
- "*自動*" の DNS サーバー設定を使用して作成した仮想ネットワークで、カスタム DNS サーバーに変更すると失敗します。 更新した設定は、その Vnet 内の VM にプッシュされません。

<!-- 2702741 -  IS ASDK --> 
- 動的割り当てメソッドを使用してデプロイされているパブリック IP は、停止 - 割り当て解除が発行された後も保持される保証はありません。

<!-- 2529607 - IS ASDK --> 
- Azure Stack の "*シークレット ローテーション*" 中は、2 ～ 5 分間、Public IP Addresses に到達できない期間があります。

<!-- 2664148 - IS ASDK --> 
- テナントが S2S VPN トンネルを使用して仮想マシンにアクセスするシナリオでは、ゲートウェイが既に作成された後でオンプレミスのサブネットがローカル ネットワーク ゲートウェイに追加された場合、接続しようとしても失敗するシナリオが発生する可能性があります。 


<!--  #### SQL and MySQL  -->


#### <a name="app-service"></a>App Service
<!-- 2352906 - IS ASDK --> 
- ユーザーは、サブスクリプションに最初の Azure 関数を作成する前に、ストレージ リソース プロバイダーを登録する必要があります。

<!-- TBD - IS ASDK --> 
- インフラストラクチャ (worker、管理、フロントエンド ロール) をスケールアウトするには、コンピューティングのリリース ノートの説明に従って PowerShell を使用する必要があります。  


#### <a name="usage"></a>使用法  
<!-- TBD -  IS ASDK --> 
- パブリック IP アドレス使用量メーターのデータは、レコードが作成された日時を示す *TimeDate* スタンプではなく、各レコードに対して同じ *EventDateTime* 値を示します。 現在、このデータを使用して、パブリック IP アドレスの使用を正確に算出することはできません。

<!-- #### Identity -->




## <a name="build-11807076"></a>Build 1.1807.0.76

### <a name="new-features"></a>新機能
このビルドには、Azure Stack に対する次の機能強化と修正が含まれています。  

<!-- 1658937 | ASDK, IS --> 
- **定義済みのスケジュールでバックアップを開始** - アプライアンスとしての Azure Stack に、インフラストラクチャ バックアップを自動で定期的にトリガーする機能が追加され、人の介入が不要になりました。 また、定義されている保有期間を超えたバックアップについては、外部共有が自動的にクリーンアップされます。 詳細については、「[PowerShell で Azure Stack のバックアップを有効にする](.\.\azure-stack-backup-enable-backup-powershell.md)」をご覧ください。

<!-- 2496385 | ASDK, IS -->  
- **合計バックアップ時間にデータ転送時間が追加されました。** 詳細については、「[PowerShell で Azure Stack のバックアップを有効にする](.\.\azure-stack-backup-enable-backup-powershell.md)」をご覧ください。

<!-- 1702130 | ASDK, IS --> 
- **外部バックアップ容量に、外部共有の正確な容量が表示されるようになりました。** (従来は 10 GB にハードコーディングされていました。)詳細については、「[PowerShell で Azure Stack のバックアップを有効にする](.\.\azure-stack-backup-enable-backup-powershell.md)」をご覧ください。
 
<!-- 2753130 |  IS, ASDK   -->  
- **Azure Resource Manager テンプレートで条件要素がサポートされるようになりました** - 条件を使用して Azure Resource Manger テンプレートでリソースをデプロイできるようになりました。 パラメーター値の有無の評価などの条件に基づいてリソースをデプロイするようにテンプレートを設計することができます。 テンプレートを条件として使用する方法については、Azure ドキュメントの「[リソースを条件付きでデプロイする](https://docs.microsoft.com/azure/architecture/building-blocks/extending-templates/conditional-deploy)」および「[Azure Resource Manager テンプレートの変数セクション](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-templates-variables)」を参照してください。 

   テンプレートを使用して、[複数のサブスクリプションまたはリソース グループにリソースをデプロイする](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-cross-resource-group-deployment)こともできます。  

<!--2753073 | IS, ASDK -->  
- **Microsoft.Network API リソース バージョンのサポートが更新され**、Azure Stack ネットワーク リソースで API バージョン 2015-06-15 から 2017-10-01 がサポートされるようになりました。 リソース バージョン 2017-10-01 から 2015-06-15 までのサポートは、このリリースには含まれていません。 機能の相違点については、「[Azure Stack ネットワークに関する考慮事項](.\.\user\azure-stack-network-differences.md)」を参照してください。

<!-- 2272116 | IS, ASDK   -->  
- **Azure Stack に、外部向け Azure Stack インフラストラクチャ エンドポイント (portal、adminportal、management、adminmanagement) に対する DNS 逆引き参照のサポートが追加されました**。 これにより、Azure Stack 外部エンドポイント名を IP アドレスから解決できます。

<!-- 2780899 |  IS, ASDK   --> 
- **Azure Stack で、既存の VM にネットワーク インターフェイスをさらに追加できるようになりました。**  この機能は、ポータル、PowerShell、CLI を使用して利用できます。 詳細については、Azure ドキュメントの「[仮想マシンのネットワーク インターフェイスの追加と削除](https://docs.microsoft.com/azure/virtual-network/virtual-network-network-interface-vm)」を参照してください。 

<!-- 2222444 | IS, ASDK   -->  
- **ネットワーク使用量メーターの正確性と回復性が向上しました**。 ネットワーク使用量メーターがより正確になり、中断されたサブスクリプション、停止期間、競合状態が考慮されるようになりました。

<!-- 2297790 | IS, ASDK -->  
- **Azure Stack の Syslog クライアントの機能強化 (プレビュー機能)**。 このクライアントを使用すると、Azure Stack インフラストラクチャに関連する監査とログを、Azure Stack 外部の Syslog サーバーまたはセキュリティ情報イベント管理 (SIEM) ソフトウェアに転送できます。 Syslog クライアントで、プレーン テキストまたは TLS 1.2 暗号化 (後者が既定の構成) による TCP プロトコルがサポートされるようになりました。 サーバーのみの認証または相互認証のいずれかを使用して、TLS 接続を構成できます。

  Syslog クライアントが Syslog サーバーと通信する方法 (プロトコル、暗号化、認証など) を構成するには、Set-SyslogServer コマンドレットを使用します。 このコマンドレットは、特権エンドポイント (PEP) から入手できます。 

  Syslog クライアント TLS 1.2 の相互認証用のクライアント側証明書を追加するには、PEP で Set-SyslogClient コマンドレットを使用します。

  このプレビューでは、監査と警告の数が大幅に増加します。 

  この機能はまだプレビュー段階であるため、運用環境では使用しないでください。

  詳細については、「[Azure Stack の Syslog 転送](.\.\azure-stack-integrate-security.md)」を参照してください。

<!-- ####### | IS, ASDK -->  
- **Azure Resource Manager にリージョン名が含まれています。** このリリースでは、Azure Resource Manager から取得したオブジェクトに、リージョンの名前属性が追加されるようになります。 既存の PowerShell スクリプトが別のコマンドレットにオブジェクトを直接渡すと、スクリプトによってエラーが発生し、失敗することがあります。 これは、Azure Resource Manager に準拠した動作であり、呼び出し元のクライアントがリージョン属性を削除する必要があります。 Azure Resource Manager の詳細については、「[Azure Resource Manager のドキュメント](https://docs.microsoft.com/azure/azure-resource-manager/)」を参照してください。

<!-- TBD | IS, ASDK -->  
- **委任されたプロバイダー間でのサブスクリプションの移動。** 同じディレクトリ テナントに属している新規または既存の委任されたプロバイダー サブスクリプション間で、サブスクリプションを移動できるようになりました。 また、既定プロバイダー サブスクリプションに属しているサブスクリプションも、同じディレクトリ テナント内にある委任されたプロバイダー サブスクリプションに移動できます。 詳細については、「[Azure Stack でのプランの委任](.\.\azure-stack-delegated-provider.md)」を参照してください。
 
<!-- 2536808 IS ASDK --> 
- Azure Marketplace からダウンロードしたイメージを使用して作成された **VM の VM 作成時間が改善**されました。

### <a name="fixed-issues"></a>修正された問題

<!-- TBD | ASDK, IS --> 
- 更新プロセスをより信頼できるものにするために、さまざまな改善が行われました。 さらに、基になるインフラストラクチャに修正が加えられました。これによりノード ドレインが改善され、その結果、更新中に発生する可能性のあるワークロードのダウンタイムが最小限に抑えられます。

<!--2292271 | ASDK, IS --> 
- 変更したクォータ制限が既存のサブスクリプションに適用されない問題を修正しました。  今後は、ユーザーのサブスクリプションに関連付けられているオファーとプランについて、そこに含まれるネットワーク リソースのクォータ制限を引き上げると、新しいサブスクリプションだけでなく既存のサブスクリプションにも新しい制限が適用されます。

<!-- 2448955 | IS ASDK --> 
- UTC+N タイム ゾーンでデプロイされているシステムをアクティビティ ログから検索するクエリが問題なく実行できるようになりました。    

<!-- 2319627 |  ASDK, IS --> 
- バックアップ構成パラメーター (パス/ユーザー名/パスワード/暗号化キー) の事前確認で、バックアップ構成に間違った設定が適用される問題を修正しました。 (以前は、バックアップに間違った設定が適用され、トリガーされた時点でバックアップが失敗していました。)

<!-- 2215948 |  ASDK, IS --> 
- 外部共有から手動でバックアップを削除したときにバックアップ リストが最新の情報に更新されるようになりました。

<!-- 2360715 |  ASDK, IS -->  
- データセンターの統合を設定する際、今後は、共有場所の AD FS メタデータ ファイルにはアクセスしません。 詳細については、「[フェデレーション メタデータ ファイルを指定して AD FS の統合を設定する](.\.\azure-stack-integrate-identity.md#setting-up-ad-fs-integration-by-providing-federation-metadata-file)」を参照してください。 

<!-- 2388980 | ASDK, IS --> 
- ネットワーク インターフェイスまたはロード バランサーに割り当てられている既存のパブリック IP アドレスを新しいネットワーク インターフェイスまたは Azure Load Balancer に割り当てることができない問題を修正しました。  

<!-- 2551834 - IS, ASDK --> 
- 管理ポータルまたはユーザー ポータルでストレージ アカウントの *[概要]* を選択すると、*[基本]* ウィンドウに必要なすべての情報が正しく表示されるようになりました。 

<!-- 2551834 - IS, ASDK --> 
- 管理ポータルまたはユーザー ポータルでストレージ アカウントに *[タグ]* を選択すると、情報が正しく表示されるようになりました。

<!-- TBD - IS ASDK --> 
- このバージョンの Azure Stack では、OEM 拡張機能パッケージからドライバーの更新プログラムを適用できないという問題が修正されています。

<!-- 2055809- IS ASDK --> 
- VM の作成が失敗したときに、コンピューティング ブレードから VM を削除できないという問題が修正されました。  

<!--  2643962 IS ASDK -->  
- *メモリ容量不足*に対する誤ったアラートが表示されなくなりました。

<!--  TBD ASDK --> 
- 特権エンドポイント (PEP) をホストする仮想マシンが 4 GB に引き上げられました。 ASDK では、この仮想マシンの名前は AzS-ERCS01 です。

- **さまざまな修正** - パフォーマンス、安定性、セキュリティ、Azure Stack で使用されるオペレーティング システムが修正されました。


<!-- ### Changes  -->
<!--   ### Additional releases timed with this update  -->


### <a name="known-issues"></a>既知の問題

#### <a name="portal"></a>ポータル  
<!-- 2931230 – IS  ASDK --> 
- アドオン プランとしてユーザー サブスクリプションに追加されたプランは、ユーザー サブスクリプションからプランを削除しても削除できません。 アドオン プランを参照するサブスクリプションも削除されるまで、プランは残ります。 

<!--2760466 – IS  ASDK --> 
- このバージョンを実行する新しい Azure Stack 環境をインストールすると、「*アクティブ化が必要*」を示すアラートが表示されない場合があります。 マーケットプレース シンジケーションを使用するには、[アクティブ化](.\.\azure-stack-registration.md)する必要があります。 

<!-- TBD - IS ASDK --> 
- バージョン 1804 で導入された 2 種類の管理サブスクリプションは使用しないでください。 **Metering サブスクリプション**と **Consumption サブスクリプション**のサブスクリプションの種類です。 これらのサブスクリプションの種類は、**Metering サブスクリプション**と **Consumption サブスクリプション**です。 これらのサブスクリプションの種類は、バージョン 1804 以降の新しい Azure Stack 環境では表示されますが、まだ使用できる状態ではありません。 **既定のプロバイダー サブスクリプション**の種類を引き続き使用する必要があります。

<!-- 2403291 - IS ASDK --> 
- 管理ポータルとユーザー ポータルの下部に水平スクロールバーが表示されない可能性があります。 水平スクロールバーにアクセスできない場合は、ポータルの左上にある階層リンク リストから表示するブレードの名前を選択して、階層リンクを使用してポータル内の前のブレードに移動します。
  ![階層リンク](media/asdk-release-notes/breadcrumb.png)

<!-- TBD -  IS ASDK --> 
- ユーザー サブスクリプションを削除すると、リソースが孤立します。 回避策として、まず、ユーザー リソースまたはリソース グループ全体を削除してから、ユーザー サブスクリプションを削除します。

<!-- TBD -  IS ASDK --> 
- Azure Stack ポータルを使用して、サブスクリプションへのアクセス許可を表示することはできません。 この問題を回避するには、PowerShell を使用してアクセス許可を確認します。

<!--  TBD | ASDK -->  
- Azure Stack のデプロイに対する既定のタイム ゾーンは UTC に設定されます。 Azure Stack のインストール時にタイム ゾーンを選択できますが、インストール中に自動的に既定として UTC に戻されます。

#### <a name="health-and-monitoring"></a>正常性と監視
<!-- 1264761 - IS ASDK -->  
- 以下の詳細情報の*正常性コントローラー* コンポーネントのアラートが表示されることがあります:  

   アラート #1:
   - 名前: インフラストラクチャ ロールの異常
   - 重大度: 警告
   - コンポーネント: 正常性コントローラー
   - 説明: 正常性コントローラーのハートビート スキャナーは使用できません。 これは、正常性レポートとメトリックに影響する可能性があります。  

  アラート #2:
   - 名前: インフラストラクチャ ロールの異常
   - 重大度: 警告
   - コンポーネント: 正常性コントローラー
   - 説明: 正常性コントローラーの障害スキャナーは使用できません。 これは、正常性レポートとメトリックに影響する可能性があります。

  どちらのアラートも無視しても問題ありません。時間が経過すると、自動的に閉じられます。  

<!-- 2368581 - IS. ASDK --> 
- Azure Stack オペレーターで、メモリ不足のアラートを受信し、テナント仮想マシンが*ファブリック VM の作成エラー*でデプロイできなかった場合、Azure Stack スタンプに使用できるメモリが不足している可能性があります。 ワークロードに使用できる容量の詳細については、[Azure Stack Capacity Planner](https://gallery.technet.microsoft.com/Azure-Stack-Capacity-24ccd822) に関するページを参照してください。

<!-- TBD - IS. ASDK --> 
- 特権エンドポイント (PEP) で **Test-AzureStack** コマンドレットを実行すると、**Azure Stack インフラストラクチャ ロール インスタンスのパフォーマンス** テストによって ERCS VM の警告メッセージが生成されます。 警告メッセージは無視して ASDK を引き続き使用できます。

#### <a name="compute"></a>コンピューティング
<!-- 2494144 - IS, ASDK --> 
- 仮想マシンの展開用に仮想マシンのサイズを選択すると、VM を作成するときに F シリーズの VM のサイズがサイズ セレクターの一部として表示されません。 セレクターに *F8s_v2*、*F16s_v2*、*F32s_v2*、および *F64s_v2* の VM サイズが表示されません。  
  この問題を回避するには、次のいずれかの方法を使用して VM をデプロイします。 どの方法でも、使用する VM のサイズを指定する必要があります。

  - **Azure Resource Manager テンプレート:** テンプレートを使用する際に、テンプレートの *vmSize* を使用する VM サイズと同じに設定します。 たとえば、*F32s_v2* サイズを使用する VM をデプロイするには、次のように入力します。  

    ```
        "properties": {
        "hardwareProfile": {
                "vmSize": "Standard_F32s_v2"
        },
    ```  
  - **Azure CLI:** [az vm create](https://docs.microsoft.com/cli/azure/vm?view=azure-cli-latest#az-vm-create) コマンドを使用して、`--size "Standard_F32s_v2"` と同様に VM サイズをパラメーターとして指定できます。

  - **PowerShell:** Powershell では、`-VMSize "Standard_F32s_v2"` と同様に VM サイズを指定するパラメーターとともに [New-AzureRMVMConfig](https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvmconfig?view=azurermps-6.0.0) を使用することができます。


<!-- TBD -  IS ASDK --> 
- 仮想マシン スケール セットのスケーリング設定は、ポータルで使用できません。 回避策として、[Azure PowerShell](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-manage-powershell#change-the-capacity-of-a-scale-set) を使用できます。 PowerShell のバージョンの違いにより、`-VMScaleSetName` パラメーターの代わりに `-Name` を使用する必要があります。

<!-- TBD -  IS ASDK --> 
- Azure Stack ユーザー ポータルで仮想マシンを作成するときに、ポータルでは、D シリーズ VM に接続できるデータ ディスクの数に誤った値が表示されます。 サポートされているすべての D シリーズ VM は、Azure の構成と同数のデータ ディスクに対応できます。

<!-- TBD -  IS ASDK --> 
- VM イメージの作成に失敗した場合に、失敗したのに削除できない項目が、VM イメージのコンピューティング ブレードに追加される可能性があります。

  この問題を回避するには、Hyper-V (New-VHD -Path C:\dummy.vhd -Fixed -SizeBytes 1 GB) で作成できるダミーの VHD で新しい VM イメージを作成します。 このプロセスによって、失敗した項目の削除を妨げている問題が修正されます。 その後、ダミーのイメージを作成してから 15 分経つと、正常に削除できます。

  次に、前に失敗した VM イメージのダウンロードを再試行できます。

<!-- TBD -  IS ASDK --> 
- VM の展開で拡張機能のプロビジョニングに時間がかかりすぎる場合、ユーザーは、プロセスを停止して VM の割り当て解除または削除を試みるのではなく、プロビジョニングをタイムアウトさせる必要があります。  

<!-- 1662991 - IS ASDK --> 
- Linux の VM 診断は、Azure Stack でサポートされていません。 VM 診断を有効にして Linux VM を展開すると、展開が失敗します。 診断設定で Linux VM の基本メトリックを有効にした場合も、展開が失敗します。

<!-- 2724961- IS ASDK --> 
- サブスクリプション設定で **Microsoft.Insight** リソース プロバイダーを登録し、ゲスト OS 診断を有効にした Windows VM を作成すると、VM の概要ページにメトリック データが表示されません。 

   VM の CPU 使用率グラフなどのメトリック データを表示するには、**[メトリック]** ブレードに移動して、サポートされているすべての Windows VM ゲスト メトリックを表示します。

#### <a name="networking"></a>ネットワーク
<!-- 1766332 - IS, ASDK --> 
- **[ネットワーク]** で、**[Create VPN Gateway]\(VPN ゲートウェイの作成\)** をクリックして VPN 接続を設定する場合、VPN の種類として **[ポリシー ベース]** が表示されます。 このオプションを選択しないでください。 Azure Stack では **[ルート ベース]** オプションのみがサポートされています。

<!-- 1902460 -  IS ASDK --> 
- Azure Stack では、IP アドレスごとに 1 つの "*ローカル ネットワーク ゲートウェイ*" がサポートされます。 これは、テナントのすべてのサブスクリプションに当てはまります。 最初のローカル ネットワーク ゲートウェイ接続を作成した後に、続いて同じ IP アドレスでローカル ネットワーク ゲートウェイ リソースを作成しようとすると、ブロックされます。

<!-- 16309153 -  IS ASDK --> 
- "*自動*" の DNS サーバー設定を使用して作成した仮想ネットワークで、カスタム DNS サーバーに変更すると失敗します。 更新した設定は、その Vnet 内の VM にプッシュされません。

<!-- 2702741 -  IS ASDK --> 
- 動的割り当てメソッドを使用してデプロイされているパブリック IP は、停止 - 割り当て解除が発行された後も保持される保証はありません。

<!-- 2529607 - IS ASDK --> 
- Azure Stack の "*シークレット ローテーション*" 中は、2 ～ 5 分間、Public IP Addresses に到達できない期間があります。

<!-- 2664148 - IS ASDK --> 
- テナントが S2S VPN トンネルを使用して仮想マシンにアクセスするシナリオでは、ゲートウェイが既に作成された後でオンプレミスのサブネットがローカル ネットワーク ゲートウェイに追加された場合、接続しようとしても失敗するシナリオが発生する可能性があります。 


#### <a name="sql-and-mysql"></a>SQL および MySQL
<!-- TBD - ASDK --> 
- データベースをホストするサーバーは、リソース プロバイダーとユーザーのワークロード専用にする必要があります。 他のコンシューマー (App Services など) が使用中のインスタンスは使用できません。

<!-- IS, ASDK --> 
- SQL と MySQL リソース プロバイダーの SKU を作成する場合、**[ファミリ]** 名では、スペースやピリオドなどの特殊文字はサポートされていません。

#### <a name="app-service"></a>App Service
<!-- 2352906 - IS ASDK --> 
- ユーザーは、サブスクリプションに最初の Azure 関数を作成する前に、ストレージ リソース プロバイダーを登録する必要があります。

<!-- TBD - IS ASDK --> 
- インフラストラクチャ (worker、管理、フロントエンド ロール) をスケールアウトするには、コンピューティングのリリース ノートの説明に従って PowerShell を使用する必要があります。  

<!-- TBD - IS ASDK --> 
- 現在、App Service は、*既定のプロバイダー サブスクリプション*にのみデプロイできます。

#### <a name="usage"></a>使用法  
<!-- TBD -  IS ASDK --> 
- パブリック IP アドレス使用量メーターのデータは、レコードが作成された日時を示す *TimeDate* スタンプではなく、各レコードに対して同じ *EventDateTime* 値を示します。 現在、このデータを使用して、パブリック IP アドレスの使用を正確に算出することはできません。

<!-- #### Identity -->






## <a name="build-11805147"></a>ビルド 1.1805.1.47

> [!TIP]  
> お客様のフィードバックに基づき、Microsoft Azure Stack に使用されているバージョン スキーマが更新されています。 今回の更新プログラム 1805 以降、新しいスキーマは現在のクラウド バージョンをより適切に表します。  
>
> バージョン スキーマは *Version.YearYearMonthMonth.MinorVersion.BuildNumber* になりました。この 2 番目と 3 番目のセットはバージョンとリリースを示しています。 たとえば、1805.1 は、1805 の*開発完了* (RTM) バージョンを示しています。  


### <a name="new-features"></a>新機能
このビルドには、Azure Stack に対する次の機能強化と修正が含まれています。  

<!-- 2297790 - IS, ASDK --> 
- **Azure Stack には、*プレビュー機能*として *Syslog* クライアント**が追加されました。 このクライアントを使用すると、Azure Stack インフラストラクチャに関連する監査ログとセキュリティログを、Azure Stack の外部にある Syslog サーバーまたはセキュリティ情報イベント管理 (SIEM) ソフトウェアに転送できます。 現在、Syslog クライアントは、既定のポート 514 を介した認証されていない UDP 接続のみをサポートしています。 各 Syslog メッセージのペイロードは、共通イベント形式 (CEF) です。

  Syslog クライアントを構成するには、特権エンドポイントで **Set-SyslogServer** コマンドレットを使用します。

  このプレビューでは、次の 3 つのアラートが表示されることがあります。 Azure Stack でこれらのアラートが表示される場合、アラートには*説明*と*修復*のガイダンスが記載されます。
  - タイトル: コードの整合性のオフ  
  - タイトル: 監査モードのコードの整合性
  - タイトル: ユーザー アカウントの作成

  この機能はプレビュー段階ですが、運用環境では使用しないでください。   


### <a name="fixed-issues"></a>修正された問題
- 管理ポータル内の[ドロップダウンから新しいサポート リクエストを開く](.\.\azure-stack-manage-portals.md#quick-access-to-help-and-support)ことができない問題を修正しました。 このオプションは意図したとおりに機能するようになりました。

<!--  TBD ASDK --> 
- 特権エンドポイント (PEP) をホストする仮想マシンが 4 GB に引き上げられました。 ASDK では、この仮想マシンの名前は AzS-ERCS01 です。

- **さまざまな修正** - パフォーマンス、安定性、セキュリティ、Azure Stack で使用されるオペレーティング システムが修正されました。


<!-- ### Changes  -->


<!--   ### Additional releases timed with this update  -->


### <a name="known-issues"></a>既知の問題

#### <a name="portal"></a>ポータル
<!-- 2931230 – IS  ASDK --> 
- アドオン プランとしてユーザー サブスクリプションに追加されたプランは、ユーザー サブスクリプションからプランを削除しても削除できません。 アドオン プランを参照するサブスクリプションも削除されるまで、プランは残ります。 

<!-- 2551834 - IS, ASDK --> 
- 管理ポータルまたはユーザー ポータルでストレージ アカウントの **[概要]** を選択すると、*[基本]* ウィンドウの情報が表示されません。  [基本] ウィンドウには、*リソース グループ*、*リージョン*、*サブスクリプション ID* などのアカウントに関する情報が表示されます。  [概要] のその他のオプションにアクセスできます。たとえば、*[サービス]*、*[監視]*、*[Explorer で開く]*、*[ストレージ アカウントの削除]* のオプションです。  

  利用不可の情報を表示するには、[Get-azureRMstorageaccount](https://docs.microsoft.com/powershell/module/azurerm.storage/get-azurermstorageaccount?view=azurermps-6.2.0) PowerShell コマンドレットを使用します。

<!-- 2551834 - IS, ASDK --> 
- 管理ポータルまたはユーザー ポータルでストレージ アカウントに **[タグ]** を選択したときに、情報が読み込まれず、表示されません。  

  利用不可の情報を表示するには、[Get-AzureRmTag](https://docs.microsoft.com/powershell/module/azurerm.tags/get-azurermtag?view=azurermps-6.2.0) PowerShell コマンドレットを使用します。

<!-- TBD - IS ASDK --> 
- 新しい管理サブスクリプションの種類である *Metering サブスクリプション*と *Consumption サブスクリプション*は使用しないでください。 これらの新しいサブスクリプションの種類は、バージョン 1804 で導入されましたが、まだ使用できる状態ではありません。 *既定のプロバイダー* サブスクリプションの種類を引き続き使用する必要があります。
  
<!-- TBD - IS ASDK --> 
- このバージョンの Azure Stack では、OEM Extension パッケージを使用してドライバーの更新プログラムを適用することはできません。  この問題の回避策はありません。
 
<!-- TBD - IS ASDK --> 
- 管理者ポータルの[ドロップダウン リストから新しいサポート要求を開く](.\.\azure-stack-manage-portals.md#quick-access-to-help-and-support)機能は使用できません。 代わりに、次のリンクを使用します。     
    - Azure Stack Development Kit の場合は、 https://aka.ms/azurestackforum を使います。    

<!-- 2403291 - IS ASDK --> 
- 管理ポータルとユーザー ポータルの下部に水平スクロールバーが表示されない可能性があります。 水平スクロールバーにアクセスできない場合は、ポータルの左上にある階層リンク リストから表示するブレードの名前を選択して、階層リンクを使用してポータル内の前のブレードに移動します。
  ![階層リンク](media/asdk-release-notes/breadcrumb.png)

<!-- TBD -  IS ASDK --> 
- ユーザー サブスクリプションを削除すると、リソースが孤立します。 回避策として、まず、ユーザー リソースまたはリソース グループ全体を削除してから、ユーザー サブスクリプションを削除します。

<!-- TBD -  IS ASDK --> 
- Azure Stack ポータルを使用して、サブスクリプションへのアクセス許可を表示することはできません。 この問題を回避するには、PowerShell を使用してアクセス許可を確認します。


#### <a name="health-and-monitoring"></a>正常性と監視
<!-- 1264761 - IS ASDK -->  
- 以下の詳細情報の*正常性コントローラー* コンポーネントのアラートが表示されることがあります:  

   アラート #1:
   - 名前: インフラストラクチャ ロールの異常
   - 重大度: 警告
   - コンポーネント: 正常性コントローラー
   - 説明: 正常性コントローラーのハートビート スキャナーは使用できません。 これは、正常性レポートとメトリックに影響する可能性があります。  

  アラート #2:
   - 名前: インフラストラクチャ ロールの異常
   - 重大度: 警告
   - コンポーネント: 正常性コントローラー
   - 説明: 正常性コントローラーの障害スキャナーは使用できません。 これは、正常性レポートとメトリックに影響する可能性があります。

    アラート #1 と #2 は、どちらも無視しても問題ありません。時間が経過すると、自動的に閉じられます。 

  *容量*に関する次のアラートも表示されることがあります。 このアラートでは、説明の中に示されている使用可能なメモリの割合が変化する可能性があります。  

  アラート #3:
   - 名前: メモリ容量不足
   - 重大度: 緊急
   - コンポーネント: 容量
   - 説明: このリージョンは、使用可能なメモリの 80.00% を超えるメモリを消費しています。 大量のメモリを使用する仮想マシンを作成すると、エラーが発生する可能性があります。  

  このバージョンの Azure Stack では、このアラートが間違って発行される可能性があります。 テナントの仮想マシンが引き続き正常にデプロイされる場合は、このアラートを無視しても問題はありません。 
  
  アラート #3 は、自動的に閉じることはありません。 このアラートを閉じた場合、Azure Stack は 15 分以内に同じアラートを作成します。  

<!-- 2368581 - IS. ASDK --> 
- Azure Stack オペレーターで、メモリ不足のアラートを受信し、テナント仮想マシンが*ファブリック VM の作成エラー*でデプロイできなかった場合、Azure Stack スタンプに使用できるメモリが不足している可能性があります。 ワークロードに使用できる容量の詳細については、[Azure Stack Capacity Planner](https://gallery.technet.microsoft.com/Azure-Stack-Capacity-24ccd822) に関するページを参照してください。

<!-- TBD - IS. ASDK --> 
- 特権エンドポイント (PEP) で Test-AzureStack コマンドレットを実行すると、ERCS VM の警告メッセージが生成されます。 ASDK は引き続き使用できます。 


#### <a name="compute"></a>コンピューティング
<!-- TBD - IS, ASDK --> 
- 仮想マシンの展開用に仮想マシンのサイズを選択すると、VM を作成するときに F シリーズの VM のサイズがサイズ セレクターの一部として表示されません。 セレクターに *F8s_v2*、*F16s_v2*、*F32s_v2*、および *F64s_v2* の VM サイズが表示されません。  
  この問題を回避するには、次のいずれかの方法を使用して VM をデプロイします。 どの方法でも、使用する VM のサイズを指定する必要があります。

  - **Azure Resource Manager テンプレート:** テンプレートを使用する際に、テンプレートの *vmSize* を使用する VM サイズと同じに設定します。 たとえば、*F32s_v2* サイズを使用する VM をデプロイするには、次のように入力します。  

    ```
        "properties": {
        "hardwareProfile": {
                "vmSize": "Standard_F32s_v2"
        },
    ```  
  - **Azure CLI:** [az vm create](https://docs.microsoft.com/cli/azure/vm?view=azure-cli-latest#az-vm-create) コマンドを使用して、`--size "Standard_F32s_v2"` と同様に VM サイズをパラメーターとして指定できます。

  - **PowerShell:** Powershell では、`-VMSize "Standard_F32s_v2"` と同様に VM サイズを指定するパラメーターとともに [New-AzureRMVMConfig](https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvmconfig?view=azurermps-6.0.0) を使用することができます。


<!-- TBD -  IS ASDK --> 
- 仮想マシン スケール セットのスケーリング設定は、ポータルで使用できません。 回避策として、[Azure PowerShell](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-manage-powershell#change-the-capacity-of-a-scale-set) を使用できます。 PowerShell のバージョンの違いにより、`-VMScaleSetName` パラメーターの代わりに `-Name` を使用する必要があります。

<!-- TBD -  IS ASDK --> 
- Azure Stack ユーザー ポータルで仮想マシンを作成するときに、ポータルでは、D シリーズ VM に接続できるデータ ディスクの数に誤った値が表示されます。 サポートされているすべての D シリーズ VM は、Azure の構成と同数のデータ ディスクに対応できます。

<!-- TBD -  IS ASDK --> 
- VM イメージの作成に失敗した場合に、失敗したのに削除できない項目が、VM イメージのコンピューティング ブレードに追加される可能性があります。

  この問題を回避するには、Hyper-V (New-VHD -Path C:\dummy.vhd -Fixed -SizeBytes 1 GB) で作成できるダミーの VHD で新しい VM イメージを作成します。 このプロセスによって、失敗した項目の削除を妨げている問題が修正されます。 その後、ダミーのイメージを作成してから 15 分経つと、正常に削除できます。

  次に、前に失敗した VM イメージのダウンロードを再試行できます。

<!-- TBD -  IS ASDK --> 
- VM の展開で拡張機能のプロビジョニングに時間がかかりすぎる場合、ユーザーは、プロセスを停止して VM の割り当て解除または削除を試みるのではなく、プロビジョニングをタイムアウトさせる必要があります。  

<!-- 1662991 - IS ASDK --> 
- Linux の VM 診断は、Azure Stack でサポートされていません。 VM 診断を有効にして Linux VM を展開すると、展開が失敗します。 診断設定で Linux VM の基本メトリックを有効にした場合も、展開が失敗します。

#### <a name="networking"></a>ネットワーク
<!-- TBD - IS ASDK --> 
- 管理ポータルまたはユーザー ポータルで、ユーザー定義のルートを作成できません。 回避策として、[Azure PowerShell](https://docs.microsoft.com/azure/virtual-network/tutorial-create-route-table-powershell) を使用します。

<!-- 1766332 - IS, ASDK --> 
- **[ネットワーク]** で、**[Create VPN Gateway]\(VPN ゲートウェイの作成\)** をクリックして VPN 接続を設定する場合、VPN の種類として **[ポリシー ベース]** が表示されます。 このオプションを選択しないでください。 Azure Stack では **[ルート ベース]** オプションのみがサポートされています。

<!-- 2388980 -  IS ASDK --> 
- VM を作成してパブリック IP アドレスに関連付けた後は、IP アドレスからその VM の関連付けを解除することはできません。 関連付けの解除は機能したように見えますが、以前に割り当てられたパブリック IP アドレスは、元の VM に関連付けられたままになります。

  現時点では、作成した新しい VM には新しいパブリック IP アドレスのみを使用する必要があります。

  この動作は、IP アドレスを新しい VM に 再割り当てした (一般に *VIP スワップ*と呼ばれます) 場合でも行われます。 以降のこの IP アドレスによるすべての接続の試みは、新しい VM ではなく、元の VM に接続する結果になります。

<!-- 2292271 - IS ASDK --> 
- テナントのサブスクリプションに関連付けられているオファーとプランの一部であるネットワーク リソースのクォータ制限を引き上げた場合、新しい制限がそのサブスクリプションに適用されません。 ただし、クォータを増加した後に作成した新しいサブスクリプションには新しい制限が適用されます。

  この問題を回避するには、プランがサブスクリプションに既に関連付けられている場合は、アドオン プランを使用して、ネットワーク クォータを増やします。 詳細については、[アドオン プランを利用できるようにする方法](.\.\azure-stack-subscribe-plan-provision-vm.md#to-make-an-add-on-plan-available)を参照してください。

<!-- 2304134 IS ASDK --> 
- DNS ゾーン リソースまたはそれに関連付けられたルート テーブル リソースがあるサブスクリプションを削除することができません。 サブスクリプションを正常に削除するには、まずテナント サブスクリプションから DNS ゾーンとルート テーブルのリソースを削除する必要があります。

<!-- 1902460 -  IS ASDK --> 
- Azure Stack では、IP アドレスごとに 1 つの "*ローカル ネットワーク ゲートウェイ*" がサポートされます。 これは、テナントのすべてのサブスクリプションに当てはまります。 最初のローカル ネットワーク ゲートウェイ接続を作成した後に、続いて同じ IP アドレスでローカル ネットワーク ゲートウェイ リソースを作成しようとすると、ブロックされます。

<!-- 16309153 -  IS ASDK --> 
- "*自動*" の DNS サーバー設定を使用して作成した仮想ネットワークで、カスタム DNS サーバーに変更すると失敗します。 更新した設定は、その Vnet 内の VM にプッシュされません。

<!-- TBD -  IS ASDK --> 
- Azure Stack では、VM を展開した後に、VM インスタンスにネットワーク インターフェイスをさらに追加することはできません。 VM に複数のネットワーク インターフェイスが必要な場合は、展開時に定義する必要があります。


#### <a name="sql-and-mysql"></a>SQL および MySQL
<!-- TBD - ASDK --> 
- データベースをホストするサーバーは、リソース プロバイダーとユーザーのワークロード専用にする必要があります。 他のコンシューマー (App Services など) が使用中のインスタンスは使用できません。

<!-- IS, ASDK --> 
- SQL と MySQL リソース プロバイダーの SKU を作成する場合、**[ファミリ]** 名では、スペースやピリオドなどの特殊文字はサポートされていません。

#### <a name="app-service"></a>App Service
<!-- 2352906 - IS ASDK --> 
- ユーザーは、サブスクリプションに最初の Azure 関数を作成する前に、ストレージ リソース プロバイダーを登録する必要があります。

<!-- TBD - IS ASDK --> 
- インフラストラクチャ (worker、管理、フロントエンド ロール) をスケールアウトするには、コンピューティングのリリース ノートの説明に従って PowerShell を使用する必要があります。  

<!-- TBD - IS ASDK --> 
- 現在、App Service は、*既定のプロバイダー サブスクリプション*にのみデプロイできます。 <!-- In a future update, App Service will deploy into the new *Metering subscription* that was introduced in Azure Stack 1804. When Metering is supported for use, all existing deployments will be migrated to this new subscription type. -->

#### <a name="usage"></a>使用法  
<!-- TBD -  IS ASDK --> 
- パブリック IP アドレス使用量メーターのデータは、レコードが作成された日時を示す *TimeDate* スタンプではなく、各レコードに対して同じ *EventDateTime* 値を示します。 現在、このデータを使用して、パブリック IP アドレスの使用を正確に算出することはできません。

<!-- #### Identity -->

