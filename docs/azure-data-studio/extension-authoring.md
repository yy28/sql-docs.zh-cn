---
title: 创建扩展
description: 了解创建扩展并将其发布到 Azure Data Studio
ms.prod: azure-data-studio
ms.technology: ''
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 63a4c95f12aefafec97a58a186d33a5095b90dc2
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/20/2020
ms.locfileid: "86483841"
---
# <a name="extend-the-functionality-by-creating-azure-data-studio-extensions"></a>通过创建 Azure Data Studio 扩展来扩展功能

借助 Azure Data Studio 中的扩展，可轻松地向基本 Azure Data Studio 安装添加更多功能。

扩展由 Azure Data Studio 团队 (Microsoft) 以及第三方社区（你）提供。


## <a name="author-an-extension"></a>编写扩展

如果你对扩展 Azure Data Studio 感兴趣，则可创建自己的扩展并将其发布到扩展库。

**编写扩展**

***先决条件***

若要开发扩展，你需要在 `$PATH` 中安装并提供 [Node.js](https://nodejs.org/)。 Node.js 包含 npm（即 Node.js 包管理器），它将用于安装扩展生成器。

若要创建新的扩展，可使用 Azure Data Studio 扩展生成器。 Yeoman [扩展生成器](https://www.npmjs.com/package/generator-azuredatastudio)是扩展项目的一个有用起点。 若要启动生成器，请在命令提示符中键入以下内容：

```
npm install -g yo generator-azuredatastudio # Install the generator
yo azuredatastudio
```

有关如何开始使用扩展模板的深入指南，请参阅[创建扩展](https://docs.microsoft.com/sql/azure-data-studio/tutorial-create-extension?view=sql-server-ver15)，这将指导你完成创建键映射扩展。

**扩展性参考**

若要了解 Azure Data Studio 扩展性，请参阅[扩展性概述](extensibility.md)。 还可在现有[示例](https://github.com/Microsoft/azuredatastudio/tree/main/samples)中查看如何使用 API 的示例。


## <a name="debug-an-extension"></a>调试扩展

可使用 Visual Studio Code 扩展 [Azure Data Studio 调试](https://github.com/kevcunnane/sqlops-debug)来调试新扩展。

步骤
1. 使用 [Visual Studio Code](https://code.visualstudio.com/) 打开扩展。
1. 安装 Azure Data Studio 调试扩展。
1. 按“F5”或单击“调试”图标，然后单击“启动” 。
1. Azure Data Studio 的新实例在特殊模式（扩展开发主机）下启动，此新实例现在可以识别你的扩展。


## <a name="create-an-extension-package"></a>创建扩展包

编写扩展后，需要创建 VSIX 包，以便能够在 Azure Data Studio 中安装它。 可以使用 [vsce](https://github.com/Microsoft/vscode-vsce)（Visual Studio Code 扩展）创建 VSIX 包。 

```
npm install -g vsce
cd myExtensionName
vsce package
# The myExtensionName.vsix file has now been generated
```

借助 VSIX 包，可以通过共享 `.vsix` 文件并使用“命令面板”中的命令“扩展：从 VSIX 文件安装”将扩展安装到 Azure Data Studio 中，从而以本地和非公开形式共享扩展。


## <a name="publish-an-extension"></a>发布扩展

若要将新扩展发布到 Azure Data Studio，请执行以下操作：

1. 将扩展添加到 https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json
2. 我们目前不支持托管第三方扩展，因此，Azure Data Studio 提供浏览到下载页的选项，而不会下载扩展。 若要为扩展设置下载页，请设置资产“Microsoft.AzureDataStudio.DownloadPage”的值。
3. 针对发布/扩展分支创建 PR。
4. 向团队发送评审请求。

你的扩展将接受评审并添加到扩展库中。

**发布扩展更新**

发布更新的过程与发布扩展的过程类似。 请确保在 package.json 中更新版本。
