---
title: 创建扩展
titleSuffix: Azure Data Studio
description: 了解如何创建和将扩展添加到 Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: craigg
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: d7d51459c49bd170b676a219474d35d8e50c1862
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105125"
---
# <a name="extend-the-functionality-by-creating-azure-data-studio-extensions"></a>通过创建 Azure Data Studio 扩展来扩展功能

[!INCLUDE[name-sos](../includes/name-sos-short.md)]擴充模組提供一個簡單的方式，可以新增更多功能至基礎 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 安裝。

扩展是团队提供的 Azure Data Studio (Microsoft) 以及第三方社区 （你 ！）。


## <a name="author-an-extension"></a>创作了一个扩展

如果有兴趣扩展 Azure Data Studio，可以创建自己的扩展，并将其发布到扩展库。

**编写扩展**

***先决条件***

若要开发扩展需要 Node.js 已安装并在你 $PATH 中可用。 Node.js 包含 npm，Node.js 包管理器，它将用于安装的扩展生成器。

若要启动新的扩展名，可以使用 Azure 数据 Studio 扩展生成器。 Yeoman[扩展生成器](https://www.npmjs.com/package/generator-azuredatastudio)可以非常轻松创建简单的扩展项目。 若要启动生成器，请在命令提示符下键入以下内容：

`npm install -g yo generator-azuredatastudio`

`yo azuredatastudio`


**扩展引用**

若要了解有关 Azure 数据 Studio 可扩展性，请参阅[扩展性概述](extensibility.md)。 您还可以查看有关如何使用现有 API 的示例[示例](https://github.com/Microsoft/azuredatastudio/tree/master/samples)。


## <a name="debug-an-extension"></a>调试扩展

您可以调试你使用 Visual Studio Code 扩展的新扩展[Azure 数据 Studio 调试](https://github.com/kevcunnane/sqlops-debug)。

步骤
- 打开你的扩展使用[Visual Studio Code](https://code.visualstudio.com/)
- 安装 Azure 数据 Studio 调试扩展
- 按**F5**或单击调试图标，然后单击**启动**。
- Azure Data Studio 的新实例启动 （扩展开发主机） 以特殊模式，此新实例现已了解你的扩展。


## <a name="create-an-extension-package"></a>创建扩展包

在编写您的扩展插件之后, 您需要创建 VSIX 包，以便能够将其安装在 Azure Data Studio。 可以使用[vsce](https://github.com/Microsoft/vscode-vsce)创建 VSIX 包。

`npm install -g vsce`

`vsce package`


## <a name="publish-an-extension"></a>发布扩展

若要发布到 Azure Data Studio 的新的扩展名：

1. 添加你的扩展 https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json
2. 我们目前没有支持添加到主机的第三方扩展，因此，Azure Data Studio 而不是下载的扩展，必须浏览到下载页的选项。 若要设置您的扩展插件的下载页，设置资产"Microsoft.AzureDataStudio.DownloadPage"的值。
3. 创建针对发布/扩展分支的拉取请求。
4. 向团队发送评审请求。

您的扩展插件将进行审查和添加到扩展库。

**发布扩展更新**发布更新的过程是类似于发布扩展。 请确保在 package.json 中更新版本
