---
title: "部署使用 TRANSACT-SQL (VS Code) 的 SSIS 项目 |Microsoft 文档"
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
ms.sourcegitcommit: dd20fe12af6f1dcaf378d737961bc2ba354aabe5
ms.openlocfilehash: 2dc6de798ca76b43627a3c381fe628506c3e7480
ms.contentlocale: zh-cn
ms.lasthandoff: 10/04/2017

---
# <a name="deploy-an-ssis-project-from-visual-studio-code-with-transact-sql"></a>部署 SSIS 项目从 Visual Studio 代码使用 TRANSACT-SQL
本快速入门演示如何使用 Visual Studio 代码连接到 SSIS 目录数据库，然后使用 TRANSACT-SQL 语句将 SSIS 项目部署到 SSIS 目录。

> [!NOTE]
> 连接到 VS Code 的 Azure SQL 数据库服务器时，本文中所述的方法不可用。 `catalog.deploy_project`存储的过程需要到路径`.ispac`（在本地） 本地文件系统中的文件。

Visual Studio Code 是 Windows、 macOS，和支持的扩展，包括的 Linux 的代码编辑器`mssql`用于连接到 Microsoft SQL Server、 Azure SQL 数据库或 Azure SQL 数据仓库的扩展。 有关 VS Code 的详细信息，请参阅[Visual Studio Code](https://code.visualstudio.com/)。

## <a name="prerequisites"></a>先决条件

在开始之前，请确保已安装最新版本的 Visual Studio Code 和加载`mssql`扩展。 若要下载这些工具，请参阅以下页面：
-   [下载 Visual Studio Code](https://code.visualstudio.com/Download)
-   [mssql 扩展](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)

## <a name="set-language-mode-to-sql-in-vs-code"></a>将语言模式设置为在 VS Code 中的 SQL

若要启用`mssql`命令和 T-SQL 的 intellisense 功能，则将语言模式设置为**SQL**在 Visual Studio 代码中。

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
   | **服务器名称** | 完全限定的服务器名称 |  |
   | **数据库名称** | **SSISDB** | 要连接到数据库的名称。 |
   | **身份验证** | SQL 登录名| 此快速开始使用 SQL 身份验证。 |
   | **用户名** | 与服务器管理员帐户 | 这是你在创建服务器时指定的帐户。 |
   | **密码 （SQL 登录名）** | 你的服务器管理员帐户的密码 | 这是你在创建服务器时指定的密码。 |
   | **保存的密码？** | 是或否 | 如果你不希望每次输入的密码，选择是。 |
   | **输入此配置文件的名称** | 一个配置文件名称，如**mySSISServer** | 保存配置文件名称对后续登录名可加快你的连接。 | 

5. 按**ESC**键关闭通知你，该配置文件已创建并已连接的信息消息。

6. 在状态栏中验证连接。

## <a name="run-the-t-sql-code"></a>运行 T-SQL 代码
运行下面的 TRANSACT-SQL 代码，若要部署的 SSIS 项目。

1. 在**编辑器**窗口中，在空查询窗口中输入以下查询。

2. 更新中的参数值`catalog.deploy_project`存储于您的系统的过程。

3. 按**CTRL + SHIFT + E**来运行的代码和部署项目。

```sql
DECLARE @ProjectBinary AS varbinary(max)
DECLARE @operation_id AS bigint
SET @ProjectBinary = (SELECT * FROM OPENROWSET(BULK '<project_file_path>.ispac', SINGLE_BLOB) AS BinaryData)

EXEC catalog.deploy_project @folder_name = '<target_folder>',
    @project_name = '<project_name',
    @Project_Stream = @ProjectBinary,
    @operation_id = @operation_id out
```

## <a name="next-steps"></a>后续步骤
- 考虑使用其他方法来部署的包。
    - [部署 SSIS 包使用 SSMS](./ssis-quickstart-deploy-ssms.md)
    - [部署 SSIS 包使用 TRANSACT-SQL (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
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

