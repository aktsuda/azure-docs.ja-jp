---
title: Azure IoT Hub Toolkit for VS Code を使用した Azure IoT ハブの作成 | Microsoft Docs
description: Azure IoT Hub Toolkit for VS Code を使用して IoT ハブを作成する方法。
author: formulahendry
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 07/30/2018
ms.author: junhan
ms.openlocfilehash: cee71ddfbf1a20cc7417976d60b04bff6f0deac8
ms.sourcegitcommit: edacc2024b78d9c7450aaf7c50095807acf25fb6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/13/2018
ms.locfileid: "53339027"
---
# <a name="create-an-iot-hub-using-the-azure-iot-hub-toolkit-for-visual-studio-code"></a>Azure IoT Hub Toolkit for Visual Studio Code を使用した IoT ハブの作成

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

この記事では、[Azure IoT Hub Toolkit for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit) (旧称 Azure IoT Toolkit) を使用して Azure IoT ハブを作成する方法について説明します。 

この記事を完了するには、以下が必要です。

- Azure サブスクリプション。 Azure サブスクリプションをお持ちでない場合は、開始する前に [無料アカウント](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) を作成してください。

- [Visual Studio Code](https://code.visualstudio.com/)

- [Azure IoT Hub Toolkit](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit)

## <a name="create-an-iot-hub"></a>IoT Hub の作成

1. Visual Studio Code で**エクスプローラー** ビューを開きます。

2. エクスプローラーの下部で、**[Azure IoT Hub Devices]\(Azure IoT Hub デバイス\)** セクションを展開します。 

   ![Azure IoT Hub デバイスを展開する](./media/iot-hub-create-use-iot-toolkit/azure-iot-hub-devices.png)

3. **[Azure IoT Hub Devices]\(Azure IoT Hub デバイス\)** セクション ヘッダーで **[...]** をクリックします。 省略記号が表示されない場合は、ヘッダーをポイントします。 

4. **[Create IoT Hub]\(IoT ハブを作成する\)** を選択します。

5. 右下隅にポップアップが表示され、Azure への初めてのサインインを行うことができます。

6. Azure サブスクリプションを選択します。 

7. リソース グループを選択します。

8. 場所を選択します。

9. 価格レベルを選択します。

10. IoT ハブのグローバルに一意の名前を入力します。

11. IoT ハブが作成されるまで数分待ちます。

## <a name="next-steps"></a>次の手順

ここでは、Azure IoT Hub Toolkit for Visual Studio Code を使用して IoT ハブをデプロイしました。 次の記事に進んでください。

* [Visual Studio Code 用 Azure IoT Hub Toolkit 拡張機能を使用してデバイスと IoT Hub の間のメッセージを送受信する](iot-hub-vscode-iot-toolkit-cloud-device-messaging.md)。

* [Azure IoT Hub デバイスの管理に Visual Studio Code 用 Azure IoT Hub Toolkit 拡張機能を使用する](iot-hub-device-management-iot-toolkit.md)

* [Azure IoT Hub Toolkit の Wiki ページを参照する](https://github.com/microsoft/vscode-azure-iot-toolkit/wiki)。
