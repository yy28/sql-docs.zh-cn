---
title: 对于 RevoScaleR 教程-SQL Server 机器学习中创建一个数据库和权限
description: 如何为 R 教程创建的 SQL Server 数据库的教程演练...
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 2ed5d6e7ef3b0d6e8ac5ebaa3533c6bebce5e856
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62641096"
---
# <a name="create-a-database-and-permissions-sql-server-and-revoscaler-tutorial"></a>创建一个数据库和权限 （SQL Server 和 RevoScaleR 教程）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本课程中属于[RevoScaleR 教程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)如何使用[RevoScaleR 函数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)与 SQL Server。

有关如何设置 SQL Server 数据库和权限所需完成本教程是第一课。 使用[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)或另一个查询编辑器来完成以下任务：

> [!div class="checklist"]
> * 创建一个新的数据库来存储的数据训练和评分两个 R 模型
> * 创建具有用于创建和使用数据库对象权限的数据库用户登录
  
## <a name="create-the-database"></a>创建数据库

本教程需要一个数据库用于存储数据和代码。 如果你不是管理员，要求数据库管理员为你创建的数据库和登录名。 您将需要权限来写入和读取数据，并运行 R 脚本。

1. 在 SQL Server Management Studio，连接到启用了 R 的数据库实例。

2. 右键单击**数据库**，然后选择**新数据库**。
  
2. 键入新数据库的名称：RevoDeepDive。
  

## <a name="create-a-login"></a>创建登录名
  
1. 单击“新建查询”  ，然后将数据库上下文更改为 master 数据库。
  
2. 在新的“查询”  窗口中，运行以下命令以创建用户帐户并将其分配到本教程中使用的数据库。 如有需要，请务必更改数据库名称。

3. 若要验证该登录名，请选择新的数据库，展开**安全**，然后展开**用户**。
  
**Windows 用户**
  
```sql
 -- Create server user based on Windows account
USE master
GO
CREATE LOGIN [<DOMAIN>\<user_name>] FROM WINDOWS WITH DEFAULT_DATABASE=[RevoDeepDive]

 --Add the new user to tutorial database
USE [RevoDeepDive]
GO
CREATE USER [<user_name>] FOR LOGIN [<DOMAIN>\<user_name>] WITH DEFAULT_SCHEMA=[db_datareader]
```

**SQL 登录名**

```sql
-- Create new SQL login
USE master
GO
CREATE LOGIN [DDUser01] WITH PASSWORD='<type password here>', CHECK_EXPIRATION=OFF, CHECK_POLICY=OFF;

-- Add the new SQL login to tutorial database
USE RevoDeepDive
GO
CREATE USER [DDUser01] FOR LOGIN [DDUser01] WITH DEFAULT_SCHEMA=[db_datareader]
```

## <a name="assign-permissions"></a>分配权限

本教程演示 R 脚本和 DDL 操作，包括创建和删除表和存储的过程，以及 SQL Server 上在外部进程中运行 R 脚本。 在此步骤中，将分配权限以允许这些任务。

此示例假定 SQL 登录名 (DDUser01)，但如果您创建了 Windows 登录名，使用该副本。

```sql
USE RevoDeepDive
GO

EXEC sp_addrolemember 'db_owner', 'DDUser01'
GRANT EXECUTE ANY EXTERNAL SCRIPT TO DDUser01
GO
```

## <a name="troubleshoot-connections"></a>排查连接问题

本部分列出在设置数据库的过程中可能遇到的一些常见问题。

- **如何验证数据库连接并检查 SQL 查询？**
  
    在使用服务器运行 R 代码之前，建议检查是否可以从 R 开发环境访问数据库。 [Visual Studio 中的服务器资源管理器](https://docs.microsoft.com/previous-versions/x603htbk(v=vs.140)) 和 [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) 是具有强大的数据库连接和管理功能的免费工具。
  
    如果不想安装附加的数据库管理工具，可以在控制面板中使用 [ODBC 数据源管理器](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator?view=sql-server-2017) 创建到 SQL Server 实例的测试连接。 如果该数据库配置正确，并输入了正确的用户名和密码，则应能看到刚刚创建的数据库，并能将其选为默认数据库。
  
    连接失败的常见原因包括远程服务器上，不启用连接且未启用命名管道协议。 在本文中，可以找到更多疑难解答提示：[解决 SQL Server 数据库引擎的连接问题](https://docs.microsoft.com/sql/database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine)。
  
- **表名称具有 datareader 前缀，为什么？**
  
    当指定为此用户的默认架构**db_datareader**，所有表和此用户创建的其他新对象都带有前缀*架构*名称。 架构像是一个文件夹，可将其添加到数据库来组织对象。 架构还定义了数据库中用户的权限。
  
    其中一个特定的用户名称相关联的架构时，该用户是_架构所有者_。 创建对象时，将始终在自己的架构中创建，除非明确要求在另一个架构中创建对象。
  
    例如，如果使用名称创建一个表**TestData**，且默认架构**db_datareader**，使用以下名称创建表`<database_name>.db_datareader.TestData`。
  
    出于此原因，数据库可以包含多个具有相同名称的表，前提是这些表属于不同的架构。
   
    如果你寻找表时，未指定架构，数据库服务器查找你拥有的架构。 因此，访问与登录名关联的架构中的表时，无需指定架构名称。
  
- **我没有 DDL 权限。是否仍可以运行此教程？**
  
    是的但你应该请人预加载到数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表，并跳到下一课中继续操作。 需要 DDL 权限的函数被调用本教程中，只要有可能。

    此外，让管理员授予的权限 EXECUTE ANY EXTERNAL SCRIPT。 是否远程中或通过使用执行 R 脚本，需要`sp_execute_external_script`。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [使用 RxSqlServerData 创建 SQL Server 数据对象](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)