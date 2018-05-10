---
title: 使用 Transact-SQL (SSMS) 部署 SSIS 项目 | Microsoft Docs
ms.date: 09/25/2017
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.component: quick-start
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 975bf68b5d3255ff965e9092e84b2dabf982b90b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="deploy-an-ssis-project-from-ssms-with-transact-sql"></a>使用 Transact-SQL 从 SSMS 部署 SSIS 项目

快速入门将演示如何使用 SQL Server Management Studio (SSMS) 连接到 SSIS 目录数据库，然后使用 Transact-SQL 语句向 SSIS 目录部署 SSIS 项目。 

> [!NOTE]
> 使用 SSMS 连接至 Azure SQL 数据库服务器时，本文中所述的方法不可用。 `catalog.deploy_project` 存储过程需使用指向本地文件系统中 `.ispac` 文件的路径。

SQL Server Management Studio 是一种集成环境，用于管理从 SQL Server 到 SQL 数据库的任何 SQL 基础结构。 有关 SSMS 的详细信息，请参阅 [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)。

## <a name="prerequisites"></a>必备条件

开始之前，请确保具有最新版本的 SQL Server Management Studio。 若要下载 SSMS，请参阅[下载 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

## <a name="connect-to-the-ssis-catalog-database"></a>连接到 SSIS 目录数据库

使用 SQL Server Management Studio 与 SSIS 目录建立连接。 

> [!NOTE]
> Azure SQL 数据库服务器侦听端口 1433。 如果尝试从企业防火墙内连接到 Azure SQL 数据库服务器，必须在企业防火墙中打开该端口，才能成功连接。

1. 打开 SQL Server Management Studio。

2. 在“连接到服务器”对话框中，输入以下信息：

   | 设置       | 建议的值 | 详细信息 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **服务器类型** | 数据库引擎 | 此值是必需的。 |
   | **服务器名称** | 完全限定的服务器名称 |  |
   | **身份验证** | SQL Server 身份验证 | 本快速入门使用 SQL 身份验证。 |
   | **登录** | 服务器管理员帐户 | 此帐户是在创建服务器时指定的帐户。 |
   | **密码** | 服务器管理员帐户的密码 | 此密码是在创建服务器时指定的密码。 |

3. 单击 **“连接”**。 对象资源管理器窗口在 SSMS 中打开。 

4. 在对象资源管理器中，展开“Integration Services 目录”，然后展开“SSISDB”查看 SSIS 目录数据库中的对象。

## <a name="run-the-t-sql-code"></a>运行 T-SQL 代码
运行下面的 Transact-SQL 代码以部署 SSIS 项目。

1.  在 SSMS 中，打开新的查询窗口并粘贴以下代码。

2.  为系统更新 `catalog.deploy_project` 存储过程中的参数值。

3.  请确保 SSISDB 是当前数据库。

4.  运行该脚本。

5. 在对象资源管理器中，如有必要，请刷新 SSISDB 的内容，然后检查已部署的项目。

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
- 考虑部署包的其他方式。
    - [使用 SSMS 部署 SSIS 包](./ssis-quickstart-deploy-ssms.md)
    - [使用 Transact-SQL (VS Code) 部署 SSIS 包](ssis-quickstart-deploy-tsql-vscode.md)
    - [从命令提示符部署 SSIS 包](./ssis-quickstart-deploy-cmdline.md)
    - [使用 PowerShell 部署 SSIS 包](ssis-quickstart-deploy-powershell.md)
    - [使用 C# 部署 SSIS 包](./ssis-quickstart-deploy-dotnet.md) 
- 运行已部署的包。 若要运行包，可以从多个工具和语言中进行选择。 有关详细信息，请参阅下文：
    - [使用 SSMS 运行 SSIS 包](./ssis-quickstart-run-ssms.md)
    - [使用 Transact-SQL 运行 SSIS 包 (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [使用 Transact-SQL 运行 SSIS 包 (VS Code)](ssis-quickstart-run-tsql-vscode.md)
    - [从命令提示符运行 SSIS 包](./ssis-quickstart-run-cmdline.md)
    - [使用 PowerShell 运行 SSIS 包](ssis-quickstart-run-powershell.md)
    - [使用 C# 运行 SSIS 包](./ssis-quickstart-run-dotnet.md) 
