---
title: Azure Stack の主要な機能と概念 | Microsoft Docs
description: Azure Stack の主要な機能と概念について説明します。
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: 09ca32b7-0e81-4a27-a6cc-0ba90441d097
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/10/2018
ms.author: jeffgilb
ms.reviewer: ''
ms.openlocfilehash: 21a6eeb4b0a83574be4c5c996e43d9867c3249d0
ms.sourcegitcommit: 5b869779fb99d51c1c288bc7122429a3d22a0363
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2018
ms.locfileid: "53185734"
---
# <a name="key-features-and-concepts-in-azure-stack"></a>Azure Stack の主要な機能と概念
Microsoft Azure Stack を初めて使う場合は、次の用語と機能の説明を参考にしてください。

## <a name="personas"></a>ペルソナ
Microsoft Azure Stack には、オペレーターとユーザーという 2 種類のユーザーが存在します。

* Azure Stack **オペレーター**は、Azure Stack を構成し、オファー、プラン、サービス、クォータ、および価格を管理して、テナント ユーザーにリソースを提供できます。 さらに、オペレーターは、容量を管理し、アラートに対処します。  
* Azure Stack **ユーザー** (テナントとも呼ばれます) は、オペレーターが提供するサービスを使用します。 ユーザーは、サブスクライブしたサービス (Web アプリ、Storage、Virtual Machines など) のプロビジョニング、監視、管理を行うことができます。

## <a name="portal"></a>ポータル
Microsoft Azure Stack を操作する主な方法は、管理ポータル、ユーザー ポータル、および PowerShell です。

Azure Stack のポータルは、それぞれが Azure Resource Manager の個別のインスタンスでサポートされています。 オペレーターは、管理ポータルを使用して Azure Stack を管理し、テナントに提供するサービスの作成などの処理を行います。 ユーザー ポータル (テナント ポータルとも呼ばれます) は、仮想マシンやストレージ アカウント、Web アプリなどのクラウド リソースを消費するためのセルフ サービス エクスペリエンスを提供します。 詳細については、「[Using the Azure Stack administrator and user portals](azure-stack-manage-portals.md)」(Azure Stack の管理者ポータルとユーザーポータルの使用) を参照してください。

## <a name="identity"></a>ID 
Azure Stack は、ID プロバイダーとして Azure Active Directory (Azure AD) または Active Directory フェデレーション サービス (AD FS) のいずれかを使用します。  

### <a name="azure-active-directory"></a>Azure Active Directory
Azure AD は、マイクロソフトが提供するクラウドベースのマルチテナント対応 ID プロバイダーです。 ほとんどのハイブリッド シナリオでは、ID ストアとして Azure AD を使用します。

### <a name="active-directory-federation-services"></a>Active Directory フェデレーション サービス (AD FS)
Azure Stack のオフラインでの展開に Active Directory フェデレーション サービス (AD FS) を使用することを選択できます。 Azure Stack、リソース プロバイダー、およびその他のアプリケーションは、Azure AD を使用するのとほぼ同じ方法で AD FS を使用します。 Azure Stack には、独自の Active Directory インスタンスと、Active Directory Graph API が含まれています。 Azure Stack Development Kit は、次の AD FS シナリオをサポートします。

- AD FS を使用して展開にサインインする
- Key Vault 内のシークレットを使用して仮想マシンを作成する
- シークレットを格納/アクセスするためのコンテナーを作成する
- サブスクリプション内にカスタム RBAC ロールを作成する
- リソースの RBAC ロールにユーザーを割り当てる
- Azure PowerShell を使用してシステム全体の RBAC ロールを作成する
- Azure PowerShell を使用してユーザーとしてサインインする
- サービス プリンシパルを作成し、それらを使用して Azure PowerShell にサインインする


## <a name="regions-services-plans-offers-and-subscriptions"></a>リージョン、サービス、プラン、オファー、およびサブスクリプション
Azure Stack では、リージョン、サブスクリプション、オファー、およびプランを使用してサービスがテナントに提供されます。 テナントは複数のオファーにサブスクライブできます。 オファーは 1 つまたは複数のプランを含むことができ、プランは 1 つまたは複数のサービスを含むことができます。

![](media/azure-stack-key-features/image4.png)

テナントによるオファーへのサブスクリプションを階層で示した例 (各オファーに異なるプランやサービスが含まれる)。

