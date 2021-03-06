---
title: インクルード ファイル
description: インクルード ファイル
services: virtual-machines-windows
author: cynthn
ms.service: virtual-machines-windows
ms.topic: include
ms.date: 10/23/2018
ms.author: cynthn
ms.custom: include file
ms.openlocfilehash: e7dfd7d2a0363a95acb76a5dc214dbd4036de11d
ms.sourcegitcommit: ada7419db9d03de550fbadf2f2bb2670c95cdb21
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2018
ms.locfileid: "50973861"
---
各エンドポイントには、*パブリック ポート*と*プライベート ポート*があります。

* パブリック ポートは、インターネットから仮想マシンに発信される着信トラフィックをリッスンするときに、Azure Load Balancer によって使用されます。
* プライベート ポートは、一般的に仮想マシンで実行されているアプリケーションまたはサービスを宛先とする着信トラフィックをリッスンする仮想マシンによって使用されます。

Azure ポータルでエンドポイントを作成するときに、周知のネットワーク プロトコルの IP プロトコルと、TCP ポートまたは UDP ポートの既定値が提示されます。 カスタム エンドポイントの場合、正しい IP プロトコル (TCP または UDP) と、パブリック ポートとプライベート ポートを指定します。 着信トラフィックを複数の仮想マシンにランダムに分散するには、複数のエンドポイントで構成される負荷分散セットを作成します。

エンドポイントを作成した後、アクセス制御リスト (ACL) を使用して、発信元 IP アドレスに基づいて、エンドポイントのパブリック ポートを宛先とする着信トラフィックの許可または拒否に役立つルールを定義できます。 ただし、仮想マシンが Azure Virtual Network 内にある場合、ネットワーク セキュリティ グループを代わりに使用します。 詳細については、「 [ネットワーク セキュリティ グループについて](../articles/virtual-network/security-overview.md)」をご覧ください。

> [!NOTE]
> Azure が自動で設定するリモート接続エンドポイントに関連付けられているポートに対して、Azure 仮想マシンのファイアウォール構成が自動的に行われます。 他のすべてのエンドポイントに対して指定されているポートについては、仮想マシンのファイアウォールは自動的には構成されません。 仮想マシンにエンドポイントを作成するとき、仮想マシンのファイアウォールで、エンドポイントの構成に対応するプロトコルとプライベート ポートでトラフィックが許可されていることを確認します。 ファイアウォールを構成するには、仮想マシンで実行しているオペレーティング システムの文書またはオンライン ヘルプを参照してください。
>
>

## <a name="create-an-endpoint"></a>エンドポイントの作成
1. [Azure Portal](https://portal.azure.com) にサインインします。

2. **[仮想マシン]** をクリックし、構成する仮想マシンを選択します。

3. **[設定]** グループで **[エンドポイント]** を選択します。 仮想マシンの現在のすべてのエンドポイントが表示されている **[エンドポイント]** ページが表示されます。 (この例は Windows VM のものです。 Linux VM の場合、SSH のエンドポイントが既定で表示されます。)

   <!-- ![Endpoints](./media/virtual-machines-common-classic-setup-endpoints/endpointswindows.png) -->
   ![エンドポイント](./media/virtual-machines-common-classic-setup-endpoints/endpointsblade.png)


4. エンドポイントのエントリの上部にあるコマンド バーで、**[追加]** を選択します。 **[エンドポイントの追加]** ページが表示されます。

5. **[名前]** に、エンドポイントの名前を入力します。

6. **[プロトコル]** に、**[TCP]** または **[UDP]** のどちらかを選択します。

7. **[パブリック ポート]** に、インターネットからのトラフィックが着信するポート番号を入力します。 

8. **[プライベート ポート]** に、仮想マシンがリッスンするポート番号を入力します。 パブリック ポートとプライベート ポートには異なる番号を指定できます。 プロトコルとプライベート ポートに対応するトラフィックを許可するように、仮想マシン上のファイアウォールが構成されていることを確認します。

9. **[OK]** を選択します。

新しいエンドポイントが **[エンドポイント]** ページの一覧に表示されます。

![エンドポイントの作成に成功](./media/virtual-machines-common-classic-setup-endpoints/endpointcreated.png)

## <a name="manage-the-acl-on-an-endpoint"></a>エンドポイントの ACL の管理
トラフィックを送信できるコンピューターを定義するために、エンドポイント上の ACL によって、発信元 IP アドレスに基づいてトラフィックを制限できます。 エンドポイントの ACL を追加、変更、削除するには、次のステップに従います。

> [!NOTE]
> エンドポイントが負荷分散セットの一部である場合、エンドポイントの ACL に対して行った変更はそのセット内のすべてのエンドポイントに適用されます。
>
>

仮想マシンが Azure Virtual Network 内にある場合、ACL の代わりにネットワーク セキュリティ グループを使用します。 詳細については、「 [ネットワーク セキュリティ グループについて](../articles/virtual-network/security-overview.md)」をご覧ください。

1. Azure ポータルにサインインします。

2. **[仮想マシン]** を選択し、構成する仮想マシンの名前を選択します。

3. **[エンドポイント]** を選択します。 エンドポイントの一覧から適切なエンドポイントを選択します。 ページの下部に ACL リストがあります。

   ![[HTTPS エンドポイントの ACL の詳細の指定]](./media/virtual-machines-common-classic-setup-endpoints/aclpreentry.png)

4. 一覧内の行を使用して、ACL のルールの追加、削除、編集を行い、順序を変更します。 **[リモート サブネット]** の値は、インターネットからのトラフィックを着信する IP アドレスの範囲です。Azure Load Balancer では、この値を使用して、発信元 IP アドレスに基づいてトラフィックを許可または拒否します。 IP アドレスの範囲は、クラスレス ドメイン間ルーティング (CIDR) 形式 (アドレス プレフィックス形式とも呼ばれる) で指定してください。 たとえば、「 `10.1.0.0/8` 」のように入力します。

 ![新しい ACL エントリ](./media/virtual-machines-common-classic-setup-endpoints/newaclentry.png)


ルールを使用して、インターネット上のご使用のコンピューターに該当する特定のコンピューターから発信されるトラフィックのみを許可したり、特定の範囲の既知のアドレスから発信されるトラフィックを拒否したりすることができます。

ルールの評価は、一覧の最初に示されているルールから開始され、最後に示されているルールで終了します。 そのため、一覧には、制限の最も少ないルールから制限の最も多いルールの順に整列されている必要があります。 詳細については、[ネットワーク アクセス制御リストの概要](../articles/virtual-network/virtual-networks-acl.md)に関するページを参照してください。
