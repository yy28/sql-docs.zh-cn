---
title: "使用 SSMS 部署 SSIS 项目 | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 17670ea5b9cc4f0795a0aa8801a1c9b496ed580b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="deploy-an-ssis-project-with-sql-server-management-studio-ssms"></a>使用 SQL Server Management Studio (SSMS) 部署 SSIS 项目
本快速入门演示如何使用 SQL Server Management Studio (SSMS) 连接到 SSIS 目录数据库，然后运行 Integration Services 部署向导以将 SSIS 项目部署到 SSIS 目录。 

SQL Server Management Studio 是一种集成环境，用于管理从 SQL Server 到 SQL 数据库的任何 SQL 基础结构。 有关 SSMS 的详细信息，请参阅 [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)。

## <a name="prerequisites"></a>先决条件

开始之前，请确保具有最新版本的 SQL Server Management Studio。 若要下载 SSMS，请参阅[下载 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

## <a name="connect-to-the-ssisdb-database"></a>连接到 SSISDB 数据库

使用 SQL Server Management Studio 与 SSIS 目录建立连接。 

> [!NOTE]
> Azure SQL 数据库服务器侦听端口 1433。 如果尝试从企业防火墙内连接到 Azure SQL 数据库服务器，必须在企业防火墙中打开该端口，才能成功连接。

1. 打开 SQL Server Management Studio。

2. 在“连接到服务器”对话框中，输入以下信息：

   | 设置       | 建议的值 | 详细信息 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **服务器类型** | 数据库引擎 | 此值是必需的。 |
   | **服务器名称** | 完全限定服务器名称 | 如果正在连接到 Azure SQL 数据库服务器，名称按以下格式：`<server_name>.database.windows.net`。 |
   | **身份验证** | SQL Server 身份验证 | 本快速入门使用 SQL 身份验证。 |
   | **登录** | 服务器管理员帐户 | 此帐户是在创建服务器时指定的帐户。 |
   | **密码** | 服务器管理员帐户的密码 | 此密码是在创建服务器时指定的密码。 |

3. 单击 **“连接”**。 对象资源管理器窗口在 SSMS 中打开。 

4. 在对象资源管理器中，展开“Integration Services 目录”，然后展开“SSISDB”查看 SSIS 目录数据库中的对象。

## <a name="start-the-integration-services-deployment-wizard"></a>启动 Integration Services 部署向导
1. 在对象资源管理器中，在展开“Integration Services 目录”节点和“SSISDB”后，展开一个项目文件夹。

2.  选择“项目”节点。

3.  右键单击“项目”节点，选择“部署项目”。 Integration Services 部署向导随即打开。 可以从当前目录或从文件系统部署项目。

## <a name="deploy-a-project-with-the-wizard"></a>使用向导部署项目
1. 在向导的“简介”页上查看简介。 单击“下一步”打开“选择源”页。

2. 在“选择源”页上，选择要部署的现有 SSIS 项目。
    -   若要部署你所创建的项目部署文件，请选择“项目部署文件”  并输入 .ispac 文件的路径。
    -   若要部署位于 SSIS 目录中的项目，请选择“Integration Services 目录”，然后输入目录中该项目的服务器名称和路径。
    单击“下一步”  以查看“选择目标”  页。
  
3.  在“选择目标”页上，选择项目的目标。
    -   输入完全限定服务器名称。 如果目标服务器是 Azure SQL 数据库服务器，则名称采用以下格式：`<server_name>.database.windows.net`。
    -   然后单击“浏览”，在 SSISDB 中选择目标文件夹。
    单击“下一步”打开“查看”页。  
  
4.  在“查看”页上，查看所选的设置。
    -   可以通过单击 **“上一步”**或单击左窗格中的任意步骤来更改所做的选择。
    -   单击“部署”  以启动部署过程。
  
5.  部署过程完成之后，“结果”页随即打开。 该页显示每个操作是成功了还是失败了。
    -   如果操作失败，则单击“结果”列中的“失败”以显示错误说明。
    -   （可选）单击“保存报告...”以将结果保存到某一 XML 文件。
    -   单击“关闭”以退出向导。

## <a name="next-steps"></a>后续步骤
- 考虑部署包的其他方式。
    - [使用 Transact-SQL (SSMS) 部署 SSIS 包](./ssis-quickstart-deploy-tsql-ssms.md)
    - [使用 Transact-SQL (VS Code) 部署 SSIS 包](ssis-quickstart-deploy-tsql-vscode.md)
    - [从命令提示符部署 SSIS 包](./ssis-quickstart-deploy-cmdline.md)
    - [使用 PowerShell 部署 SSIS 包](ssis-quickstart-deploy-powershell.md)
    - [使用 C# 部署 SSIS 包](./ssis-quickstart-deploy-dotnet.md) 
- 运行已部署的包。 若要运行包，可以从多个工具和语言中进行选择。 有关详细信息，请参阅下文：
    - [使用 SSMS 运行 SSIS 包](./ssis-quickstart-run-ssms.md)
    - [使用 Transact-SQL (SSMS) 运行 SSIS 包](./ssis-quickstart-run-tsql-ssms.md)
    - [使用 Transact-SQL (VS Code) 运行 SSIS 包](ssis-quickstart-run-tsql-vscode.md)
    - [从命令提示符运行 SSIS 包](./ssis-quickstart-run-cmdline.md)
    - [使用 PowerShell 运行 SSIS 包](ssis-quickstart-run-powershell.md)
    - [使用 C# 运行 SSIS 包](./ssis-quickstart-run-dotnet.md) 