### <a name="regions"></a>リージョン
Azure Stack のリージョンは、スケールと管理の基本要素です。 組織は、複数のリージョンを用意することができ、各リージョンでリソースを利用可能にできます。 リージョンごとに異なるサービスを利用可能にすることもできます。 Azure Stack Development Kit では単一のリージョンのみがサポートされ、自動的に *local* という名前が与えられます。

### <a name="services"></a>サービス
Microsoft Azure Stack によって、プロバイダーは、仮想マシンや SQL Server データベース、SharePoint、Exchange などの多種多様なアプリケーションやサービスを提供できます。

### <a name="plans"></a>プラン
プランは、1 つまたは複数のサービスをグループ化したものです。 プロバイダーは、テナントに提供するプランを作成します。 作成されたオファーテナントがサブスクライブし、オファーに含まれるプランとサービスを使用します。

プランに追加するサービスごとにクォータの設定を構成できるため、クラウドの容量を管理するのに便利です。 クォータには、VM、RAM、CPU の上限などの制限が含まれており、ユーザー サブスクリプションごとに適用されます。 クォータは、場所によって区別できます。 たとえば、リージョン A のコンピューティング サービスを含むプランには、2 台の仮想マシン、4 GB の RAM、10 個の CPU コアで構成されるクォータを設定できます。

オファーを作成するときに、サービス管理者は**基本プラン**を含めることができます。 テナントがそのプランにサブスクライブすると、基本プランが既定で組み込まれます。 ユーザーは、サブスクライブする (サブスクリプションが作成される) と、基本プランに指定されたすべてのリソース プロバイダーにアクセスできます (対応するクォータが適用されます)。

サービス管理者は、オファーに **アドオン プラン** を含めることもできます。 既定では、サブスクリプションにアドオン プランは含まれません。 アドオン プランは、サブスクリプションの所有者が自分のサブスクリプションに付加できる、オファー内の利用可能な追加プラン (クォータ) です。

### <a name="offers"></a>オファー
オファーは、プロバイダーから提示されてテナントが購入 (サブスクライブ) する、1 つまたは複数のプランをグループ化したものです。 たとえば、Alpha というオファーには、一連のコンピューティング サービスを含むプラン A と、一連のストレージ サービスとネットワーク サービスを含むプラン B を含めることができます。

オファーには一連の基本プランが既定で含まれていますが、サービス管理者はアドオン プランを作成でき、テナントはアドオン プランをサブスクリプションに追加できます。

### <a name="subscriptions"></a>サブスクリプション
サブスクリプションは、テナントがオファーを購入する方法です。 また、サブスクリプションはテナントとオファーの組み合わせです。 テナントは複数のオファーへのサブスクリプションを行うことができます。 各サブスクリプションは 1 つのプランだけに適用されます。 サブスクリプションによって、テナントがアクセスできるプランやサービスが決定します。

サブスクリプションは、プロバイダーがクラウドのリソースやサービスを整理してアクセスするために便利です。

管理者に対して、デプロイ中に既定のプロバイダー サブスクリプションが作成されます。 このサブスクリプションを使用して、Azure Stack の管理、他のリソース プロバイダのデプロイ、およびテナント向けのプランとオファーの作成を実行できます。 このサブスクリプションは、顧客ワークロードとアプリケーションを実行するために使用すべきではありません。 バージョン 1804 以降、2 つのサブスクリプションが既定のプロバイダー サブスクリプションに補足として追加されました。測定サブスクリプションと消費サブスクリプションです。 この追加によって、コア インフラストラクチャ、追加リソース プロバイダー、ワークロードの分割管理が容易になります。  

## <a name="azure-resource-manager"></a>Azure Resource Manager
Azure Resource Manager を使用することで、インフラストラクチャのリソースをテンプレート ベースの宣言型モデルで操作できます。   それは、ソリューション コンポーネントのデプロイと管理に使用できる単一のインターフェイスを備えています。 詳しい説明とガイダンスについては、「[Azure Resource Manager の概要](../azure-resource-manager/resource-group-overview.md)」を参照してください。

### <a name="resource-groups"></a>リソース グループ
リソース グループは、リソース、サービス、およびアプリケーションのコレクションであり、各リソースには、仮想マシン、仮想ネットワーク、パブリック IP、ストレージ アカウント、Web サイトなどの種類があります。 各リソースは、リソース グループに属する必要があります。このため、リソース グループを使用して、ワークロード別や場所別などにリソースを論理的に整理できます。 Azure Stack では、プランやオファーなどのリソースもリソース グループで管理されます。

