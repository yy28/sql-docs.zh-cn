---
title: "使用 TRANSACT-SQL (SQL 快速入门中的 R) 中的 R 代码 |Microsoft 文档"
ms.custom: SQL2016_New_Updated
ms.date: 08/20/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 4e6fe30d-a105-4d5b-bc05-5e5204753847
caps.latest.revision: "36"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 9c0896ca67df3d8000fae8f3cd3d336b047ee481
ms.sourcegitcommit: d7dcbcebbf416298f838a39dd5de6a46ca9f77aa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2018
---
# <a name="using-r-code-in-transact-sql-r-in-sql-quickstart"></a>使用 TRANSACT-SQL (SQL 快速入门中的 R) 中的 R 代码

本教程将带你演练从 T-SQL 存储过程调用 R 脚本的基础技术。

**学习内容**

+ 如何在 T-SQL 函数中嵌入 R
+ 有关使用 R 和 SQL 数据类型和数据对象的一些提示
+ 如何创建简单的模型，并将其保存到 SQL Server
+ 如何创建预测和使用模型 R 绘图

**估计的时间**

30 分钟，不包括安装

## <a name="prerequisites"></a>必要條件

你必须访问 SQL Server 的实例与已安装下列项之一：

+ SQL Server 自 2017 年 1 机器学习服务，与安装的 R 语言
+ SQL Server 2016 R Services

SQL Server 实例可以是 Azure 虚拟机或本地。 只需注意，外部脚本功能默认处于禁用状态，因此你可能需要执行一些附加步骤以使其正常工作。

若要运行包含 R 脚本的 SQL 查询，可以使用任何其他应用程序可以连接到数据库并运行 T-SQL 代码。 SQL 专业人员可以使用 SQL Server Management Studio (SSMS) 或 Visual Studio。

对于本教程，以显示运行在 SQL Server，R 是多么容易，我们使用新**mssql 扩展 Visual Studio Code**。 VS Code 是一个免费的开发环境，可以在 Linux、 macOS 或 Windows 上运行。 **Mssql**扩展是一个轻型的运行 T-SQL 查询扩展。 若要安装该开发环境，请参阅以下文章：[使用用于 Visual Studio Code 的 mssql 扩展](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode)。

## <a name="connect-to-a-database-and-run-a-hello-world-test-script"></a>连接到数据库并运行 Hello World 测试脚本

1. 在 Visual Studio Code 中，创建一个新的文本文件并将其命名为 BasicRSQL.sql。
2. 在此文件处于打开状态的情况下，按 CTRL+SHIFT+P（在 macOS 上为 COMMAND + P），键入 **sql** 来列出 SQL 命令，然后选择 **CONNECT**。 Visual Studio 代码会提示你创建使用连接到特定的数据库时的配置文件。 这是可选的但它可以更轻松地切换数据库和登录名。
    + 选择服务器或 SQL Server 中的 R 安装位置的实例。
    + 使用一个有权创建新数据库、运行 SELECT 语句并查看表定义的帐户。
2. 如果连接成功，则你应当能够在状态栏中看到服务器和数据库名称以及你的当前凭据。 如果连接失败，请检查计算机名称和服务器名称是否正确。
3. 粘贴以下语句并运行该语句。

    ```sql
    EXEC sp_execute_external_script
      @language =N'R',
      @script=N'OutputDataSet<-InputDataSet',
      @input_data_1 =N'SELECT 1 AS hello'
      WITH RESULT SETS (([hello] int not null));
    GO
    ```

    在 Visual Studio Code 中，你可以突出显示你要运行的代码并按 CTRL+SHIFT+E。 如果这难以记住，你可以更改此组合键！ 请参阅[自定义快捷键绑定](https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts)。

    ![rsql-basictut_hello1code](media/rsql-basictut-hello1code.PNG)

**结果**

![rsql_basictut_hello1](media/rsql-basictut-hello1.PNG)

## <a name="troubleshooting"></a>故障排除

+ 如果你将获得此查询的任何错误，安装可能不完整。 在使用 SQL Server 安装向导添加该功能后，你必须执行一些额外的步骤来启用外部代码库。  请参阅[安装 SQL Server R Services](../r/set-up-sql-server-r-services-in-database.md)。

+ 确保启动板服务正在运行。 取决于你的环境，你可能需要使 R 辅助角色帐户能够连接到 SQL Server，安装额外的网络库，启用远程代码执行，或者在配置所有项后重新启动实例。 请参阅 [R Services 安装和升级常见问题](../r/upgrade-and-installation-faq-sql-server-r-services.md)

+ 若要获取 Visual Studio Code，请参阅[下载和安装 Visual Studio Code](https://code.visualstudio.com/Download)。

## <a name="next-lesson"></a>下一课

现在，你的实例已准备好使用 R，让我们开始吧。

第 1 课：[使用输入和输出](rtsql-working-with-inputs-and-outputs.md)

第 2 课： [R 和 SQL 数据类型和数据对象](rtsql-r-and-sql-data-types-and-data-objects.md)

第 3 课：[与 SQL Server 数据的使用 R 函数](rtsql-using-r-functions-with-sql-server-data.md)

第 4 课：[创建预测模型](rtsql-create-a-predictive-model-r.md)

第 5 课：[预测和模型中的绘图](rtsql-predict-and-plot-from-model.md)
