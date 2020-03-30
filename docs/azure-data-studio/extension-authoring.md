---
title: 创建扩展
titleSuffix: Azure Data Studio
description: 了解如何创建扩展并将其添加到 Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: d0c43df8b24a33f3763dc5ff3a80e989b9b85038
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "67959606"
---
# <a name="extend-the-functionality-by-creating-azure-data-studio-extensions"></a>通过创建 Azure Data Studio 扩展来扩展功能

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 中的扩展提供向基本 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 安装添加更多功能的简便方法。

扩展由 Azure Data Studio 团队 (Microsoft) 以及第三方社区（你）提供。


## <a name="author-an-extension"></a>编写扩展

如果你对扩展 Azure Data Studio 感兴趣，则可创建自己的扩展并将其发布到扩展库。

**编写扩展**

***先决条件***

若要开发扩展，你需要在 $PATH 中安装并提供 Node.js。 Node.js 包含 npm（即 Node.js 包管理器），它将用于安装扩展生成器。

若要启动新的扩展，可使用 Azure Data Studio 扩展生成器。 借助 Yeoman [扩展生成器](https://www.npmjs.com/package/generator-azuredatastudio)，可非常轻松地创建简单的扩展项目。 若要启动生成器，请在命令提示符中键入以下内容：

`npm install -g yo generator-azuredatastudio`

`yo azuredatastudio`


**扩展性参考**

若要了解 Azure Data Studio 扩展性，请参阅[扩展性概述](extensibility.md)。 还可在现有[示例](https://github.com/Microsoft/azuredatastudio/tree/master/samples)中查看如何使用 API 的示例。


## <a name="debug-an-extension"></a>调试扩展

可使用 Visual Studio Code 扩展 [Azure Data Studio 调试](https://github.com/kevcunnane/sqlops-debug)来调试新扩展。

步骤
- 使用 [Visual Studio Code](https://code.visualstudio.com/) 打开扩展
- 安装 Azure Data Studio 调试扩展
- 按“F5”或单击“调试”图标，然后单击“启动”   。
- Azure Data Studio 的新实例在特殊模式（扩展开发主机）下启动，此新实例现在可以识别你的扩展。


## <a name="create-an-extension-package"></a>创建扩展包

编写扩展后，需要创建 VSIX 包，以便能够在 Azure Data Studio 中安装它。 可使用 [vsce](https://github.com/Microsoft/vscode-vsce) 来创建 VSIX 包。

`npm install -g vsce`

`vsce package`


## <a name="publish-an-extension"></a>发布扩展

若要将新扩展发布到 Azure Data Studio，请执行以下操作：

1. 将扩展添加到 https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json
2. 我们目前不支持托管第三方扩展，因此，Azure Data Studio 提供浏览到下载页的选项，而不会下载扩展。 若要为扩展设置下载页，请设置资产“Microsoft.AzureDataStudio.DownloadPage”的值。
3. 针对发布/扩展分支创建 PR。
4. 向团队发送评审请求。

你的扩展将接受评审并添加到扩展库中。

**发布扩展更新** 发布更新的过程与发布扩展的过程类似。 请确保在 package.json 中更新版本
