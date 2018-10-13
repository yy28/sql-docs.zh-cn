---
title: "\"Hello World\"基本 R 代码执行的 T-SQL （SQL Server 机器学习） 中的快速入门 |Microsoft Docs"
description: SQL Server 中的 R 脚本的快速入门。 了解调用 R 脚本在你好 world 练习使用 sp_execute_external_script 系统存储过程的基础知识。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/08/2018
ms.topic: quickstart
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 1a51fcb9e67bef48346ff74ebfb1e911a6ee3365
ms.sourcegitcommit: ce4b39bf88c9a423ff240a7e3ac840a532c6fcae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2018
ms.locfileid: "48878080"
---
# <a name="quickstart-hello-world-r-script-in-sql-server"></a>快速入门： SQL Server 中的"Hello world"R 脚本 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 包括对数据科学驻留的 SQL Server 数据分析的 R 语言支持。 在 R 脚本可以包含的开放源代码 R 函数、 第三方 R 库或内置的 Microsoft R 库等[RevoScaleR](../r/revoscaler-overview.md)用于在规模较大的预测分析。 

脚本执行是通过存储过程，使用以下方法之一：

+ 内置[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)存储过程，传递作为输入参数中的 R 脚本。
+ 包装中的 R 脚本[自定义存储过程](sqldev-in-database-r-for-sql-developers.md)你创建的。

在本快速入门教程，了解关键概念，通过运行"Hello World"R 脚本 inT SQL，简介**sp_execute_external_script**系统存储过程。 

## <a name="prerequisites"></a>必要條件

本演练需要访问 SQL Server 的实例与已安装以下项之一：

+ [SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)，与安装的 R 语言
+ [SQL Server 2016 R 服务](../install/sql-r-services-windows-install.md)

  SQL Server 实例可以是 Azure 虚拟机或本地。 只需注意，外部脚本编写功能默认处于禁用状态，因此可能需要[启用外部脚本](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)并确认**SQL Server Launchpad 服务**在开始之前运行。

+ 用于运行 SQL 查询的工具。 可以使用任何应用程序可以连接到 SQL Server 数据库并运行 T-SQL 代码。 SQL 专业人员可以使用 SQL Server Management Studio (SSMS) 或 Visual Studio。

对于本快速入门，以展示如何轻松地运行 R 在 SQL Server，我们已使用新**适用于 Visual Studio Code 的 mssql 扩展**。 VS Code 是一个免费的开发环境，可以在 Linux、 macOS 或 Windows 上运行。 **Mssql**扩展是一个轻型扩展运行 T-SQL 查询。 若要获取 Visual Studio Code，请参阅[下载和安装 Visual Studio Code](https://code.visualstudio.com/Download)。 若要添加**mssql**扩展，请参阅以下文章：[使用适用于 Visual Studio Code 的 mssql 扩展](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode)。

## <a name="connect-to-a-database-and-run-a-hello-world-test-script"></a>连接到数据库并运行 Hello World 测试脚本

1. 在 Visual Studio Code 中，创建一个新的文本文件并将其命名为 BasicRSQL.sql。

2. 在此文件处于打开状态的情况下，按 CTRL+SHIFT+P（在 macOS 上为 COMMAND + P），键入 **sql** 来列出 SQL 命令，然后选择 **CONNECT**。 Visual Studio Code 会提示您创建用于连接到特定数据库时使用的配置文件。 这是可选的但它可以更轻松地切换之间数据库和登录名。
    + 选择服务器或已安装 SQL Server 中的 R 实例。
    + 使用一个有权创建新数据库、运行 SELECT 语句并查看表定义的帐户。

2. 如果连接成功，则你应当能够在状态栏中看到服务器和数据库名称以及你的当前凭据。 如果连接失败，请检查计算机名称和服务器名称是否正确。

3. 粘贴以下语句并运行该语句。

    ```sql
    EXEC sp_execute_external_script
      @language =N'R',
      @script=N'OutputDataSet<-InputDataSet',
      @input_data_1 =N'SELECT 1 AS hello'
      WITH RESULT SETS (([Hello World] int));
    GO
    ```

此存储过程的输入包括：

+ *@language* 参数定义的语言扩展。 若要调用，在这种情况下，。
+ *@script* 参数定义传递给 R 运行时的命令。 必须以 Unicode 文本形式将整个 R 脚本封装在此参数中。 还可将文本添加到 **nvarchar** 类型的变量并调用该变量。
+ *@input_data_1* 该查询中，传递给 R 运行时，将数据返回到 SQL Server 作为数据帧返回数据。
+ 使用结果集子句返回的数据的表的架构定义的 SQL Server，将"Hello World"添加列名称，为**int**的数据类型。

**结果**

![rsql_basictut_hello1](media/rsql-basictut-hello1.PNG)

如果此查询中获取的任何错误，请排除任何安装问题。 安装后则需要配置才能启用对外部代码库的使用。 请参阅[安装 SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)或[安装 SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)。同样，请确保快速启动板服务正在运行。 

取决于你的环境，你可能需要使 R 辅助角色帐户能够连接到 SQL Server，安装额外的网络库，启用远程代码执行，或者在配置所有项后重新启动实例。 有关详细信息，请参阅[R Services 的安装和升级常见问题](../r/upgrade-and-installation-faq-sql-server-r-services.md)

> [!TIP]
> 在 Visual Studio Code 中，你可以突出显示你要运行的代码并按 CTRL+SHIFT+E。 如果这难以记住，你可以更改此组合键！ 请参阅[自定义快捷键绑定](https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts)。
> 
> ![rsql-basictut_hello1code](media/rsql-basictut-hello1code.PNG)
> 

## <a name="next-steps"></a>后续步骤

现在，已确认你的实例已准备好与 R 一起使用，更详细地介绍构造输入和输出。

> [!div class="nextstepaction"]
> [快速入门： 处理输入和输出](rtsql-working-with-inputs-and-outputs.md)
