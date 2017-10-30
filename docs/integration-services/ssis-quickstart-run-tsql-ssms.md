---
title: "运行 SSIS 包使用 TRANSACT-SQL (SSMS) |Microsoft 文档"
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
ms.openlocfilehash: 1c656661f645ac9f5d1659800893290819525f39
ms.contentlocale: zh-cn
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-from-ssms-with-transact-sql"></a>运行 SSIS 包从 SSMS 使用 TRANSACT-SQL
本快速入门演示如何使用 SQL Server Management Studio (SSMS) 连接到 SSIS 目录数据库，然后使用 TRANSACT-SQL 语句运行 SSIS 包存储在 SSIS 目录中。

SQL Server Management Studio 是用于管理任何 SQL 基础结构中，从到 SQL 数据库的 SQL Server 的集成的环境。 有关 SSMS 的详细信息，请参阅[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)。

## <a name="prerequisites"></a>先决条件

在开始之前，请确保您拥有最新版本的 SQL Server Management Studio (SSMS)。 若要下载 SSMS，请参阅[下载 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

## <a name="connect-to-the-ssisdb-database"></a>连接到 SSISDB 数据库

使用 SQL Server Management Studio 来建立与 Azure SQL 数据库服务器上的 SSIS 目录的连接。 

> [!NOTE]
> Azure SQL 数据库服务器在端口 1433年上侦听。 如果你正在尝试连接到 Azure SQL 数据库服务器从企业防火墙内，此端口必须为你成功连接到企业防火墙中打开。

1. 打开 SQL Server Management Studio。

2. 在**连接到服务器**对话框框中，输入以下信息：

   | 设置       | 建议的值 | 详细信息 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **服务器类型** | 数据库引擎 | 此值是必需的。 |
   | **服务器名称** | 完全限定的服务器名称 | 如果你正在连接到 Azure SQL 数据库服务器，名称是按以下格式： `<server_name>.database.windows.net`。 |
   | **身份验证** | SQL Server 身份验证 | 此快速开始使用 SQL 身份验证。 |
   | **登录** | 与服务器管理员帐户 | 这是你在创建服务器时指定的帐户。 |
   | **密码** | 你的服务器管理员帐户的密码 | 这是你在创建服务器时指定的密码。 |

3.  单击 **“连接”**。 在 SSMS 中打开对象资源管理器窗口。

4. 在对象资源管理器，展开**Integration Services 目录**然后展开**SSISDB** SSIS 目录数据库中查看的对象。

## <a name="run-a-package"></a>运行包
运行下面的 TRANSACT-SQL 代码，以运行 SSIS 包。

1.  在 SSMS 中，打开新查询窗口并粘贴以下代码。 (此代码是由生成的代码**脚本**选项**执行包**在 SSMS 中的对话框。)

2.  更新中的参数值`catalog.create_execution`存储于您的系统的过程。

3.  请确保 SSISDB 是当前数据库。

4.  运行该脚本。

5. 在对象资源管理器，刷新的内容**SSISDB**如有必要，并检查你部署的项目。

```sql
Declare @execution_id bigint
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx',
    @execution_id=@execution_id OUTPUT,
    @folder_name=N'Deployed Projects',
      @project_name=N'Integration Services Project1',
    @use32bitruntime=False,
      @reference_id=Null
Select @execution_id
DECLARE @var0 smallint = 1
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,
    @object_type=50,
      @parameter_name=N'LOGGING_LEVEL',
      @parameter_value=@var0
EXEC [SSISDB].[catalog].[start_execution] @execution_id
GO
```

## <a name="next-steps"></a>后续步骤
- 考虑运行包的其他方式。
    - [使用 SSMS 中运行 SSIS 包](./ssis-quickstart-run-ssms.md)
    - [使用 TRANSACT-SQL (VS Code) 运行 SSIS 包](ssis-quickstart-run-tsql-vscode.md)
    - [在命令提示符下运行 SSIS 包](./ssis-quickstart-run-cmdline.md)
    - [使用 PowerShell 运行 SSIS 包](ssis-quickstart-run-powershell.md)
    - [使用 C# 运行 SSIS 包](./ssis-quickstart-run-dotnet.md) 

