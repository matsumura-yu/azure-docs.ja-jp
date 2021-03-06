---
title: 制限と境界 - QnA Maker
titleSuffix: Azure Cognitive Services
description: QnA Maker における制限の包括的な一覧です。
services: cognitive-services
author: tulasim88
manager: cgronlun
ms.service: cognitive-services
ms.component: qna-maker
ms.topic: article
ms.date: 09/12/2018
ms.author: tulasim
ms.openlocfilehash: 76024266a8ae3eb03e910e140184a07ae363e881
ms.sourcegitcommit: f20e43e436bfeafd333da75754cd32d405903b07
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2018
ms.locfileid: "49384954"
---
# <a name="qna-maker-limits"></a>QnA Maker の制限
QnA Maker における制限の包括的な一覧です。

## <a name="knowledge-bases"></a>ナレッジ ベース

* [Azure Search レベルの制限](https://docs.microsoft.com/azure/search/search-limits-quotas-capacity)に基づくナレッジ ベースの最大数

|**Azure Search 層** | **Free** | **Basic** |**S1** | **S2**| **S3** |**S3 HD**|
|---|---|---|---|---|---|----|
|許可される発行済みナレッジ ベースの最大数 (最大インデックス数 - 1 (テスト用に予約済み))|2|14|49|199|199|2999|

## <a name="extraction-limits"></a>抽出の制限
* 抽出できるファイルの最大数と最大のファイル サイズ: [QnA Maker の価格](https://azure.microsoft.com/pricing/details/cognitive-services/qna-maker/)に関するページを参照してください。
* よくあるご質問の HTML ページから QnA を抽出するためにクロールできるディープリンクの最大数: 20

## <a name="metadata-limits"></a>メタデータの制限
* [Azure Search レベルの制限](https://docs.microsoft.com/azure/search/search-limits-quotas-capacity)に基づくナレッジ ベースごとのメタデータ フィールドの最大数

|**Azure Search 層** | **Free** | **Basic** |**S1** | **S2**| **S3** |**S3 HD**|
|---|---|---|---|---|---|----|
|QnA Maker サービスごとの最大のメタデータ フィールド数 (すべてのナレッジ ベースにわたって)|1,000|100*|1,000|1,000|1,000|1,000|

## <a name="knowledge-base-content-limits"></a>ナレッジ ベースのコンテンツの制限
ナレッジ ベース内のコンテンツの全体的な制限は以下のとおりです。
* 回答のテキストの長さ: 250,000
* 質問のテキストの長さ: 1,000
* メタデータのキー/値のテキストの長さ: 100
* メタデータ名でサポートされる文字: アルファベット、数字、_  
* メタデータ値でサポートされる文字: : と | を除くすべての文字 
* ファイル名の長さ: 200
* サポートされるファイル形式: ".tsv"、".pdf"、".txt"、".docx"、".xlsx"
* 代替の質問の最大数: 100
* 質問と回答のペアの最大数: 選択した [Azure Search レベル](https://docs.microsoft.com/azure/search/search-limits-quotas-capacity#document-limits)によって異なります。 

## <a name="create-knowledge-base-call-limits"></a>ナレッジ ベースの作成の呼び出しの制限
これらは、ナレッジ ベース作成操作 (つまり、*[KB を作成する]* のクリック、または CreateKnowledgeBase API の呼び出し) ごとの制限を表します。
* 回答ごとの代替の質問の最大数: 100
* URL の最大数: 10
* ファイルの最大数: 10

## <a name="update-knowledge-base-call-limits"></a>ナレッジ ベースの更新の呼び出しの制限
これらは、更新操作 (つまり、*[Save and train]\(保存してトレーニング\)* のクリック、または UpdateKnowledgeBase API の呼び出し) ごとの制限を表します。
* 各ソース名の長さ: 300
* 追加または削除される代替の質問の最大数: 100
* 追加または削除されるメタデータ フィールドの最大数: 10
* 更新可能な URL の最大数: 5
