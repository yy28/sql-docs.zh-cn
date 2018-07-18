---
title: SQL 操作 Studio （预览版） 用户和工作区设置 |Microsoft 文档
description: 如何修改 SQL 操作 Studio （预览版） 用户和工作区设置。
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 67f60d30693eeb60030f3a977ec1bcf5a1f98be1
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2018
ms.locfileid: "34235134"
---
# <a name="user-and-workspace-settings"></a>用户和工作区设置

很容易地配置[!INCLUDE[name-sos](../includes/name-sos-short.md)]根据通过设置自己的喜好。 几乎每个属于[!INCLUDE[name-sos](../includes/name-sos-short.md)]的编辑器、 用户界面和功能的行为具有选项可以修改。

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 提供两个不同的作用域的设置：

* **用户**这些设置应用到的任何实例的全局[!INCLUDE[name-sos](../includes/name-sos-short.md)]打开。
* **工作区**工作区设置是特定于你计算机上的文件夹的设置，在资源管理器侧栏中打开文件夹时才可用。 在此作用域上定义的设置会覆盖用户作用域。

## <a name="creating-user-and-workspace-settings"></a>创建用户和工作区设置

菜单命令**文件** > **首选项** > **设置**(**代码** >  **首选项** > **设置**Mac 上) 提供入口点，以配置用户和工作区设置。 提供的默认设置的列表。 将复制任何你想要将更改为适当的设置`settings.json`文件。 在右侧的选项卡，可以在用户和工作区设置文件之间快速切换。

你也可以打开中的用户和工作区设置**命令控制板**(**Ctrl + Shift + P**) 与**首选项： 打开用户设置**和**首选项： 打开工作区设置**或使用键盘快捷方式 (**Ctrl +**)。

下面的示例禁用在编辑器中的行号，并配置代码行以自动缩进。

![设置示例](media/settings/sample-settings.png)

对设置的更改在重新加载由[!INCLUDE[name-sos](../includes/name-sos-short.md)]后已修改`settings.json`保存文件。

>**注意：** 工作区设置可用于在团队之间共享特定于项目的设置。

## <a name="settings-file-locations"></a>设置文件的位置

根据您的平台，用户设置文件的位置如下：

* **Windows** `%APPDATA%\sqlops\User\settings.json`
* **Mac** `$HOME/Library/Application Support/sqlops/User/settings.json`
* **Linux** `$HOME/.config/sqlops/User/settings.json`

工作区设置文件位于`.[!INCLUDE[name-sos](../includes/name-sos-short.md)]`项目文件夹中的。

## <a name="hot-exit"></a>热退出

当你退出默认情况下 SQL 操作 Studio 将记住文件未保存的更改。 这是与 Visual Studio 代码中的热退出功能相同。

默认情况下，热退出处于关闭状态。 启用作用通过编辑退出`files.hotExit`设置。 有关详细信息，请参阅[（在 Visual Studio Code 文档中） 的热退出](https://code.visualstudio.com/docs/editor/codebasics#_hot-exit)。


## <a name="tab-color"></a>选项卡颜色

若要简化标识你正在使用哪些连接，在编辑器中打开的选项卡可以具有它们的设置相匹配的连接所属的服务器组的颜色的颜色。 默认情况下，选项卡颜色默认为关闭的。 启用通过编辑选项卡颜色`sql.tabColorMode`设置。

## <a name="additional-resources"></a>其他资源

因为[!INCLUDE[name-sos](../includes/name-sos-short.md)]继承从 Visual Studio 代码中，设置有关的详细信息的功能都位于其用户和工作区设置[设置 Visual Studio Code](https://code.visualstudio.com/docs/getstarted/settings)文章。
