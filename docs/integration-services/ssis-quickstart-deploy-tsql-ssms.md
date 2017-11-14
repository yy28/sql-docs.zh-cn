---
title: "部署的 SSIS 项目使用 TRANSACT-SQL (SSMS) |Microsoft 文档"
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
ms.openlocfilehash: e97fb20f5b0ee10aa3e5de690676b7e0bb797b4c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/22/2017

---
# <a name="deploy-an-ssis-project-from-ssms-with-transact-sql"></a>部署的 SSIS 项目，从 SSMS 使用 TRANSACT-SQL

本快速入门演示如何使用 SQL Server Management Studio (SSMS) 连接到 SSIS 目录数据库，然后使用 TRANSACT-SQL 语句将 SSIS 项目部署到 SSIS 目录。 

> [!NOTE]
> 连接到 SSMS 的 Azure SQL 数据库服务器时，本文中所述的方法不可用。 `catalog.deploy_project`存储的过程需要到路径`.ispac`（在本地） 本地文件系统中的文件。

SQL Server Management Studio 是用于管理任何 SQL 基础结构中，从到 SQL 数据库的 SQL Server 的集成的环境。 有关 SSMS 的详细信息，请参阅[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)。

## <a name="prerequisites"></a>先决条件

在开始之前，请确保你有最新版本的 SQL Server Management Studio。 若要下载 SSMS，请参阅[下载 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

## <a name="connect-to-the-ssis-catalog-database"></a>连接到 SSIS 目录数据库

使用 SQL Server Management Studio 来建立与 SSIS 目录的连接。 

> [!NOTE]
> Azure SQL 数据库服务器在端口 1433年上侦听。 如果你正在尝试连接到 Azure SQL 数据库服务器从企业防火墙内，此端口必须为你成功连接到企业防火墙中打开。

1. 打开 SQL Server Management Studio。

2. 在**连接到服务器**对话框框中，输入以下信息：

   | 设置       | 建议的值 | 详细信息 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **服务器类型** | 数据库引擎 | 此值是必需的。 |
   | **服务器名称** | 完全限定的服务器名称 |  |
   | **身份验证** | SQL Server 身份验证 | 此快速开始使用 SQL 身份验证。 |
   | **登录** | 与服务器管理员帐户 | 这是你在创建服务器时指定的帐户。 |
   | **密码** | 你的服务器管理员帐户的密码 | 这是你在创建服务器时指定的密码。 |

3. 单击 **“连接”**。 在 SSMS 中打开对象资源管理器窗口。 

4. 在对象资源管理器，展开**Integration Services 目录**然后展开**SSISDB** SSIS 目录数据库中查看的对象。

## <a name="run-the-t-sql-code"></a>运行 T-SQL 代码
运行下面的 TRANSACT-SQL 代码，若要部署的 SSIS 项目。

1.  在 SSMS 中，打开新查询窗口并粘贴以下代码。

2.  更新中的参数值`catalog.deploy_project`存储于您的系统的过程。

3.  请确保 SSISDB 是当前数据库。

4.  运行该脚本。

5. 在对象资源管理器，刷新的内容**SSISDB**如有必要，并检查你部署的项目。

```sql
DECLARE @ProjectBinary AS varbinary(max)
DECLARE @operation_id AS bigint
SET @ProjectBinary =
    (SELECT * FROM OPENROWSET(BULK '<project_file_path>.ispac', SINGLE_BLOB) AS BinaryData)

EXEC catalog.deploy_project @folder_name = '<target_folder>',
    @project_name = '<project_name',
    @Project_Stream = @ProjectBinary,
    @operation_id = @operation_id out
```

## <a name="next-steps"></a>后续步骤
- 考虑使用其他方法来部署的包。
    - [部署 SSIS 包使用 SSMS](./ssis-quickstart-deploy-ssms.md)
    - [部署 SSIS 包使用 TRANSACT-SQL (VS Code)](ssis-quickstart-deploy-tsql-vscode.md)
    - [部署 SSIS 包从命令提示符](./ssis-quickstart-deploy-cmdline.md)
    - [部署 SSIS 包使用 PowerShell](ssis-quickstart-deploy-powershell.md)
    - [部署使用 C# SSIS 包](./ssis-quickstart-deploy-dotnet.md) 
- 运行部署的包。 若要运行包，你可以从多个工具和语言选择。 有关详细信息，请参阅以下文章：
    - [使用 SSMS 中运行 SSIS 包](./ssis-quickstart-run-ssms.md)
    - [运行 SSIS 包使用 TRANSACT-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [使用 TRANSACT-SQL (VS Code) 运行 SSIS 包](ssis-quickstart-run-tsql-vscode.md)
    - [在命令提示符下运行 SSIS 包](./ssis-quickstart-run-cmdline.md)
    - [使用 PowerShell 运行 SSIS 包](ssis-quickstart-run-powershell.md)
    - [使用 C# 运行 SSIS 包](./ssis-quickstart-run-dotnet.md) 

