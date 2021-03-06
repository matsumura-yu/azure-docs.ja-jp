---
title: Azure リソースのマネージド ID に関する FAQ と既知の問題
description: Azure リソースのマネージド ID に関する既知の問題。
services: active-directory
documentationcenter: ''
author: daveba
manager: mtillman
editor: ''
ms.assetid: 2097381a-a7ec-4e3b-b4ff-5d2fb17403b6
ms.service: active-directory
ms.component: msi
ms.devlang: ''
ms.topic: conceptual
ms.tgt_pltfrm: ''
ms.workload: identity
ms.date: 12/12/2017
ms.author: daveba
ms.openlocfilehash: 2a759aea4288af2e90335b47244408d6a537e24b
ms.sourcegitcommit: f3bd5c17a3a189f144008faf1acb9fabc5bc9ab7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2018
ms.locfileid: "44295583"
---
# <a name="faqs-and-known-issues-with-managed-identities-for-azure-resources"></a>Azure リソースのマネージド ID に関する FAQ と既知の問題

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

## <a name="frequently-asked-questions-faqs"></a>よく寄せられる質問 (FAQ)

> [!NOTE]
> Azure リソースのマネージド ID は、以前のマネージドサービス ID (MSI) の新しい名前です。

### <a name="does-managed-identities-for-azure-resources-work-with-azure-cloud-services"></a>Azure リソースのマネージド ID は Azure Cloud Services で動作しますか?

いいえ、Azure Cloud Services で Azure リソースのマネージド ID をサポートする予定はありません。

### <a name="does-managed-identities-for-azure-resources-work-with-the-active-directory-authentication-library-adal-or-the-microsoft-authentication-library-msal"></a>Azure リソースのマネージド ID は Active Directory Authentication Library (ADAL) または Microsoft Authentication Library (MSAL) で動作しますか?

いいえ、Azure リソースのマネージド ID は、ADAL または MSAL とまだ統合されていません。 REST エンドポイントを使用して Azure リソースのマネージド ID のトークンを取得する方法については、[Azure VM 上で Azure リソースのマネージド ID を使用してアクセス トークンを取得する方法](how-to-use-vm-token.md) を参照してください。

### <a name="what-is-the-security-boundary-of-managed-identities-for-azure-resources"></a>Azure リソースのマネージド ID のセキュリティ境界は何ですか?

ID のセキュリティ境界は、ID のアタッチ先リソースです。 たとえば、Azure リソースのマネージド ID が有効な仮想マシンのセキュリティ境界は、仮想マシンです。 その VM 上で実行されているすべてのコードは、Azure リソース エンドポイントと要求トークンのマネージド ID を呼び出すことができます。 これは Azure リソースのマネージド ID をサポートする他のリソースと同様のエクスペリエンスです。

### <a name="should-i-use-the-managed-identities-for-azure-resources-vm-imds-endpoint-or-the-vm-extension-endpoint"></a>Azure リソース VM IMDS エンドポイントまたは VM 拡張エンドポイントにマネージド ID を使用する必要はありますか?

VM で Azure リソースのマネージド ID を使用する場合は、Azure リソース IMDS エンドポイントのマネージド ID を使用することをお勧めします。 Azure Instance Metadata Service は、Azure Resource Manager を使用して作成されたすべての IaaS VM にアクセスできる REST エンドポイントです。 Azure リソースのマネージド ID を IMDS 上で使用する場合、次のような利点があります:

1. すべての Azure IaaS でサポートされているオペレーティング システムは、IMDS 上で Azure リソースのマネージド ID を使用できます。 
2. Azure リソースのマネージド ID を有効にするために、VM に拡張機能をインストールする必要はなくなりました。 
3. Azure リソースのマネージド ID によって使用される証明書は、VM に存在しなくなりました。 
4. IMDS エンドポイントは、既知のルーティング不可能な IP アドレスです。VM 内でのみ使用できます。 

Azure リソース VM 拡張機能のマネージド ID は、現在でも使用可能です。ただし、今後は IMDS エンドポイントの使用が既定になります。 Azure リソース VM 拡張機能のマネージド ID は、2019 年 1 月に非推奨になります。 

