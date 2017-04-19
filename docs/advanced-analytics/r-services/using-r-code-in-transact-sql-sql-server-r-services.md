---
title: "在 Transact-SQL 中使用 R 代码 (SQL Server R Services) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 4e6fe30d-a105-4d5b-bc05-5e5204753847
caps.latest.revision: 36
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d9da8f73ddaf3caf633260a97c2e056637489c8e
ms.lasthandoff: 04/11/2017

---
# <a name="using-r-code-in-transact-sql-sql-server-r-services"></a>在 Transact-SQL 中使用 R 代码 (SQL Server R Services)
本教程将带你演练从 T-SQL 存储过程调用 R 脚本的基础技术。 

**学习内容**

+ 关于 R 和 SQL 的数据类型与数据对象
+ 如何在 T-SQL 函数中嵌入 R 
+ 创建一个简单模型并将其保存在 SQL Server 中
+ 使用模型创建预测和 R 绘图   

**估计所需时间**

30 分钟，不包括安装 

## <a name="prerequisites"></a>先决条件

你必须对某个已安装了 R Services 的 SQL Server 实例具有访问权限。 该实例可以位于 Azure 虚拟机中，也可以位于本地。 你可以使用 SQL Server 2016 或 SQL Server vNext。


若要运行包括 R 脚本的 SQL 查询，请使用 SQL Server Management Studio (SSMS)、Visual Studio 或可以连接到数据库并运行临时 T-SQL 代码的任何其他应用程序。 为了演示在 SQL Server 内运行 R 是多么容易，我们将使用新的**用于 Visual Studio Code 的 mssql 扩展**，这是一个可以在 Linux、macOS 或 Windows 上运行的免费开发环境。 若要安装该开发环境，请参阅以下文章：[使用用于 Visual Studio Code 的 mssql 扩展](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode)。


## <a name="connect-to-a-database-and-run-a-hello-world-test-script"></a>连接到数据库并运行 Hello World 测试脚本

1. 在 Visual Studio Code 中，创建一个新的文本文件并将其命名为 BasicRSQL.sql。
2. 在此文件处于打开状态的情况下，按 CTRL+SHIFT+P（在 macOS 上为 COMMAND + P），键入 **sql** 来列出 SQL 命令，然后选择 **CONNECT**。 Visual Studio Code 会提示你创建在连接到特定数据库时要使用的配置文件。 这是可选的，但可以使得在各个数据库与登录名之间进行切换更为容易。
    + 选择一个已安装了 R Services 的服务器或实例。
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

    ![rsql-basictut_hello1code](../../advanced-analytics/r-services/media/rsql-basictut-hello1code.PNG)

**结果**

![rsql_basictut_hello1](../../advanced-analytics/r-services/media/rsql-basictut-hello1.PNG)
   
## <a name="troubleshooting"></a>故障排除

+ 如果运行此查询时遇到任何错误，则 R Services 的安装可能不完整。 在使用 SQL Server 安装向导添加该功能后，你必须执行一些额外的步骤来启用外部代码库。  请参阅[安装 SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)。

+ 确保启动板服务正在运行。 取决于你的环境，你可能需要使 R 辅助角色帐户能够连接到 SQL Server，安装额外的网络库，启用远程代码执行，或者在配置所有项后重新启动实例。 请参阅 [R Services 安装和升级常见问题](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md)

+ 若要获取 Visual Studio Code，请参阅[下载和安装 Visual Studio Code](https://code.visualstudio.com/Download)。

## <a name="next-step"></a>下一步

现在，你的 R Services 实例已准备就绪，让我们开始使用吧。 

步骤 1：[使用输入和输出](../../advanced-analytics/r-services/working-with-inputs-and-outputs-r-in-t-sql-tutorial.md)

步骤 2：[R 和 SQL 的数据类型与数据对象](../../advanced-analytics/r-services/r-and-sql-data-types-and-data-objects-r-in-t-sql-tutorial.md)

步骤 3：[对 SQL Server 数据使用 R 函数](../../advanced-analytics/r-services/using-r-functions-with-sql-server-data-r-in-t-sql-tutorial.md)

步骤 4：[创建预测模型](../../advanced-analytics/r-services/create-a-predictive-model-r-in-t-sql-tutorial.md)

步骤 5：[通过模型预测和绘图](../../advanced-analytics/r-services/predict-and-plot-from-model-r-in-t-sql-tutorial.md)


