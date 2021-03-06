---
title: Azure ストレージ アカウント名のエラー | Microsoft Docs
description: ストレージ アカウント名を指定する際に発生する可能性のあるエラーについて説明します。
services: azure-resource-manager
documentationcenter: ''
author: tfitzmac
manager: timlt
editor: ''
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: troubleshooting
ms.date: 03/09/2018
ms.author: tomfitz
ms.openlocfilehash: da7147439bba668c6c614c19d91a22ee78275c69
ms.sourcegitcommit: b6319f1a87d9316122f96769aab0d92b46a6879a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2018
ms.locfileid: "34357345"
---
# <a name="resolve-errors-for-storage-account-names"></a>ストレージ アカウント名のエラーの解決

この記事では、ストレージ アカウントをデプロイする際に発生する可能性のある名前付けに関するエラーについて説明します。

## <a name="symptom"></a>症状

ストレージ アカウント名に禁止文字が含まれる場合、次のようなエラーが表示されます。

```
Code=AccountNameInvalid
Message=S!torageckrexph7isnoc is not a valid storage account name. Storage account name must be 
between 3 and 24 characters in length and use numbers and lower-case letters only.
```

ストレージ アカウントには、Azure 全体で一意であるリソースの名前を指定する必要があります。 一意の名前を指定しないと、次のようなエラーが発生します。

```
Code=StorageAccountAlreadyTaken
Message=The storage account named mystorage is already taken.
```

ストレージ アカウントをデプロイするとき、ご利用のサブスクリプションに既に存在するストレージ アカウントと同じ名前を使用したうえで別の場所にデプロイすると、ストレージ アカウントが既に別の場所に存在しているというエラーが表示されます。 既存のストレージ アカウントを削除するか、既存のストレージ アカウントと同じ場所を指定してください。

## <a name="cause"></a>原因

ストレージ アカウント名の長さは 3 ～ 24 文字で、数字と小文字のみを使用する必要があります。 名前は一意である必要があります。

## <a name="solution"></a>解決策

ストレージ アカウント名は必ず一意にしてください。 一意の名前を作成するには、使用している命名規則に、 [uniqueString](resource-group-template-functions-string.md#uniquestring) 関数の結果を連結します。

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

ストレージ アカウント名が 24 文字を超えないようにしてください。 [uniqueString](resource-group-template-functions-string.md#uniquestring) 関数は 13 文字を返します。 **uniqueString** の結果にプレフィックスまたはポストフィックスを連結する場合は、11 文字以下の値を指定してください。

```json
"parameters": {
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "The value to use for starting the storage account name."
      }
    }
}
```

ストレージ アカウント名には、大文字や特殊文字を含めないでください。