[Azure](../azure-resource-manager/resource-group-move-resources.md) とは異なり、リソース グループ間で Azure Stack リソースを移動することはできません。 Azure Stack 管理ポータルでリソースまたはリソース グループのプロパティを表示すると、*[移動]* ボタンが淡色表示となり、クリックできません。 さらに、リソース グループまたはリソース グループ項目のプロパティからの**リソース グループの変更**または**サブスクリプションの変更**アクションの使用もサポートされていません。 試行されたすべて移動操作は失敗します。
 
### <a name="azure-resource-manager-templates"></a>Azure Resource Manager のテンプレート
Azure Resource Manager を使用して、アプリケーションのデプロイと構成を定義する (JSON 形式の) テンプレートを作成できます。 このテンプレートは Azure リソース マネージャー テンプレートと呼ばれ、デプロイメントの定義を宣言できます。 テンプレートを使用すると、アプリケーションをアプリのライフサイクルを通して繰り返しデプロイできるほか、常にリソースが一貫した状態でデプロイされます。

## <a name="resource-providers-rps"></a>リソース プロバイダー (RP)
リソース プロバイダーは、Azure ベースのあらゆる IaaS サービスと PaaS サービスの基盤となる Web サービスです。 Azure Resource Manager は、さまざまな RP を使用してサービスへのアクセスを提供します。

これには次の 4 つの基本的な RP があります。ネットワーク、ストレージ、コンピューティング、および KeyVault です。 各 RP を使用して、それぞれのリソースを構成および制御できます。 サービス管理者は、新しいカスタム リソース プロバイダーを追加することもできます。

### <a name="compute-rp"></a>コンピューティング RP
コンピューティング リソース プロバイダー (CRP) では、Azure Stack テナントが独自の仮想マシンを作成できます。 CRP には、仮想マシンと仮想マシン拡張機能を作成する機能があります。 仮想マシン拡張機能サービスは、Windows および Linux の仮想マシンで使用する IaaS 機能を提供します。  たとえば、CRP を使用して Linux 仮想マシンをプロビジョニングし、デプロイ中に Bash スクリプトを実行して VM を構成できます。

### <a name="network-rp"></a>ネットワーク RP
ネットワーク リソース プロバイダー (NRP) は、プライベート クラウドでソフトウェアによるネットワーク制御 (SDN) およびネットワーク機能の仮想化 (NFV) に使用する一連の機能を提供します。  NRP を使用して、ソフトウェア ロード バランサー、パブリック IP、ネットワーク セキュリティ グループ、仮想ネットワークなどのリソースを作成できます。

### <a name="storage-rp"></a>ストレージ RP
ストレージ RP は、Azure との一貫性があるストレージ サービス (BLOB、テーブル、キュー、およびアカウント管理) を提供します。 Azure との一貫性があるストレージ サービスのサービス プロバイダーによる管理を容易にするためのストレージ クラウド管理サービスも提供します。 Azure Storage には柔軟性があり、ドキュメントやメディア ファイルなどの大量の構造化されていないデータは Azure Blobs で、構造化された NoSQL ベースのデータは Azure Tables で格納と取得が行われます。 Azure Storage の詳細については、「[Microsoft Azure Storage の概要](../storage/common/storage-introduction.md)」をご覧ください。

#### <a name="blob-storage"></a>BLOB ストレージ
BLOB ストレージには、あらゆるデータ セットが格納されます。 ドキュメント、メディア ファイル、アプリケーション インストーラーなど、任意の種類のテキスト データやバイナリ データを BLOB として保存できます。 テーブル ストレージには、構造型データが格納されます。 テーブル ストレージは、NoSQL キー属性データ ストアであるため、開発が迅速化され、大量のデータにすばやくアクセスできます。 キュー ストレージは、ワークフロー処理およびクラウド サービスのコンポーネント間通信のための、信頼性の高いメッセージング機能を提供します。

