---
title: 用户和工作区设置
titleSuffix: Azure Data Studio
description: 如何通过修改用户和工作区设置自定义 Azure Data Studio。
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: a874aaf9ec136ff9ea27cbeaa92011a07f3718c7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959274"
---
# <a name="modify-user-and-workspace-settings"></a>修改用户和工作区设置

很容易地配置[!INCLUDE[name-sos](../includes/name-sos-short.md)]根据需要通过设置。 几乎每个属于[!INCLUDE[name-sos](../includes/name-sos-short.md)]的编辑器、 用户界面和功能的行为有选项可以修改。

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 提供了两个不同的作用域的设置：

* **用户**这些设置全局应用到的任何实例[!INCLUDE[name-sos](../includes/name-sos-short.md)]打开。
* **工作区**工作区设置为特定于您的计算机上的文件夹的设置，在资源管理器侧栏中打开文件夹时才可用。 在此范围定义的设置重写用户范围。

## <a name="creating-user-and-workspace-settings"></a>创建用户和工作区设置

菜单命令**文件** > **首选项** > **设置**(**代码** >  **首选项** > **设置**Mac 上) 提供的入口点，若要配置用户和工作区设置。 提供的默认设置的列表。 将复制你想要将更改为适当的任何设置`settings.json`文件。 在右侧的选项卡，可以在用户和工作区设置文件之间快速切换。

您还可以打开中的用户和工作区设置**命令面板**(**Ctrl + Shift + P**) 与**首选项：打开用户设置**和**首选项：打开设置工作区**或使用键盘快捷方式 (**Ctrl +，** )。

以下示例禁用在编辑器中的行号，并配置的代码行来自动缩进。

![示例设置](media/settings/sample-settings.png)

对设置的更改会通过重新加载[!INCLUDE[name-sos](../includes/name-sos-short.md)]后已修改`settings.json`保存文件。

>**注意：** 工作区设置可用于跨团队共享特定于项目的设置。

## <a name="settings-file-locations"></a>设置文件位置

根据您的平台，用户设置文件的位置如下：

* **Windows** `%APPDATA%\azuredatastudio\User\settings.json`
* **Mac** `$HOME/Library/Application Support/azuredatastudio/User/settings.json`
* **Linux** `$HOME/.config/azuredatastudio/User/settings.json`

工作区设置文件位于`.[!INCLUDE[name-sos](../includes/name-sos-short.md)]`项目文件夹中的。

## <a name="hot-exit"></a>热退出

Azure Data Studio 会记住未保存的更改到文件时默认情况下退出。 这是与 Visual Studio Code 中的热退出功能相同。

默认情况下，热退出处于关闭状态。 通过编辑启用热退出`files.hotExit`设置。 有关详细信息，请参阅[（在 Visual Studio Code 文档中） 的热退出](https://code.visualstudio.com/docs/editor/codebasics#_hot-exit)。


## <a name="tab-color"></a>选项卡颜色

若要简化标识正在使用何种连接，在编辑器中打开的选项卡可以具有其颜色设置为匹配连接所属的服务器组的颜色。 默认情况下，选项卡颜色是默认情况下关闭。 通过编辑来启用选项卡颜色`sql.tabColorMode`设置。

## <a name="additional-resources"></a>其他资源

因为[!INCLUDE[name-sos](../includes/name-sos-short.md)]继承从 Visual Studio Code 中，设置的详细信息的功能都位于其用户和工作区设置[Visual Studio Code 设置](https://code.visualstudio.com/docs/getstarted/settings)一文。
