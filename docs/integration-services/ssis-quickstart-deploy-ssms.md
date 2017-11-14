---
title: "部署使用 SSMS 的 SSIS 项目 |Microsoft 文档"
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
ms.openlocfilehash: b9729343ab14563ee6264795d6f098f3c22e91bf
ms.contentlocale: zh-cn
ms.lasthandoff: 09/22/2017

---
# <a name="deploy-an-ssis-project-with-sql-server-management-studio-ssms"></a>部署的 SSIS 项目与 SQL Server Management Studio (SSMS)
本快速入门演示如何使用 SQL Server Management Studio (SSMS) 连接到 SSIS 目录数据库，然后运行 Integration Services 部署向导将 SSIS 项目部署到 SSIS 目录。 

SQL Server Management Studio 是用于管理任何 SQL 基础结构中，从到 SQL 数据库的 SQL Server 的集成的环境。 有关 SSMS 的详细信息，请参阅[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)。

## <a name="prerequisites"></a>先决条件

在开始之前，请确保你有最新版本的 SQL Server Management Studio。 若要下载 SSMS，请参阅[下载 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

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

## <a name="start-the-integration-services-deployment-wizard"></a>启动 Integration Services 部署向导
1. 在对象资源管理器，使用**Integration Services 目录**节点和**SSISDB**展开，展开项目文件夹。

2.  选择**项目**节点。

3.  右键单击**项目**节点，然后选择**部署项目**。 Integration Services 部署向导将打开。 你可以部署一个项目，从当前目录或从文件系统。

## <a name="deploy-a-project-with-the-wizard"></a>部署向导项目
1. 上**简介**页的向导中，查看简介。 单击**下一步**以打开**选择源**页。

2. 上**选择源**页上，选择要部署的现有 SSIS 项目。
    -   若要部署你所创建的项目部署文件，请选择“项目部署文件”  并输入 .ispac 文件的路径。
    -   若要部署的 SSIS 目录中驻留的项目，选择**Integration Services 目录**，，然后输入服务器名称和路径的目录中的项目。
    单击“下一步”  以查看“选择目标”  页。
  
3.  上**选择目标**页上，选择项目的目标。
    -   输入完全限定的服务器名称。 如果目标服务器，Azure SQL 数据库服务器的名称所采用此格式： `<server_name>.database.windows.net`。
    -   然后单击**浏览**在 SSISDB 中选择目标文件夹。
    单击**下一步**以打开**评审**页。  
  
4.  上**查看**页上，查看所选的设置。
    -   可以通过单击 **“上一步”**或单击左窗格中的任意步骤来更改所做的选择。
    -   单击“部署”  以启动部署过程。
  
5.  在部署过程完成后**结果**页将打开。 该页显示每个操作是成功了还是失败了。
    -   如果操作失败，请单击**失败**中**结果**列以显示的错误说明。
    -   （可选） 单击**保存报表...**将结果保存到 XML 文件。
    -   单击**关闭**以退出向导。

## <a name="next-steps"></a>后续步骤
- 考虑使用其他方法来部署的包。
    - [部署 SSIS 包使用 TRANSACT-SQL (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
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