すべての BLOB はコンテナーに編成されます。 コンテナーを使用すると、オブジェクトのグループにセキュリティ ポリシーを便利に割り当てることができます。 ストレージ アカウントの容量の上限である 500 TB (テラバイト) を超えない限り、ストレージ アカウントには任意の数のコンテナーを含めることができ、コンテナーには任意の数の BLOB を含めることができます。 BLOB ストレージが提供する BLOB には、ブロック BLOB、追加 BLOB、ページ BLOB (ディスク) の 3 種類があります。 ブロック BLOB はストリーミングとクラウド オブジェクトの格納に最適化されているので、ドキュメント、メディア ファイル、バックアップなどの格納に適しています。追加 BLOB はブロック BLOB に似ていますが、追加操作用に最適化されています。 追加 BLOB は、新しいブロックを最後に追加することによってのみ更新できます。 追加 BLOB は、新しいデータが BLOB の最後のみに書き込まれる必要がある、ログ記録のようなシナリオに適しています。 ページ BLOB は、IaaS ディスクとして使用でき、ランダムな書き込みをサポートするように最適化され、最大 1 TB (テラバイト) まで拡大できます。 Azure 仮想マシン ネットワークに設置された IaaS ディスクは、ページ BLOB として格納される VHD です。

#### <a name="table-storage"></a>テーブル ストレージ
テーブル ストレージは、Microsoft の NoSQL キー属性ストアですが、従来のリレーショナル データベースと異なり、スキーマがない設計です。 データ ストアのスキーマがないため、アプリケーションの進化のニーズに合わせてデータを容易に修正できます。 テーブル ストレージは使いやすいため、開発者はアプリケーションを迅速に作成できます。 テーブル ストレージは、キー属性ストアであるため、テーブル内のすべての値に型指定されたプロパティ名が付いて保存されます。 このプロパティ名は、フィルタリングや、選択条件の指定に使用できます。 1 つのエンティティは、一連のプロパティとその値で構成されます。 テーブル ストレージはスキーマがないため、同じテーブル内の 2 つのエンティティが異なるコレクションのプロパティを持つことができ、それらのプロパティに異なる型を使用できます。 テーブル ストレージを使用すると、Web アプリケーションのユーザー データ、アドレス帳、デバイス情報、およびサービスに必要なその他の種類のメタデータなど、柔軟なデータセットを保存できます。 ストレージ アカウントの容量の上限を超えない限り、テーブルには任意の数のエンティティを保存でき、ストレージ アカウントには任意の数のテーブルを含めることができます。

#### <a name="queue-storage"></a>Queue Storage
Azure Queue Storage は、アプリケーション コンポーネント間のクラウド メッセージングを提供します。 拡張性を重視してアプリケーションを設計する場合、通常、アプリケーション コンポーネントを個別に拡張できるように分離します。 Queue Storage は、アプリケーション コンポーネントがクラウド、デスクトップ、オンプレミスのサーバー、モバイル デバイスのいずれで実行されている場合でも、アプリケーション コンポーネント間の通信に非同期メッセージングを提供します。 Queue Storage ではまた、非同期タスクの管理とプロセス ワークフローの構築もサポートします。

### <a name="keyvault"></a>KeyVault
KeyVault RP は、パスワードや証明書などのシークレットの管理と監査を提供します。 たとえば、テナントは、KeyVault RP を使用して、VM のデプロイ中に管理者のパスワードやキーを指定できます。

## <a name="high-availability-for-azure-stack"></a>Azure Stack の高可用性
*適用対象: Azure Stack 1802 以降のバージョン*

