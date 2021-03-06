---
title: 'チュートリアル: Azure Active Directory と MyWorkDrive の統合 | Microsoft Docs'
description: Azure Active Directory と MyWorkDrive の間でシングル サインオンを構成する方法について説明します。
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4d049778-3c7b-46c0-92a4-f2633a32334b
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/13/2018
ms.author: jeedes
ms.openlocfilehash: 7644a8517840b4fdffe0bc47c5a9bb97d48f6322
ms.sourcegitcommit: db2cb1c4add355074c384f403c8d9fcd03d12b0c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/15/2018
ms.locfileid: "51686798"
---
# <a name="tutorial-azure-active-directory-integration-with-myworkdrive"></a>チュートリアル: Azure Active Directory と MyWorkDrive の統合

このチュートリアルでは、MyWorkDrive と Azure Active Directory (Azure AD) を統合する方法について説明します。

MyWorkDrive と Azure AD の統合には、次の利点があります。

- MyWorkDrive にアクセスする Azure AD ユーザーを制御できます。
- ユーザーが自分の Azure AD アカウントで自動的に MyWorkDrive にサインオン (シングル サインオン) できるようにします。
- 1 つの中央サイト (Azure Portal) でアカウントを管理できます。

SaaS アプリと Azure AD の統合の詳細については、「[Azure Active Directory のアプリケーション アクセスとシングル サインオンとは](../manage-apps/what-is-single-sign-on.md)」をご覧ください。

## <a name="prerequisites"></a>前提条件

MyWorkDrive と Azure AD の統合を構成するには、次のものが必要です。

- Azure AD サブスクリプション
- MyWorkDrive でのシングル サインオンが有効なサブスクリプション

> [!NOTE]
> このチュートリアルの手順をテストする場合、運用環境を使用しないことをお勧めします。

このチュートリアルの手順をテストするには、次の推奨事項に従ってください。

