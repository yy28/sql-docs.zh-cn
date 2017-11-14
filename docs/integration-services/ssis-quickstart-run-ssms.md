---
title: "使用 SSMS 中运行 SSIS 包 |Microsoft 文档"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: bbc17907311785ef98560493cb453b7b9b6d1556
ms.contentlocale: zh-cn
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-with-sql-server-management-studio-ssms"></a>运行 SSIS 包与 SQL Server Management Studio (SSMS)
本快速入门演示如何使用 SQL Server Management Studio (SSMS) 连接到 SSIS 目录数据库，然后运行 SSIS 包存储在 SSMS 对象资源管理器从 SSIS 目录中。

SQL Server Management Studio 是用于管理任何 SQL 基础结构中，从到 SQL 数据库的 SQL Server 的集成的环境。 有关 SSMS 的详细信息，请参阅[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)。

## <a name="prerequisites"></a>先决条件

在开始之前，请确保您拥有最新版本的 SQL Server Management Studio (SSMS)。 若要下载 SSMS，请参阅[下载 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

## <a name="connect-to-the-ssisdb-database"></a>连接到 SSISDB 数据库

使用 SQL Server Management Studio 来建立与 SSIS 目录的连接。 

> [!NOTE]
> Azure SQL 数据库服务器在端口 1433年上侦听。 如果你正在尝试连接到 Azure SQL 数据库服务器从企业防火墙内，此端口必须为你成功连接到企业防火墙中打开。

1. 打开 SQL Server Management Studio。

2. 在**连接到服务器**对话框框中，输入以下信息：

   | 设置       | 建议的值 | 详细信息 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **服务器类型** | 数据库引擎 | 此值是必需的。 |
   | **服务器名称** | 完全限定的服务器名称 | 如果你正在连接到 Azure SQL 数据库服务器，名称是按以下格式： `<server_name>.database.windows.net`。 |
   | **身份验证** | SQL Server 身份验证 | 此快速开始使用 SQL 身份验证。 |
   | **登录** | 与服务器管理员帐户 | 这是你在创建服务器时指定的帐户。 |
   | **密码** | 你的服务器管理员帐户的密码 | 这是你在创建服务器时指定的密码。 |

3. 单击 **“连接”**。 在 SSMS 中打开对象资源管理器窗口。 

4. 在对象资源管理器，展开**Integration Services 目录**然后展开**SSISDB** SSIS 目录数据库中查看的对象。

## <a name="run-a-package"></a>运行包

1. 在对象资源管理器，选择你想要运行的包。

2. 右键单击并选择**执行**。 **执行包**对话框随即打开。

3.  通过使用上的设置来配置包执行**参数**，**连接管理器**，和**高级**执行包对话框中的选项卡。

4.  单击确定以运行包。

## <a name="next-steps"></a>后续步骤
- 考虑运行包的其他方式。
    - [运行 SSIS 包使用 TRANSACT-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [使用 TRANSACT-SQL (VS Code) 运行 SSIS 包](ssis-quickstart-run-tsql-vscode.md)
    - [在命令提示符下运行 SSIS 包](./ssis-quickstart-run-cmdline.md)
    - [使用 PowerShell 运行 SSIS 包](ssis-quickstart-run-powershell.md)
    - [使用 C# 运行 SSIS 包](./ssis-quickstart-run-dotnet.md) 

