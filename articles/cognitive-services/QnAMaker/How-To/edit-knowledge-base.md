---
title: ナレッジ ベースの編集 - QnA Maker
titleSuffix: Azure Cognitive Services
description: QnA Maker では、使いやすい編集環境で、ナレッジ ベースのコンテンツを管理することができます。
services: cognitive-services
author: tulasim88
manager: cgronlun
ms.service: cognitive-services
ms.component: qna-maker
ms.topic: article
ms.date: 09/12/2018
ms.author: tulasim
ms.openlocfilehash: f927e5b7ff65b82aef9d4224d22296e0fa48ad59
ms.sourcegitcommit: f31bfb398430ed7d66a85c7ca1f1cc9943656678
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47451886"
---
# <a name="edit-a-knowledge-base"></a>ナレッジ ベースの編集

QnA Maker では、使いやすい編集環境で、ナレッジ ベースのコンテンツを管理することができます。

## <a name="edit-your-knowledge-base-content"></a>ナレッジ ベースのコンテンツの編集

1.  上部のナビゲーション バーにある **[My knowledge bases]\(マイ ナレッジ ベース\)** を選択します。 

    自分が作成したサービスと他のユーザーから共有されたサービスが、**最終更新日**の降順ですべて表示されます。

    ![[My knowledge bases]\(マイ ナレッジ ベース\)](../media/qnamaker-how-to-edit-kb/my-kbs.png)

2. 編集する特定のナレッジ ベースを選択します。
 
3. **[設定]** をクリックします。

   ここでは、必須フィールドの [サービス名] を編集できます。
  
   **[Manage knowledgebase]\(ナレッジ ベースの管理\) -> [+ Add URL]\(+ URL の追加\)** リンクをクリックして、新しい FAQ コンテンツをナレッジ ベースに追加するために新しい URL を追加できます。
   
   **削除アイコン**をクリックして既存の URL を削除できます。
   
   ナレッジ ベースで既存の URL の最新の内容をクロールする場合、**[更新]** チェック ボックスをオンにします。これにより、ナレッジ ベースが最新の URL コンテンツで更新されます。
   
**[Manage knowledgebase]\(ナレッジ ベースの管理\) -> [+ Add File]\(+ ファイルの追加\)** をクリックして、サポートされているファイル ドキュメントをナレッジ ベースの一部として追加できます。

**[Ímport Knowledgebase]\(ナレッジ ベースのインポート\)** ボタンをクリックして、既存のナレッジ ベースをインポートすることもできます。 
   
ナレッジ ベースの更新は、ナレッジ ベースと関連付けられた QnA Maker サービスの作成中に使用している**管理価格レベル**によって異なります。 必要な場合、Azure portal から管理レベルを更新することもできます。

4. ナレッジ ベースに変更を加えた後、その変更を保持するには、ページの右上隅にある **[Save and train]\(保存してトレーニング\)** をクリックします。    

    ![[Save and train]\(保存してトレーニング\)](../media/qnamaker-how-to-edit-kb/save-and-train.png)

    >[!NOTE]
    [Save and train]\(保存してトレーニング\) をクリックせずにこのページから離れた場合、変更内容は保持されません。

## <a name="add-a-qna-pair"></a>QnA ペアの追加

ナレッジ ベースのテーブルに新しい行を追加するには、**[Add QnA pair]\(QnA ペアの追加\)** を選択します。

![[Add QnA pair]\(QnA ペアの追加\)](../media/qnamaker-how-to-edit-kb/add-qnapair.png)

## <a name="delete-a-qna-pair"></a>QnA ペアの削除

QnA を削除するには、QnA 行の右端にある**削除**アイコンをクリックします。

![QnA ペアの削除](../media/qnamaker-how-to-edit-kb/delete-qnapair.png)

## <a name="add-alternate-questions"></a>代わりの質問を追加する

既存の QnA ペアに代わりの質問を追加すること (別の表現で言い換えること) で、ユーザーからの問い合わせに一致する可能性が向上します。

![代わりの質問を追加する](../media/qnamaker-how-to-edit-kb/add-alternate-question.png)

## <a name="add-metadata"></a>メタデータの追加


フィルター アイコンを選択してメタデータ ペアを追加します。

![メタデータの追加](../media/qnamaker-how-to-edit-kb/add-metadata.png)

> [!TIP]
> 編集を行った後は、変更内行が失われないよう、ナレッジ ベースの保存とトレーニングを定期的に実行してください。

## <a name="manage-large-knowledge-bases"></a>大きなナレッジ ベースの管理

1. QnA は、抽出元のデータ ソースごとに**グループ化**されます。 データ ソースは、展開したり折りたたんだりすることができます。
2. ナレッジ ベースの**検索**は、ナレッジ ベース テーブルの一番上にあるテキスト ボックスに検索語句を入力することで実行できます。 Enter キーを押すと、質問、回答、またはメタデータの内容を対象に検索が実行されます。 検索フィルターを解除するには、X アイコンをクリックします。
3. 大きなナレッジ ベースは、**改ページ**で管理することができます。

    ![検索、改ページ、グループ化](../media/qnamaker-how-to-edit-kb/search-paginate-group.png)

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [ナレッジ ベースの共同作業](./collaborate-knowledge-base.md)
