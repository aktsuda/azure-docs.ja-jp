---
title: インクルード ファイル
description: インクルード ファイル
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mtillman
editor: ''
ms.service: active-directory
ms.devlang: na
ms.topic: include
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/19/2018
ms.author: andret
ms.custom: include file
ms.openlocfilehash: bc439cbe5e690077213b5d7953a4e74488988c3b
ms.sourcegitcommit: c2c279cb2cbc0bc268b38fbd900f1bac2fd0e88f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2018
ms.locfileid: "49988550"
---
# <a name="add-sign-in-with-microsoft-to-an-aspnet-web-app"></a>ASP.NET Web アプリへの "Microsoft でサインイン" の追加

このガイドでは、OpenID Connect を使用する従来の Web ブラウザー ベースのアプリケーションで、ASP.NET MVC ソリューションを使用して "Microsoft でサインイン" を実装する方法を示します。

このガイドの最後では、アプリケーションは、個人アカウント (outlook.com、live.com などを含む) だけでなく、Azure Active Directory と統合されたすべての会社や組織の職場/学校アカウントのサインインを受け入れられるようになります。

> このガイドでは、Visual Studio 2015 Update 3 または Visual Studio 2017 が必要です。  お持ちでない場合は、  [Visual Studio 2017 を無料でダウンロードできます。](https://www.visualstudio.com/downloads/)

## <a name="how-the-sample-app-generated-by-this-guide-works"></a>このガイドで生成されたサンプル アプリの動作

![このガイドの利用法](media/active-directory-develop-guidedsetup-aspnetwebapp-intro/aspnetbrowsergeneral.png)

このガイドによって作成されるサンプル アプリケーションは、ユーザーがブラウザーを使用して、[サインイン] ボタンを介した認証をユーザーに要求する ASP.NET Web サイトにアクセスするシナリオに基づいています。 このシナリオでは、Web ページを表示する処理の大半がサーバー側で発生します。

## <a name="libraries"></a>ライブラリ

このガイドでは、次のライブラリを使用します。

|ライブラリ|説明|
|---|---|
|[Microsoft.Owin.Security.OpenIdConnect](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|アプリケーションで認証に OpenIDConnect を使用できるようにするためのミドルウェア|
|[Microsoft.Owin.Security.Cookies](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|アプリケーションで Cookie を使用してユーザー セッションを維持できるようにするためのミドルウェア|
|[Microsoft.Owin.Host.SystemWeb](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|ASP.NET 要求パイプラインを使用した、IIS 上での OWIN ベース アプリケーションの実行が可能|
