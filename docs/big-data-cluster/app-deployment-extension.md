---
title: 应用部署扩展
titleSuffix: SQL Server big data clusters
description: 将 Python 或 R 脚本部署为 SQL Server 2019 大数据群集 （预览版） 上的应用程序。
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1e5ab6364437432c803a364abd50ef5b1af4f8f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958913"
---
# <a name="how-to-use-vs-code-to-deploy-applications-to-sql-server-big-data-clusters"></a>如何使用 VS Code 来部署应用程序到 SQL Server 大数据群集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍如何向 SQL Server 大数据群集应用程序部署扩展中使用 Visual Studio Code 部署应用程序。 CTP 2.3 中引入了此功能。 

## <a name="prerequisites"></a>先决条件

- [Visual Studio Code](https://code.visualstudio.com/)。
- [SQL Server 大数据群集](big-data-cluster-overview.md)CTP 2.3 或更高版本。

## <a name="capabilities"></a>功能

在 Visual Studio Code 中，此扩展插件支持以下任务：

- 使用 SQL Server 大数据群集进行身份验证。
- 从 GitHub 存储库部署的受支持运行时检索应用程序模板。
- 管理用户的工作区中当前打开的应用程序模板。
- 部署应用程序通过 YAML 格式规范。
- 管理 SQL Server 大数据群集中部署的应用。
- 查看所有已部署的应用中的其他信息的一侧栏。
- 生成一个运行的规范，以使用该应用程序或从群集中删除该应用程序。
- 使用已部署的应用，通过运行规范 YAML。

以下部分逐步完成安装过程，并提供扩展的工作原理的概述。 

### <a name="install"></a>安装

在 VS Code 中首次安装应用程序部署扩展：

1. 下载[应用将部署扩展](https://aka.ms/app-deploy-vscode)VS 代码的一部分安装扩展。

1. 启动 VS Code 并导航到扩展侧栏。

1. 单击`…`侧栏并选择顶部的上下文菜单`Install from vsix`。

   ![安装 VSIX](media/vs-extension/install_vsix.png)

1. 查找`sqlservbdc-app-deploy.vsix`文件下载，然后选择要安装。

SQL Server 大数据群集应用程序部署后安装扩展，它会提示你重新加载 VS Code。 现在应看到在 SQL Server BDC 应用程序资源管理器在 VS Code 侧栏中。

### <a name="app-explorer"></a>应用程序资源管理器

单击侧栏以加载侧面板，其中显示在应用程序资源管理器中的扩展。 应用程序资源管理器的以下示例屏幕截图显示没有应用程序规范可用：

<img src="media/vs-extension/app_explorer.png" width=350px></img>
<!--![App Explorer](media/vs-extension/app_explorer.png)-->

#### <a name="new-connection"></a>新的连接

若要连接到群集终结点，请使用以下方法之一：

- 单击显示在底部状态栏上`SQL Server BDC Disconnected`。
- 或单击`New Connection`通过箭头指向在门口到顶部的按钮。

   ![新的连接](media/vs-extension/connect_to_cluster.png)

VS Code 会提示输入相应的终结点、 用户名和密码。 如果给出正确的凭据和应用程序终结点，VS Code 会通知您已连接到群集，你将看到在侧栏中填充任何已部署的应用。 如果您已成功连接，保存你的终结点和用户名到`./sqldbc`作为用户配置文件的一部分。 曾经将保存没有密码或令牌。 时再次登录，在提示符下将预先填充你的已保存的主机和用户名，但始终要求你输入密码。 如果你想要连接到不同的群集终结点，只需单击`New Connection`试。 如果关闭 VS Code 或打开不同的工作区并将需要重新连接，连接会自动关闭。

### <a name="app-template"></a>应用模板

若要部署新的应用程序从某个我们的模板，请单击`New App Template`按钮上`App Specifications`窗格中，其中系统将提示输入名称、 运行时，以及你想要在本地计算机上将在此新应用程序的位置。 建议，您将其放在当前的 VS Code 工作区中，以便您可以使用的全部功能的扩展，但将其放在本地文件系统中的任意位置。

![新应用程序模板](media/vs-extension/new_app_template.png)

完成后，新的应用程序模板已搭建基架为你在你指定的位置和部署`spec.yaml`将在你的工作区中打开。 如果您选择的目录是在工作区中，您还将看到下面列出`App Specifications`窗格：

![加载应用程序模板](media/vs-extension/loading_app_template.png)

模板是一个简单`Hello World`应用的布局方式，如下所示：

- **spec.yaml**
   - 指示如何将应用部署的群集
- **run-spec.yaml**
   - 告知你希望如何调用您的应用程序的群集
- **handler.py**
   - 这是由指定源代码文件`src`中 `spec.yaml`
   - 它具有名为的一个函数`handler`认为`entrypoint`应用程序中所示的`spec.yaml`。 采用名为的字符串输入`msg`，并返回字符串输出名为`out`。 中指定这些`inputs`并`outputs`的`spec.yaml`。

如果您不希望已搭建基架的模板，只是希望`spec.yaml`你已生成的应用部署，请单击`New Deploy Spec`按钮旁边`New App Template`按钮，并通过相同的过程，但您只需接收`spec.yaml`，您可以修改您选择的方式。

### <a name="deploy-app"></a>将应用部署

可能会立即部署此应用程序中的通过代码小视窗`Deploy App`中`spec.yaml`或按快如闪电文件夹按钮旁边`spec.yaml`应用规范菜单中的文件。 该扩展将在目录中的所有文件进行都压缩，您`spec.yaml`所在并将您的应用程序部署到群集。 

>[!NOTE]
>请确保所有应用文件所在的同一目录中你`spec.yaml`。 `spec.yaml`必须是您应用的源代码目录的根级别。 

![部署应用程序按钮](media/vs-extension/deploy_app_lightning.png)

![部署应用 CodeLens](media/vs-extension/deploy_app_codelens.png)

应用可供在侧栏中应用的状态上基于消耗时，你将收到通知：

![部署应用](media/vs-extension/app_deploy.png)

![应用就绪侧边栏](media/vs-extension/app_ready_side_bar.png)

![应用就绪通知](media/vs-extension/app_ready_notification.png)

在窗格中，你将能够看到您的可用以下：

使用以下信息在侧栏中，可以查看所有已部署的应用：

- state
- version
- 输入参数
- 输出参数
- 链接
  - swagger
  - details

如果单击`Links`，你将看到，您可以访问`swagger.json`的已部署的应用，以便您可以编写您自己调用您的应用程序的客户端：

![swagger](media/vs-extension/swagger.png)

请参阅[使用大数据群集上的应用程序](big-data-cluster-consume-apps.md)有关详细信息。

### <a name="app-run"></a>应用运行

应用程序准备就绪后，调用应用程序与`run-spec.yaml`提供作为应用程序模板的一部分：

![运行规范](media/vs-extension/run_spec.png)

指定您希望替代的任何字符串`hello`，然后再次运行它通过代码可重用功能区链接或侧栏中的闪电形按钮旁边`run-spec.yaml`。 如果由于任何原因没有运行规范，请在群集中生成一个从已部署的应用：

![获取运行规范](media/vs-extension/get_run_spec.png)

有一个并对其进行编辑你感到满意后，运行它。 应用程序运行完毕时，VS Code 将返回适当的反馈：

![应用程序输出](media/vs-extension/app_output.png)

正如您所看到上述，临时中提供了输出`.json`工作区中的文件。 如果你想要保留此输出，可随时将其保存，否则，在右将删除下列它。 如果您的应用程序不有任何输出打印到文件，将仅获取`Successful App Run`底部的通知。 如果没有成功运行，你将收到相应的错误消息，这样有助于确定出错的原因。

当运行应用时，有多种方式将参数传递：

你可以指定通过所需的所有输入`.json`，即：

- `inputs: ./example.json`

当调用已部署的应用，如果任何输入的参数是与生俱来的应用程序或用户指定和给定的输入参数是基元，如数组、 向量、 的数据帧之外的任何内容的复杂 JSON 等指定参数类型直接在行时它调用应用程序中：

- 向量
    - `inputs:`
        - `x: [1, 2, 3]`
- 矩阵
    - `inputs:`
        - `x: [[A,B,C],[1,2,3]]`
- Object
    - `inputs:`
        - `x: {A: 1, B: 2, C: 3}`

或为一个字符串，提供的相对或绝对文件路径作为`.txt`， `.json`，或`.csv`，为所需的输入提供的应用所需的格式。 文件分析基于`Node.js Path library`，其中文件路径定义为`string that contains a / or \ character`。

如果根据需要未提供输入的参数，则如果提供的字符串的文件路径，或该参数无效，具有不正确的文件路径将显示相应的错误消息。 负责提供给应用的创建者，以确保他们了解它们定义的参数。

若要删除应用，只需单击垃圾桶可按钮旁边的应用程序中`Deployed Apps`侧边窗格。

## <a name="next-steps"></a>后续步骤

了解如何将大数据群集在您的应用程序的 SQL Server 上部署的应用程序进行集成[使用大数据群集上的应用程序](big-data-cluster-consume-apps.md)有关详细信息。 此外可以对在其他示例引用[应用程序部署示例](https://aka.ms/sql-app-deploy)来尝试使用该扩展。

有关 SQL Server 大数据群集的详细信息，请参阅[什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)。


我们的目标是为你进行此扩展很有用，我们非常感激你的反馈。 请将它们发送到[[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]团队](https://aka.ms/sqlfeedback)。
