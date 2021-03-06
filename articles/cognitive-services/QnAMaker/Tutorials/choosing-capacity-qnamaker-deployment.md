---
title: デプロイのリソース容量 - QnA Maker
titleSuffix: Azure Cognitive Services
description: QnA Maker サービスを作成する前に、前述したサービスに関して、どのレベルが現状に適しているかを判断する必要があります。
services: cognitive-services
author: tulasim88
manager: cgronlun
ms.service: cognitive-services
ms.component: qna-maker
ms.topic: article
ms.date: 09/12/2018
ms.author: tulasim
ms.custom: seodec18
ms.openlocfilehash: 9e197929ce08f4e0c665f96d1c4ddbd382fdfb22
ms.sourcegitcommit: 9fb6f44dbdaf9002ac4f411781bf1bd25c191e26
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2018
ms.locfileid: "53084459"
---
# <a name="choosing-capacity-for-your-qna-maker-deployment"></a>QnA Maker のデプロイに使用する容量の選択

QnA Maker サービスは、次の 3 つの Azure リソースに依存しています。
1.  App Service (ランタイム用)
2.  Azure Search (QnA の格納用)
3.  App Insights (省略可能。チャット ログとテレメトリの格納用)

QnA Maker サービスを作成する前に、前述したサービスに関して、どのレベルが現状に適しているかを判断する必要があります。 

通常、次の 3 つのパラメーターを考慮する必要があります。
1. **サービスに必要なスループット**: App Service の適切な[アプリ プラン](https://azure.microsoft.com/pricing/details/app-service/plans/)を、実際のニーズに基づいて選択します。 アプリは[スケールアップ](https://docs.microsoft.com/azure/app-service/web-sites-scale)またはスケールダウンすることができます。 この点は、Azure Search の SKU の選択にも影響します。詳細については、[こちら](https://docs.microsoft.com/azure/search/search-sku-tier)を参照してください。

2. **ナレッジ ベースのサイズと数**: 実際のシナリオに合った適切な [Azure Search SKU](https://azure.microsoft.com/pricing/details/search/) を選択してください。 特定のレベルで発行できるナレッジ ベースの数は N-1 件です (N は、そのレベルで許容される最大インデックス)。 レベルごとに許容されるドキュメントの最大サイズと最大数もチェックしてください。

3. **ソースとしてのドキュメントの数**: QnA Maker 管理サービスの無料の SKU では、ポータルと API で管理できるドキュメントの数が 3 つ (サイズはそれぞれ 1 MB) に限定されます。 Standard SKU では、管理できるドキュメントの数に制限はありません。 詳細については、[こちら](https://aka.ms/qnamaker-pricing)を参照してください。

次の表は、いくつかの基本的なガイドラインを示したものです。

|                        | QnA Maker 管理 | App Service | Azure Search | 制限事項                      |
| ---------------------- | -------------------- | ----------- | ------------ | -------------------------------- |
| 実験        | 無料の SKU             | Free レベル   | Free レベル    | 発行できる KB は 2 つまで (最大サイズ 50 MB)  |
| 開発/テスト環境   | Standard SKU         | 共有      | Basic        | 発行できる KB は 14 個まで (最大サイズ 2 GB)    |
| 運用環境 | Standard SKU         | Basic       | 標準     | 発行できる KB は 49 個まで (最大サイズ 25 GB) |

QnA Maker スタックのアップグレードについては、「[QnA Maker サービスのアップグレード](../How-To/upgrade-qnamaker-service.md)」を参照してください。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [QnA Maker サービスのアップグレード](../How-To/upgrade-qnamaker-service.md)
