---
title: "使用 SQL Server 数据使用 R |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 0a3d7ba0-4113-4cde-9645-debba45cae8f
caps.latest.revision: 20
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 6db9cc485778e4074b5b648b23572edee3a0f42e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/27/2017

---
# <a name="work-with-sql-server-data-using-r"></a>使用 SQL Server 数据使用 R

在本课中，将设置环境并添加训练模型所需的数据，以及运行数据的一些快速摘要。 作为过程的一部分，将完成以下任务：
  
- 创建一个新的数据库，用于存储两个 R 模型的培训和评分的数据。
  
- 在工作站与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机之间进行通信时，创建一个要使用的帐户（Windows 用户或 SQL 登录名）。
  
- 在 R 中创建数据源，用于处理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据和数据库对象。
  
- 使用 R 数据源将数据加载到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中。
  
- 使用 R 获取变量的列表并修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表的元数据。
  
- 创建计算上下文，以便启用远程执行 R 代码。
  
- 了解在远程计算上下文中启用跟踪的方法。
  
## <a name="create-the-database-and-user"></a>创建数据库和用户

对于此演练，将在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中创建新数据库，并添加 SQL 登录名，该登录名具有写入和读取数据以及运行 R 脚本的权限。

> [!NOTE]
> 如果你只读取数据，运行 R 脚本的帐户还要求只有一些特定的权限 (**db_datareader**角色) 上指定的数据库。 但是，在本教程中，将需要 DDL 管理员权限来准备数据库并创建用于保存评分结果的表。
> 
> 此外，如果您不是数据库所有者，你将需要的权限，执行任意外部脚本，若要能够执行 R 脚本。

1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，请选择启用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的实例，右键单击“数据库”，然后选择“新建数据库”。
  
2. 键入新数据库的名称。 可以使用任何想用的名称；但切记相应地在本演练中编辑所有的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本和 R 脚本。
  
    > [!TIP]
    > 若要查看已更新的数据库名称，右键单击“数据库”，然后选择“刷新”。
  
3. 单击“新建查询”，然后将数据库上下文更改为 master 数据库。
  
4. 在新的“查询”窗口中，运行以下命令以创建用户帐户并将其分配到本教程中使用的数据库。 如有需要，请务必更改数据库名称。
  
**Windows 用户**
  
```SQL
 -- Create server user based on Windows account
USE master
GO
CREATE LOGIN [<DOMAIN>\<user_name>] FROM WINDOWS WITH DEFAULT_DATABASE=[DeepDive]

 --Add the new user to tutorial database
USE [DeepDive]
GO
CREATE USER [<user_name>] FOR LOGIN [<DOMAIN>\<user_name>] WITH DEFAULT_SCHEMA=[db_datareader]
```

**SQL 登录名**

```SQL
-- Create new SQL login
USE master
GO
CREATE LOGIN DDUser01 WITH PASSWORD='<type password here>', CHECK_EXPIRATION=OFF, CHECK_POLICY=OFF;

-- Add the new SQL login to tutorial database
USE [DeepDive]
GO
CREATE USER [DDUser01] FOR LOGIN [DDUser01] WITH DEFAULT_SCHEMA=[db_datareader]
```

5. 若要验证是否已创建用户，选择新的数据库，依次展开“安全”和“用户”。

## <a name="troubleshooting"></a>故障排除

本部分列出在设置数据库的过程中可能遇到的一些常见问题。

- **如何验证数据库连接并检查 SQL 查询？**
  
    在使用服务器运行 R 代码之前，建议检查是否可以从 R 开发环境访问数据库。 [Visual Studio 中的服务器资源管理器](https://msdn.microsoft.com/library/x603htbk.aspx) 和 [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) 是具有强大的数据库连接和管理功能的免费工具。
  
    如果不想安装附加的数据库管理工具，可以在控制面板中使用 [ODBC 数据源管理器](https://msdn.microsoft.com/library/ms714024.aspx) 创建到 SQL Server 实例的测试连接。 如果该数据库配置正确，并输入了正确的用户名和密码，则应能看到刚刚创建的数据库，并能将其选为默认数据库。
  
    如果无法连接到数据库，请验证是否对服务器启用了远程连接以及是否已启用命名管道协议。 [本文](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx)还提供了其他疑难解答提示。
  
- **表名称具有 datareader 前缀，为什么？**
  
    当指定此用户的默认架构为 **db_datareader**时，所有的表和此用户创建的其他新对象将以架构作为前缀。 架构像是一个文件夹，可将其添加到数据库来组织对象。 架构还定义了数据库中用户的权限。
  
    当架构与一个特定的用户名相关联时，将用户称为架构所有者。 创建对象时，将始终在自己的架构中创建，除非明确要求在另一个架构中创建对象。
  
    例如，如果创建一个名为 TestData 的表，且默认架构为 **db_datareader**，则将创建名为 <database_name>.db_datareader.TestData 的表。
  
    出于此原因，数据库可以包含多个具有相同名称的表，前提是这些表属于不同的架构。
   
    寻找表时，如果未指定架构，则数据库服务器将查找你拥有的架构。 因此，访问与登录名关联的架构中的表时，无需指定架构名称。
  
- **我没有 DDL 权限。是否仍可以运行此教程？**
  
    是；但你应该请人将数据预加载到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表，并跳过需要创建新表的部分。 本教程概括介绍了需要 DDL 权限的功能。

    此外，要求管理员授予您权限，执行任意外部脚本。 是远程还是通过使用 R 的脚本执行，需要`sp_execute_external_script`。

## <a name="next-step"></a>下一步

[使用 RxSqlServerData 创建 SQL Server 数据对象](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)

## <a name="overview"></a>概述

[对数据科学的深入探讨：使用 RevoScaleR 包](../../advanced-analytics/tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)




