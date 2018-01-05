---
title: "SQL 操作 Studio （预览版） 用户和工作区设置 |Microsoft 文档"
description: "如何修改 SQL 操作 Studio （预览版） 用户和工作区设置。"
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: article
author: yualan
ms.author: alayu
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2edea069c05e7ac0316042250f336f1a8c455af0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="user-and-workspace-settings"></a>用户和工作区设置

很容易地配置[!INCLUDE[name-sos](../includes/name-sos-short.md)]根据通过设置自己的喜好。 几乎每个属于[!INCLUDE[name-sos](../includes/name-sos-short.md)]的编辑器、 用户界面和功能的行为具有选项可以修改。

[!INCLUDE[name-sos](../includes/name-sos-short.md)]提供两个不同的作用域的设置：

* **用户**这些设置应用到的任何实例的全局[!INCLUDE[name-sos](../includes/name-sos-short.md)]打开。
* **工作区**工作区设置是特定于你计算机上的文件夹的设置，在资源管理器侧栏中打开文件夹时才可用。 在此作用域上定义的设置会覆盖用户作用域。

## <a name="creating-user-and-workspace-settings"></a>创建用户和工作区设置

菜单命令**文件** > **首选项** > **设置**(**代码** >  **首选项** > **设置**Mac 上) 提供入口点，以配置用户和工作区设置。 提供的默认设置的列表。 将复制任何你想要将更改为适当的设置`settings.json`文件。 在右侧的选项卡，可以在用户和工作区设置文件之间快速切换。

你也可以打开中的用户和工作区设置**命令控制板**(**Ctrl + Shift + P**) 与**首选项： 打开用户设置**和**首选项： 打开工作区设置**或使用键盘快捷方式 (**Ctrl +**)。

下面的示例禁用在编辑器中的行号，并配置的文本编辑器的大小环绕自动基于行。

![设置示例](media/settings/sample-settings.png)

对设置的更改在重新加载由[!INCLUDE[name-sos](../includes/name-sos-short.md)]后已修改`settings.json`保存文件。

>**注意：**工作区设置可用于在团队之间共享特定于项目的设置。

## <a name="settings-file-locations"></a>设置文件的位置

根据您的平台，用户设置文件的位置如下：

* **Windows**`%APPDATA%\sqlops\User\settings.json`
* **Mac**`$HOME/Library/Application Support/sqlops/User/settings.json`
* **Linux**`$HOME/.config/sqlops/User/settings.json`

工作区设置文件位于`.[!INCLUDE[name-sos](../includes/name-sos-short.md)]`项目文件夹中的。


## <a name="additional-resources"></a>其他资源

因为[!INCLUDE[name-sos](../includes/name-sos-short.md)]继承从 Visual Studio 代码中，设置有关的详细信息的功能都位于其用户和工作区设置[设置 Visual Studio Code](https://code.visualstudio.com/docs/getstarted/settings)文章。