Azure でのマルチ VM による実稼働システムの高可用性を実現するため、VM は、複数の障害ドメインと更新ドメインに分散される可用性セットに配置されます。 この方法では、次の図に示すように[可用性セットにデプロイされた VM](https://docs.microsoft.com/azure/virtual-machines/windows/tutorial-availability-sets) が複数のサーバー ラックに互いに物理的に分離され、障害からの回復性が考慮されています。

  ![Azure Stack の高可用性](media/azure-stack-key-features/high-availability.png)

### <a name="availability-sets-in-azure-stack"></a>Azure Stack の可用性セット
Azure Stack のインフラストラクチャは既に障害に対する回復性を備えていますが、基盤となっているテクノロジ (フェールオーバー クラスタリング) では、ハードウェアが故障した場合にその影響を受ける物理サーバー上の VM に多少のダウンタイムが発生します。 Azure Stack では、Azure との一貫性がある最大 3 つの障害ドメインを持つ可用性セットを用意することをサポートしています。

- **障害ドメイン**。 可用性セットに配置された VM は、複数の障害ドメイン (Azure Stack ノード) にできる限り均等に分散させることによって、互いに物理的に分離されます。 ハードウェアが故障した場合、障害が発生した障害ドメインの VM は他の障害ドメインで再起動されますが、可能であれば、同じ可用性セット内の他の VM とは別の障害ドメインに保持されます。 ハードウェアがオンラインに戻ると、高可用性を維持するために VM の再分配が行われます。 
 
- **更新ドメイン**。 更新ドメインは、可用性セットに高可用性を提供する Azure の別の概念です。 更新ドメインは、メンテナンスを同時に実行できる、基盤となるハードウェアの論理グループです。 同じ更新ドメイン内の VM は、計画済みメンテナンス中に同時に再起動されます。 テナントが可用性セット内に VM を作成すると、Azure プラットフォームは、これらの更新ドメインに VM を自動的に分散します。 Azure Stack では、VM のホストが更新される前に、クラスター内の他のオンライン ホストに VM がライブで移行されます。 ホスト更新中のテナントのダウンタイムはないため、Azure Stack の更新ドメイン機能は、Azure とのテンプレートの互換性を保つためにのみ存在します。 

### <a name="upgrade-scenarios"></a>アップグレードのシナリオ 
Azure Stack バージョン 1802 より前に作成された可用性セット内の VM には、既定数の障害ドメインと更新ドメインが与えられています (前者は 1、後者は 1)。 既存の可用性セット内の VM に対する高可用性を実現するには、既存の VM を削除した後、「[Windows VM の可用性セットの変更](https://docs.microsoft.com/azure/virtual-machines/windows/change-availability-set)」の説明に従って、適切な数の障害ドメインと更新ドメインを持つ新しい可用性セットに再デプロイする必要があります。 

仮想マシン スケール セット用の可用性セットは、既定数の障害ドメインと更新ドメイン (前者は 3、後者は 5) で内部的に作成されます。 1802 更新プログラムより前に作成されたすべての仮想マシン スケール セットは、既定数の障害ドメインと更新ドメイン (前者は 1、後者は 1) を持つ可用性セットに配置されます。 これらの仮想マシン スケール セット インスタンスを新しく分散されるように更新するには、1802 更新プログラムより前に存在していたインスタンス数によって仮想マシン スケール セットをスケール アウトした後、仮想マシン スケール セットの古いインスタンスを削除します。 

## <a name="role-based-access-control-rbac"></a>ロールベースの Access Control (RBAC)
RBAC を使用して、承認されたユーザー、グループ、およびサービスに対してサブスクリプション、リソース グループ、または個々のリソース レベルでロールを割り当てることによって、システムへのアクセスを許可することができます。 各ロールは、Microsoft Azure Stack のリソースに対するユーザー、グループ、またはサービスのアクセス レベルを定義します。

Azure RBAC には、すべてのリソースの種類に適用される 3 つの基本的なロールがあります。所有者、共同作成者、および閲覧者です。 所有者は、他のユーザーへアクセス権を委任する権限を含め、すべてのリソースへのフル アクセス権を持ちます。 作成協力者は、Azure リソースのすべてのタイプを作成および管理できますが、他のユーザーへアクセス権を付与することはできません。 閲覧者は、既存の Azure リソースを表示できるのみです。 残りの Azure RBAC ロールでは、特定の Azure リソースの管理が許可されます。 たとえば、仮想マシンの作成協力者ロールでは、仮想マシンの作成と管理は許可されますが、仮想マシンが接続する仮想ネットワークまたはサブネットの管理は許可されません。

## <a name="usage-data"></a>使用状況データ
Microsoft Azure Stack は、すべてのリソース プロバイダーの使用状況データを収集して集約し、Azure コマースによる処理のために Azure に送信します。 Azure Stack で収集された使用状況データは、REST API を使用して表示できます。 Azure と一貫性のある Tenant API だけでなく、Provider および Delegated Provider API を使用して、すべてのテナント サブスクリプション全体の使用状況データを取得できます。 このデータは、請求や配賦のために外部のツールやサービスと統合できます。 Azure コマースによって処理された使用状況は、Azure の課金ポータルに表示できます。

## <a name="next-steps"></a>次の手順
[管理の基本](azure-stack-manage-basics.md)