- 必要な場合を除き、運用環境は使用しないでください。
- Azure AD の評価環境がない場合は、[1 か月の評価版を入手できます](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>シナリオの説明

このチュートリアルでは、テスト環境で Azure AD のシングル サインオンをテストします。 このチュートリアルで説明するシナリオは、主に次の 2 つの要素で構成されています。

1. ギャラリーからの MyWorkDrive の追加
2. Azure AD シングル サインオンの構成とテスト

## <a name="adding-myworkdrive-from-the-gallery"></a>ギャラリーからの MyWorkDrive の追加

Azure AD への MyWorkDrive の統合を構成するには、ギャラリーから管理対象 SaaS アプリの一覧に MyWorkDrive を追加する必要があります。

**ギャラリーから MyWorkDrive を追加するには、次の手順に従います。**

1. **[Azure Portal](https://portal.azure.com)** の左側のナビゲーション ウィンドウで、**[Azure Active Directory]** アイコンをクリックします。 

    ![Azure Active Directory のボタン][1]

2. **[エンタープライズ アプリケーション]** に移動します。 次に、**[すべてのアプリケーション]** に移動します。

    ![[エンタープライズ アプリケーション] ブレード][2]

3. 新しいアプリケーションを追加するには、ダイアログの上部にある **[新しいアプリケーション]** をクリックします。

    ![[新しいアプリケーション] ボタン][3]

4. 検索ボックスに「**MyWorkDrive**」と入力し、結果パネルで **MyWorkDrive** を選び、**[追加]** をクリックして、アプリケーションを追加します。

    ![結果リストの MyWorkDrive](./media/myworkdrive-tutorial/tutorial_myworkdrive_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD シングル サインオンの構成とテスト

このセクションでは、"Britta Simon" というテスト ユーザーに基づいて、MyWorkDrive で Azure AD のシングル サインオンを構成し、テストします。

シングル サインオンを機能させるには、Azure AD ユーザーに対応する MyWorkDrive ユーザーが Azure AD で認識されている必要があります。 言い換えると、Azure AD ユーザーと MyWorkDrive の関連ユーザーの間で、リンク関係が確立されている必要があります。

MyWorkDrive で Azure AD のシングル サインオンを構成してテストするには、次の構成要素を完了する必要があります。

1. **[Azure AD シングル サインオンの構成](#configuring-azure-ad-single-sign-on)** - ユーザーがこの機能を使用できるようにします。
2. **[Azure AD のテスト ユーザーの作成](#creating-an-azure-ad-test-user)** - Britta Simon で Azure AD のシングル サインオンをテストします。
3. **[MyWorkDrive テスト ユーザーの作成](#creating-a-myworkdrive-test-user)** - MyWorkDrive 内で Britta Simon に対応するユーザーを作成し、Azure AD 内の Britta Simon にリンクさせます。
4. **[Azure AD テスト ユーザーの割り当て](#assigning-the-azure-ad-test-user)** - Britta Simon が Azure AD のシングル サインオンを使用できるようにします。
5. **[シングル サインオンのテスト](#testing-single-sign-on)** - 構成が機能するかどうかを確認します。

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD シングル サインオンの構成

このセクションでは、Azure portal で Azure AD のシングル サインオンを有効にして、MyWorkDrive アプリケーションでシングル サインオンを構成します。

**MyWorkDrive で Azure AD シングル サインオンを構成するには、次の手順に従います。**

1. Azure portal の **MyWorkDrive** アプリケーション統合ページで、**[シングル サインオン]** をクリックします。

    ![シングル サインオン構成のリンク][4]

2. **[シングル サインオン方式の選択]** ダイアログで、**[SAML]** モードの **[選択]** をクリックして、シングル サインオンを有効にします。

    ![Configure single sign-on](common/tutorial_general_301.png)

3. **[SAML でシングル サインオンをセットアップします]** ページで、**[編集]** アイコンをクリックして **[基本的な SAML 構成]** ダイアログを開きます。

    ![Configure single sign-on](common/editconfigure.png)

4. **[基本的な SAML 構成]** セクションで、**IDP** 開始モードでアプリケーションを構成する場合は、次の手順を実行します。

    ![[MyWorkDrive Domain and URLs] (MyWorkDrive のドメインと URL) のシングル サインオン情報](./media/myworkdrive-tutorial/tutorial_myworkdrive_url.png)

    **[応答 URL]** ボックスに、`https://<SERVER.DOMAIN.COM>/SAML/AssertionConsumerService.aspx` のパターンを使用して URL を入力します。

5. アプリケーションを **SP** 開始モードで構成する場合は、**[追加の URL を設定します]** をクリックして次の手順を実行します。

    ![[MyWorkDrive Domain and URLs] (MyWorkDrive のドメインと URL) のシングル サインオン情報](./media/myworkdrive-tutorial/tutorial_myworkdrive_url1.png)

     **[サインオン URL]** ボックスに、`https://<SERVER.DOMAIN.COM>/Account/Login-saml` のパターンを使用して URL を入力します。 

    > [!NOTE]
    > これらは実際の値ではありません。 実際の応答 URL とサインオン URL でこれらの値を更新します。  自社の MyWorkDrive サーバーのホスト名を入力します。たとえば、次のようになります。
    > 
    > 応答 URL: `https://yourserver.yourdomain.com/SAML/AssertionConsumerService.aspx`
    > 
    > サインオン URL: `https://yourserver.yourdomain.com/Account/Login-saml`
    > 
    > これらの値に対して独自のホスト名と SSL 証明書を設定する方法がわからない場合は、MyWorkDrive Client サポート チームにお問い合わせください。

6. **[SAML 署名証明書]** ページの **[SAML 署名証明書]** セクションで、コピー **アイコン**をクリックして **[アプリのフェデレーション メタデータ URL]** をコピーし、コンピューターに保存します。

    ![証明書のダウンロードのリンク](./media/myworkdrive-tutorial/tutorial_myworkdrive_certificate.png)

7. 別の Web ブラウザー ウィンドウで、セキュリティ管理者として MyWorkDrive にログインします。

8. MyWorkDrive サーバー上の管理パネルで、**[ENTERPRISE]\(エンタープライズ\)** をクリックし、次の手順を実行します。

    ![管理](./media/myworkdrive-tutorial/tutorial_myworkdrive_admin.png)

    a. **[SAML/ADFS SSO]\(SAML/ADFS SSO\)** を有効にします。

    b. **[SAML - Azure AD]\(SAML - Azure AD\)** を選択します

    c. **[Azure App Federation Metadata Url]\(Azure アプリのフェデレーション メタデータ URL\)** テキスト ボックスに、Azure portal からコピーした **[アプリのフェデレーション メタデータ URL]** の値を貼り付けます。

    d. **[保存]**

    >[!NOTE]
    >追加情報については、[MyWorkDrive の Azure AD サポートに関する記事](https://www.myworkdrive.com/support/saml-single-sign-on-azure-ad/)をご覧ください。

### <a name="creating-an-azure-ad-test-user"></a>Azure AD のテスト ユーザーの作成

このセクションの目的は、Azure Portal で Britta Simon というテスト ユーザーを作成することです。

1. Azure portal の左側のウィンドウで、**[Azure Active Directory]**、**[ユーザー]**、**[すべてのユーザー]** の順に選択します。

    ![Azure AD ユーザーの作成][100]

2. 画面の上部にある **[新しいユーザー]** を選択します。

    ![Azure AD のテスト ユーザーの作成](common/create_aaduser_01.png) 

3. [ユーザーのプロパティ] で、次の手順を実行します。

    ![Azure AD のテスト ユーザーの作成](common/create_aaduser_02.png)

    a. **[名前]** フィールドに「**BrittaSimon**」と入力します。
  
    b. **[ユーザー名]** フィールドに「**brittasimon@yourcompanydomain.extension**」と入力します  
    たとえば、BrittaSimon@contoso.com のように指定します。

    c. **[プロパティ]** を選択し、**[パスワードを表示]** チェック ボックスをオンにして、[パスワード] ボックスに表示された値を書き留めます。

    d. **作成**を選択します。

### <a name="creating-a-myworkdrive-test-user"></a>MyWorkDrive テスト ユーザーの作成

このセクションでは、MyWorkDrive で Britta Simon というユーザーを作成します。  [MyWorkDrive サポート チーム](mailto:support@myworkdrive.com)と連携して、MyWorkDrive プラットフォームにユーザーを追加します。 シングル サインオンを使用する前に、ユーザーを作成し、有効化する必要があります。

### <a name="assigning-the-azure-ad-test-user"></a>Azure AD テスト ユーザーの割り当て

このセクションでは、Britta Simon に MyWorkDrive へのアクセスを許可することで、このユーザーが Azure シングル サインオンを使用できるようにします。

1. Azure portal で **[エンタープライズ アプリケーション]** を選択し、**[すべてのアプリケーション]** を選択します。

    ![ユーザーの割り当て][201]

2. アプリケーションの一覧で **[MyWorkDrive]** を選択します。

    ![Configure single sign-on](./media/myworkdrive-tutorial/tutorial_myworkdrive_app.png) 

3. 左側のメニューで **[ユーザーとグループ]** をクリックします。

    ![ユーザーの割り当て][202]

4. **[追加]** ボタンをクリックします。 次に、**[割り当ての追加]** ダイアログで **[ユーザーとグループ]** を選択します。

    ![ユーザーの割り当て][203]

5. **[ユーザーとグループ]** ダイアログの [ユーザー] の一覧で **[Britta Simon]** を選択し、画面の下部にある **[選択]** ボタンをクリックします。

6. **[割り当ての追加]** ダイアログで、**[割り当て]** ボタンを選択します。

### <a name="testing-single-sign-on"></a>シングル サインオンのテスト

このセクションでは、アクセス パネルを使用して Azure AD のシングル サインオン構成をテストします。

アクセス パネルで [MyWorkDrive] タイルをクリックすると、自動的に MyWorkDrive アプリケーションにサインオンします。
アクセス パネルの詳細については、[アクセス パネルの概要](../user-help/active-directory-saas-access-panel-introduction.md)に関するページを参照してください。

## <a name="additional-resources"></a>その他のリソース

* [SaaS アプリと Azure Active Directory を統合する方法に関するチュートリアルの一覧](tutorial-list.md)
* [Azure Active Directory のアプリケーション アクセスとシングル サインオンとは](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: common/tutorial_general_01.png
[2]: common/tutorial_general_02.png
[3]: common/tutorial_general_03.png
[4]: common/tutorial_general_04.png

[100]: common/tutorial_general_100.png

[201]: common/tutorial_general_201.png
[202]: common/tutorial_general_202.png
[203]: common/tutorial_general_203.png
