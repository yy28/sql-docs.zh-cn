---
title: "连接到 Azure 上的 SSISDB 目录数据库 |Microsoft 文档"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: lift-shift
ms.suite: sql
ms.custom: 
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 560965a241b24a09f50a23faf63ce74d0049d5a7
ms.openlocfilehash: ac121e600c3c616006d79892c50f796ca7cd6b3f
ms.contentlocale: zh-cn
ms.lasthandoff: 10/13/2017

---
# <a name="connect-to-the-ssisdb-catalog-database-on-azure"></a>连接到 Azure 上的 SSISDB 目录数据库

获取你需要连接到 Azure SQL 数据库服务器上承载 SSISDB 目录数据库的连接信息。 你需要要连接的以下项：
- 完全限定的服务器名称
- 数据库名称
- 登录信息 

## <a name="prerequisites"></a>先决条件
在开始之前，请确保您有 17.2 或更高版本的 SQL Server Management Studio 版本。 若要下载最新版本的 SSMS，请参阅[下载 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

## <a name="get-the-connection-info-from-the-azure-portal"></a>从 Azure 门户获取连接信息
1. 登录到 [Azure 门户](https://portal.azure.com/)。
2. 在 Azure 门户中，选择**SQL 数据库**从左侧菜单，然后选择`SSISDB`上的数据库**SQL 数据库**页。 
3. 上**概述**页面`SSISDB`数据库，请查看的完全限定的服务器名称，如以下图像中所示。 将鼠标悬停在服务器名称以打开**单击此项可复制**选项。

    ![服务器连接信息](media/ssis-azure-connect-to-catalog-database/server-name.png) 

4. 如果您忘记了 SQL 数据库服务器的登录信息后，导航到 SQL 数据库服务器页。 您可以在其中查看服务器管理员命名，然后如有必要，重置密码。

## <a name="connect-with-ssms"></a>使用 SSMS 连接
1. 打开 SQL Server Management Studio。

2. **连接到服务器**。 在**连接到服务器**对话框框中，输入以下信息：

   | 设置       | 建议的值 | Description | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **服务器类型** | 数据库引擎 | 此值是必需的。 |
   | **服务器名称** | 完全限定的服务器名称 | 名称应为按以下格式： **mysqldbserver.database.windows.net**。 |
   | **身份验证** | SQL Server 身份验证 | 此快速开始使用 SQL 身份验证。 |
   | **登录** | 与服务器管理员帐户 | 这是你在创建服务器时指定的帐户。 |
   | **密码** | 你的服务器管理员帐户的密码 | 这是你在创建服务器时指定的密码。 |

3. **连接到 SSISDB 数据库**。 选择**选项**以展开**连接到服务器**对话框。 在展开**连接到服务器**对话框中，选择**连接属性**选项卡。在**连接到数据库**字段中，选择或输入`SSISDB`。

    > [!IMPORTANT]
    > 如果你未选中`SSISDB`连接时，你可能看不到对象资源管理器中的 SSIS 目录。

4. 然后选择**连接**。

5. 在对象资源管理器，展开**Integration Services 目录**然后展开**SSISDB** SSIS 目录数据库中查看的对象。

## <a name="next-steps"></a>后续步骤
- 部署包。 有关详细信息，请参阅[部署的 SSIS 项目与 SQL Server Management Studio (SSMS)](../ssis-quickstart-deploy-ssms.md)。
- 运行的包。 有关详细信息，请参阅[运行 SSIS 包与 SQL Server Management Studio (SSMS)](../ssis-quickstart-run-ssms.md)。
- 计划包。 有关详细信息，请参阅[计划 SSIS 包在 Azure 上的执行](ssis-azure-schedule-packages.md)