Azure Instance Metadata Service の詳細については、[IMDS のドキュメント](https://docs.microsoft.com/azure/virtual-machines/windows/instance-metadata-service)を参照してください

### <a name="what-are-the-supported-linux-distributions"></a>どのような Linux ディストリビューションがサポートされていますか。

Azure IaaS でサポートされているすべての Linux ディストリビューションを、IMDS エンドポイント経由の Azure リソースのマネージド ID で使用することができます。 

注: Azure リソース VM 拡張機能のマネージド ID (2019 年 1 月に非推奨になる予定) は、次の Linux ディストリビューションのみをサポートしています:
- CoreOS Stable
- CentOS 7.1
- Red Hat 7.2
- Ubuntu 15.04
- Ubuntu 16.04

他の Linux ディストリビューションは現在サポートされておらず、サポートされていないディストリビューションでは拡張機能が失敗する可能性があります。

CentOS 6.9 では拡張機能が機能します。 ただし、6.9 はシステム サポートされていないため、クラッシュした場合や停止した場合は拡張機能が自動的に再起動しません。 6.9 は VM の再起動時に再起動します。 拡張機能を手動で再起動するには、[Azure リソース拡張機能のマネージド ID を再起動するにはどうすればよいですか?](#how-do-you-restart-the-managed-identities-for-Azure-resources-extension)を参照してください

### <a name="how-do-you-restart-the-managed-identities-for-azure-resources-extension"></a>Azure リソース拡張機能のマネージド ID を再起動するにはどうすればよいですか?
Windows と特定のバージョンの Linux で拡張機能が停止した場合は、次のコマンドレットを使用して手動で再起動できます。

```powershell
Set-AzureRmVMExtension -Name <extension name>  -Type <extension Type>  -Location <location> -Publisher Microsoft.ManagedIdentity -VMName <vm name> -ResourceGroupName <resource group name> -ForceRerun <Any string different from any last value used>
```

各値の説明: 
- Windows の拡張機能の名前と種類: ManagedIdentityExtensionForWindows
- Linux の拡張機能の名前と種類: ManagedIdentityExtensionForLinux

## <a name="known-issues"></a>既知の問題

### <a name="automation-script-fails-when-attempting-schema-export-for-managed-identities-for-azure-resources-extension"></a>Azure リソース拡張機能のマネージド ID のスキーマ エクスポートを試行すると、"自動スクリプト" が失敗する

VM で Azure リソースのマネージド ID が有効になっている場合、その VM またはリソース グループに対して "自動スクリプト" 機能を使用しようとすると、次のエラーが表示されます:

![Azure リソースのマネージド ID の自動スクリプトのエクスポート エラー](./media/msi-known-issues/automation-script-export-error.png)

現時点では、Azure リソース VM 拡張機能のマネージド ID (2019 年 1 月に非推奨になる予定) は、そのスキーマをリソース グループ テンプレートにエクスポートする機能はサポートされていません。 その結果、生成されたテンプレートには、リソース上で Azure リソースのマネージド ID を有効にする構成パラメーターは表示されません。 これらのセクションは、[テンプレート を使用して Azure VM 上で Azure リソースのマネージド ID を構成する](qs-configure-template-windows-vm.md)の例に従って手動で追加できます。

Azure リソース VM 拡張機能のマネージド ID (2019 年 1 月に非推奨になる予定) でスキーマのエクスポート機能が利用可能になると、[VM 拡張機能を含むリソース グループのエクスポート](../../virtual-machines/extensions/export-templates.md#supported-virtual-machine-extensions)の一覧に表示されます。

### <a name="configuration-blade-does-not-appear-in-the-azure-portal"></a>構成ブレードが Azure ポータルに表示されない

VM 構成ブレードが VM に表示されない場合、Azure リソースのマネージド ID はご利用のリージョンのポータルでまだ有効になっていません。  後でもう一度確認してください。  [PowerShell](qs-configure-powershell-windows-vm.md) または [Azure CLI](qs-configure-cli-windows-vm.md) を使用して、VM に Azure リソースのマネージド ID を有効にすることもできます。

### <a name="cannot-assign-access-to-virtual-machines-in-the-access-control-iam-blade"></a>Access Control (IAM) ブレードで、仮想マシンにアクセスを割り当てることができない

**仮想マシン**が Azure portal に **アクセス コントロール (IAM)** > **アクセス許可の追加** で **アクセスの割り当て先** の選択肢として表示されない場合、Azure リソースのマネージド ID がご利用のリージョンのポータルでまだ有効になっていません。 後でもう一度確認してください。  Azure リソース サービス プリンシパルのマネージド ID を検索することで、ロールの割り当ての VM の ID を選択することもできます。  **[選択]** フィールドに VM の名前を入力すると、サービス プリンシパルが検索結果に表示されます。

### <a name="vm-fails-to-start-after-being-moved-from-resource-group-or-subscription"></a>リソース グループまたはサブスクリプションから移動した後に VM を開始できない

実行中の状態で VM を移動する場合、VM は移動中も実行し続けます。 ただし、移動後に、VM を停止および再起動すると、VM を開始できなくなります。 この問題は、VM が Azure リソースのマネージド ID への参照を更新できず、以前のリソース グループでポイントし続けるために発生します。

**対処法** 
 
Azure リソースのマネージド ID の正しい値を取得できるように、VM 上で更新をトリガーします。 VM プロパティの変更を行って、Azure リソース ID のマネージド ID への参照を更新できます。 たとえば、次のコマンドを使用して、VM で新しいタグの値を設定できます。

```azurecli-interactive
 az  vm update -n <VM Name> -g <Resource Group> --set tags.fixVM=1
```
 
このコマンドは、新しいタグ "fixVM" を値 1 で VM に設定します。 
 
このプロパティの設定によって、VM は Azure リソース URI の正しいマネージド ID で更新され、VM を開始できるようになります。 
 
VM が開始されると、次のコマンドを使用してタグを削除できます。

```azurecli-interactive
az vm update -n <VM Name> -g <Resource Group> --remove tags.fixVM
```

## <a name="known-issues-with-user-assigned-identities"></a>ユーザー割り当て ID に関する既知の問題

- ユーザー割り当て ID の割り当ては、VM および VMSS に対してのみ使用できます。 重要: ユーザー割り当て ID の割り当ては、今後数か月間に変更されます。
- 同じ VM/VMSS においてユーザー割り当て ID が重複していると、VM/VMSS は失敗します。 大文字と小文字の違いだけでは重複と見なされます。 たとえば、MyUserAssignedIdentity と myuserassignedidentity などです。 
- VM に対する VM 拡張機能 (2019 年 1 月に非推奨になる予定) のプロビジョニングは、DNS 検索エラーが原因で失敗することがあります。 VM を再起動して、もう一度やり直してください。 
- "存在しない" ユーザー割り当て ID を追加すると、VM は失敗します。 
- 名前に特殊文字 (アンダースコアなど) が含まれるユーザー割り当て ID の作成はサポートされていません。
- ユーザー割り当て ID の名前は、エンド ツー エンドのシナリオで 24 文字に制限されています。 ユーザー割り当て ID の名前が 24 文字より長いと、割り当ては失敗します。
- マネージド ID 仮想マシン拡張機能 (2019 年 1 月に非推奨になる予定) を使用している場合にサポートされるユーザー割り当てマネージド ID の制限値は 32 個です。 マネージド ID 仮想マシン拡張機能を使用していない場合にサポートされる制限値は 512 です。  
- 2 番目のユーザー割り当て ID を追加すると、VM 拡張機能のトークンを要求するときに、clientID を使用できなくなる場合があります。 軽減策として、次の 2 つの bash コマンドを使用して Azure リソース VM 拡張機能のマネージド ID を再起動します:
 - `sudo bash -c "/var/lib/waagent/Microsoft.ManagedIdentity.ManagedIdentityExtensionForLinux-1.0.0.8/msi-extension-handler disable"`
 - `sudo bash -c "/var/lib/waagent/Microsoft.ManagedIdentity.ManagedIdentityExtensionForLinux-1.0.0.8/msi-extension-handler enable"`
- VM にユーザー割り当て ID がありシステム割り当て ID がない場合、ポータルの UI では、Azure リソースのマネージド ID は "無効" と表示されます。 システム割り当て ID を有効にするには、Azure Resource Manager テンプレート、Azure CLI、または SDK を使用してください。
