---
title: "使用 TRANSACT-SQL (VS Code) 运行 SSIS 包 |Microsoft 文档"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: a912bf7f7944d4af3d41c5596e67aa77f3214112
ms.contentlocale: zh-cn
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-from-visual-studio-code-with-transact-sql"></a>从 Visual Studio Code 使用 TRANSACT-SQL 运行 SSIS 包
本快速入门演示如何使用 Visual Studio 代码连接到 SSIS 目录数据库，然后使用 TRANSACT-SQL 语句运行 SSIS 包存储在 SSIS 目录中。

Visual Studio Code 是 Windows、 macOS，和支持的扩展，包括的 Linux 的代码编辑器`mssql`用于连接到 Microsoft SQL Server、 Azure SQL 数据库或 Azure SQL 数据仓库的扩展。 有关 VS Code 的详细信息，请参阅[Visual Studio Cod](https://code.visualstudio.com/)。

## <a name="prerequisites"></a>先决条件

在开始之前，请确保已安装最新版本的 Visual Studio Code 和加载`mssql`扩展。 若要下载这些工具，请参阅以下页面：
-   [下载 Visual Studio Code](https://code.visualstudio.com/Download)
-   [mssql 扩展](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)

## <a name="set-language-mode-to-sql-in-vs-code"></a>将语言模式设置为在 VS Code 中的 SQL

若要启用`mssql`命令和 T-SQL 的 IntelliSense，组的语言模式设置为**SQL**在 Visual Studio 代码中。

1. 打开 Visual Studio 代码，然后打开一个新窗口。 

2. 单击**纯文本**中状态栏的右下角。

3. 在**选择的语言模式**下拉列表菜单中打开时，选择或输入**SQL**，然后按**ENTER**将语言模式设置为 SQL。 

## <a name="connect-to-the-ssis-catalog-database"></a>连接到 SSIS 目录数据库

使用 Visual Studio Code 建立到 SSIS 目录的连接。

> [!IMPORTANT]
> 在继续之前，请确保你有服务器、 数据库和准备好的登录信息。 如果在您开始输入的连接配置文件信息后，你可以将你焦点更改从 Visual Studio 代码，你必须重新开始创建的连接配置文件。

1. 在 VS Code 中，按**CTRL + SHIFT + P** (或**F1**) 以打开命令控制板。

2. 类型**sqlcon**按**ENTER**。

3. 按**ENTER**选择**创建连接配置文件**。 此步骤将创建您的 SQL Server 实例的连接配置文件。

4. 按照提示为新连接配置文件指定连接属性。 指定每个值后, 按**ENTER**以继续。 

   | 设置       | 建议的值 | 详细信息 |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **服务器名称** | 完全限定的服务器名称 | 如果你正在连接到 Azure SQL 数据库服务器，名称是按以下格式： `<server_name>.database.windows.net`。 |
   | **数据库名称** | **SSISDB** | 要连接到数据库的名称。 |
   | **身份验证** | SQL 登录名| 此快速开始使用 SQL 身份验证。 |
   | **用户名** | 与服务器管理员帐户 | 这是你在创建服务器时指定的帐户。 |
   | **密码 （SQL 登录名）** | 你的服务器管理员帐户的密码 | 这是你在创建服务器时指定的密码。 |
   | **保存的密码？** | 是或否 | 如果你不希望每次输入的密码，选择是。 |
   | **输入此配置文件的名称** | 一个配置文件名称，如**mySSISServer** | 保存配置文件名称对后续登录名可加快你的连接。 | 

5. 按**ESC**键关闭通知你，该配置文件已创建并已连接的信息消息。

6. 在状态栏中验证连接。

## <a name="run-the-t-sql-code"></a>运行 T-SQL 代码
运行下面的 TRANSACT-SQL 代码，以运行 SSIS 包。

1. 在**编辑器**窗口中，在空查询窗口中输入以下查询。 (此代码是由生成的代码**脚本**选项**执行包**在 SSMS 中的对话框。)

2. 更新中的参数值`catalog.create_execution`存储于您的系统的过程。

3. 按**CTRL + SHIFT + E**以运行该代码并运行包。

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
    - [运行 SSIS 包使用 TRANSACT-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [在命令提示符下运行 SSIS 包](./ssis-quickstart-run-cmdline.md)
    - [使用 PowerShell 运行 SSIS 包](ssis-quickstart-run-powershell.md)
    - [使用 C# 运行 SSIS 包](./ssis-quickstart-run-dotnet.md) 

