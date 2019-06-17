---
title: 教程：创建一个扩展
titleSuffix: Azure Data Studio
description: 本教程演示如何创建要将自定义功能添加到 Azure Data Studio 的扩展。
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: tutorial
author: kevcunnane
ms.author: kcunnane
manager: jroth
ms.openlocfilehash: 2f031ec68cc6ae342b8bac51c450ee40a9df0555
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66797954"
---
# <a name="tutorial-create-an-azure-data-studio-extension"></a>教程：创建 Azure Data Studio 扩展

本教程演示如何创建一个新的 Azure Data Studio 扩展。 该扩展会在 Azure Data Studio 熟悉 SSMS 的键绑定。

本教程期间，你学习如何：
> [!div class="checklist"]
> * 创建一个扩展项目
> * 安装扩展生成器
> * 创建您的扩展插件
> * 测试您的扩展
> * 打包你的扩展
> * 将你的扩展发布到 marketplace

## <a name="prerequisites"></a>先决条件

Azure Data Studio 基于相同的框架作为 Visual Studio Code 中，因此使用 Visual Studio Code 构建 Azure Data Studio 的扩展。 若要开始，需要以下组件：

- [Node.js](https://nodejs.org)已安装，不可用于你`$PATH`。 Node.js 包含[npm](https://www.npmjs.com/)，Node.js 程序包管理器，用于安装的扩展生成器。
- [Visual Studio Code](https://code.visualstudio.com)调试扩展。
- Azure Data Studio[调试扩展](https://marketplace.visualstudio.com/items?itemName=ms-mssql.sqlops-debug)（可选）。 这使您无需打包并将其安装到 Azure Data Studio 测试您的扩展插件。
- 确保`azuredatastudio`是在你的路径。 对于 Windows，请确保你选择`Add to Path`setup.exe 中的选项。 适用于 Mac 或 Linux，运行*安装路径中的 azuredatastudio 命令*选项。


## <a name="install-the-extension-generator"></a>安装扩展生成器

若要简化创建扩展的过程，我们已构建[扩展生成器](https://code.visualstudio.com/docs/extensions/yocode)使用 Yeoman。 若要安装它，请从命令提示符处运行以下：

`npm install -g yo generator-azuredatastudio`

## <a name="create-your-extension"></a>创建您的扩展插件

若要创建扩展：

1. 启动扩展生成器使用以下命令：

   `yo azuredatastudio`

2. 选择**新键映射**从扩展插件类型的列表：

   ![扩展生成器](./media/tutorial-create-extension/extension-generator.png)

3. 按相关步骤来填写扩展名称 (对于本教程中，使用**ssmskeymap2**)，并且添加说明。

完成前面的步骤创建一个新文件夹。 打开 Visual Studio Code 和您的文件夹中已准备好创建自己的键绑定扩展 ！


### <a name="add-a-keyboard-shortcut"></a>添加键盘快捷方式

**步骤 1：找到要替换的快捷方式**

现在，我们已准备就绪我们扩展，添加一些 SSMS 键盘快捷方式 （或键绑定） 到 Azure Data Studio。 我使用了[Andy Mallon 备忘单](https://am2.co/2018/02/updated-cheat-sheet/)和灵感 RedGate 的键盘快捷方式列表。

我看到缺少顶级工作项是：

- 与已启用的实际执行计划中运行查询。 这是**Ctrl + M**在 SSMS 中和不具有 Azure Data Studio 中的绑定。
- 无**CTRL + SHIFT + E**作为运行查询的第二种方法。 用户反馈表明，这是缺失。
- 无**ALT + F1**运行`sp_help`。 我们在 Azure Data Studio 中添加这但因为该绑定已使用，我们将映射到**ALT + F2**相反。
- 切换全屏显示 (**SHIFT + ALT + ENTER**)。
- **F8**以显示**对象资源管理器** / **服务器视图**。

很容易地查找和替换这些键绑定。 运行*打开键盘快捷方式*以显示**键盘快捷方式**选项卡中 Azure Data Studio，搜索*查询*，然后选择**更改密钥绑定**. 完成后更改键绑定，可以看到 keybindings.json 文件中已更新的映射 (运行*打开键盘快捷方式*以查看它)。

![键盘快捷键](./media/tutorial-create-extension/keyboard-shortcuts.png)

![keybindings.json 扩展](./media/tutorial-create-extension/keybindings-json.png)


**步骤 2：将快捷方式添加到扩展**

若要将快捷方式添加到扩展中，打开*package.json*文件 （扩展名），并替换`contributes`节替换为以下：

```json
"contributes": {
  "keybindings": [
    {
      "key": "shift+cmd+e",
      "command": "runQueryKeyboardAction"
    },
    {
      "key": "ctrl+cmd+e",
      "command": "workbench.view.explorer"
    },
    {
      "key": "alt+f1",
      "command": "workbench.action.query.shortcut1"
    },
    {
      "key": "shift+alt+enter",
      "command": "workbench.action.toggleFullScreen"
    },
    {
      "key": "f8",
      "command": "workbench.view.connections"
    },
    {
      "key": "ctrl+m",
      "command": "runCurrentQueryWithActualPlanKeyboardAction"
    }
  ]
}
```

## <a name="test-your-extension"></a>测试您的扩展

确保`azuredatastudio`通过在 Azure Data Studio 中的路径命令运行安装 azuredatastudio 命令是在你的路径。

请确保在 Visual Studio Code 中安装了 Azure 数据 Studio 进行调试的扩展。

选择**F5** Azure Data Studio 在调试模式下启动与运行的扩展：

![安装扩展](./media/tutorial-create-extension/install-extension.png)

![测试扩展](./media/tutorial-create-extension/test-extension.png)

键映射是一种最快的扩展，若要创建，因此，新的扩展名现在应成功地工作并准备好共享。

## <a name="package-your-extension"></a>打包你的扩展

若要与他人共享需要扩展打包到单个文件。 这可以是发布到 Azure Data Studio 扩展应用商店，或在你的团队或社区间共享。 若要执行此操作，需要从命令行安装另一个 npm 包：

`npm install -g vsce`

导航到该扩展的基目录并运行`vsce package`。 我需要添加几个额外的行，以停止*vsce*从抱怨的工具：

```json
"repository": {
    "type": "git",
    "url": "https://github.com/kevcunnane/ssmskeymap.git"
},
"bugs": {
    "url": "https://github.com/kevcunnane/ssmskeymap/issues"
},
```

一旦执行此操作，我 ssmskeymap 0.1.0.vsix 文件已创建并可供安装并与世界共享 ！

![安装扩展](./media/tutorial-create-extension/extensions.png)


## <a name="publish-your-extension-to-the-marketplace"></a>将你的扩展发布到 marketplace

Azure Data Studio 扩展应用商店未完全实现，但当前进程是托管扩展 VSIX 某个位置 （例如，GitHub 发布页） 然后提交拉取请求更新[此 JSON 文件](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json)与你扩展信息。


## <a name="next-steps"></a>后续步骤

在本教程中，你将了解：
> [!div class="checklist"]
> * 创建一个扩展项目
> * 安装扩展生成器
> * 创建您的扩展插件
> * 测试您的扩展
> * 打包你的扩展
> * 将你的扩展发布到 marketplace


我们希望在阅读本文您将能够生成自己的扩展的 Azure Data Studio 之后。 我们对仪表板见解 （对 SQL Server 运行的完美关系图）、 多个特定于 SQL Api 和继承自 Visual Studio Code 的扩展点一巨大现有组的支持。

如果您有个主意，但不确定如何开始，请提出问题或团队的推文： [azuredatastudio](https://twitter.com/azuredatastudio)。

您始终可以引用[Visual Studio Code 扩展指南](https://code.visualstudio.com/docs/extensions/overview)因为它涵盖了所有现有的 Api 和模式。


若要了解如何使用 T-SQL 在 Azure Data Studio 中，完成 T-SQL 编辑器教程：

> [!div class="nextstepaction"]
> [使用 TRANSACT-SQL 编辑器来创建数据库对象](tutorial-sql-editor.md)。
