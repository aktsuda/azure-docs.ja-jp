---
title: Azure Cosmos DB での Robomongo の使用
description: Azure Cosmos DB:MongoDB 用 API アカウントで Robomongo を使用する方法を説明します
keywords: robomongo
services: cosmos-db
author: SnehaGunda
ms.service: cosmos-db
ms.component: cosmosdb-mongo
ms.topic: conceptual
ms.date: 05/23/2017
ms.author: sngun
ms.openlocfilehash: 78f0158c9a80a60717b81b4788531c7efd979111
ms.sourcegitcommit: b0f39746412c93a48317f985a8365743e5fe1596
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2018
ms.locfileid: "52863807"
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a>Azure Cosmos DB:MongoDB 用 API アカウントで Robomongo を使用する
Robomongo を使用して Azure Cosmos DB:MongoDB 用 API アカウントに接続するには、以下を実行する必要があります。

* [Robomongo](https://robomongo.org/) をダウンロードしてインストールする
* Azure Cosmos DB:MongoDB 用 API アカウントの[接続文字列](connect-mongodb-account.md)情報を取得する

## <a name="connect-using-robomongo"></a>Robomongo を使用して接続する
Robomongo MongoDB 接続に Azure Cosmos DB:MongoDB 用 API アカウントを追加するには、次の手順を実行します。

1. Azure Cosmos DB:MongoDB 用 API アカウントの接続情報を、[ここ](connect-mongodb-account.md)に記載されている手順に従って取得します。

    ![Screen shot of the connection string blade](./media/mongodb-robomongo/connectionstringblade.png)
2. *Robomongo.exe* を実行します

3. **[ファイル]** の接続ボタンをクリックして、接続を管理します。 次に、**[MongoDB Connections (MongoDB 接続)]** ウィンドウで **[作成]** をクリックし、**[接続の設定]** ウィンドウを開きます。

4. **[接続の設定]** ウィンドウで、名前を選択します。 次に、手順 1. の接続情報の **[ホスト]** と **[ポート]** に示されている**アドレス**と**ポート**をそれぞれ入力します。

    ![Robomongo 管理接続のスクリーンショット](./media/mongodb-robomongo/manageconnections.png)
5. **[認証]** タブで **[Perform authentication (認証の実行)]** をクリックします。 次に、データベース (既定値は*Admin*)、**ユーザー名**、**パスワード**を入力します。
この**ユーザー名**と**パスワード**は両方とも、手順 1 の接続情報に示されています。

    ![[Robomongo Authentication (Robomongo 認証)] タブのスクリーンショット](./media/mongodb-robomongo/authentication.png)
6. **[SSL]** タブで、**[Use SSL protocol (SSL プロトコルを使用する)]** をオンにして、**[認証方法]** に **[自己署名証明書]** を指定します。

    ![[Robomongo SSL] タブのスクリーンショット](./media/mongodb-robomongo/SSL.png)
7. 最後に、**[テスト]** をクリックして接続できることを確認し、**[保存]** をクリックします。

## <a name="next-steps"></a>次の手順
* Azure Cosmos DB:MongoDB 用 API の[サンプル](mongodb-samples.md)を確認します。
