---
title: "将 MySQL 数据迁移到 SQL Server 的 Azure SQL DB (MySQLToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Data Migration, server side data migration
- Data Migration,client side data migration
ms.assetid: a6a7f4d6-68aa-4a38-93bf-53eba0d7dc82
caps.latest.revision: "24"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0887825cf16986b78cad5d1889a04d73dacf222a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="migrating-mysql-data-into-sql-server---azure-sql-db-mysqltosql"></a>将 MySQL 数据迁移到 SQL Server 的 Azure SQL DB (MySQLToSQL)
已成功同步与已转换的对象后[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，你可以将数据从迁移到的 MySQL[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
> [!IMPORTANT]  
> 如果正在使用的引擎是服务器端数据迁移引擎，然后，在迁移之前，数据，你必须安装 SSMA 适用于 MySQL 扩展包和运行 SSMA 的计算机上的 MySQL 提供程序。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]也必须运行代理服务。 有关如何安装扩展包的详细信息，请参阅[安装 SQL Server (MySQL to SQL) 上的 SSMA 组件](http://msdn.microsoft.com/en-us/6772d0c5-258f-4d7b-afb0-b5f810e71af1)  
  
## <a name="setting-migration-options"></a>设置迁移选项  
在迁移之前，数据到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，查看中的项目迁移选项**项目设置**对话框。  
  
-   通过使用此对话框可以设置迁移批大小、 表锁定、 约束检查、 null 值处理和标识值处理等选项。 有关项目迁移设置的详细信息，请参阅[项目设置 （迁移）](http://msdn.microsoft.com/en-us/2a3cba9e-cd54-4a8b-b858-8fc4cf2580d9)。  
  
    有关详细信息**扩展数据迁移设置**，请参阅[数据迁移设置](http://msdn.microsoft.com/en-us/9c396df4-5676-4f32-9c57-70d4f15f9b7a)  
  
-   **迁移引擎**中**项目设置**对话框中，允许用户执行迁移过程使用两种类型的数据迁移引擎：  
  
    1.  客户端数据迁移引擎  
  
    2.  服务器端数据迁移引擎  
  
**客户端将数据迁移：**  
  
-   若要启动客户端上的数据迁移，选择**客户端数据迁移引擎**选项**项目设置**对话框。  
  
-   在**项目设置**、**客户端数据迁移引擎**设置选项。  
  
    > [!NOTE]  
    > **客户端数据迁移引擎**驻留在 SSMA 应用程序内和，因此是不依赖于扩展包的可用性。  
  
**服务器端数据迁移：**  
  
-   服务器端数据在迁移期间，引擎驻留在目标数据库。 通过扩展包安装它。 有关如何安装扩展包的详细信息，请参阅[安装 SQL Server (MySQL to SQL) 上的 SSMA 组件](http://msdn.microsoft.com/en-us/6772d0c5-258f-4d7b-afb0-b5f810e71af1)  
  
-   若要启动的服务器端上的迁移，选择**服务器端数据迁移引擎**选项**项目设置**对话框。  
  
> [!IMPORTANT]  
> **客户端数据迁移**选项才适用于 SQL Azure。  
  
## <a name="migrating-data-to-sql-server-or-sql-azure"></a>将数据迁移到 SQL Server 或 SQL Azure  
迁移数据是一大容量加载操作，将数据的行移到的 MySQL 表从[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或多个在事务中的 SQL Azure 表。 载入的行数[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]在每个事务在项目设置中配置。  
  
若要查看迁移消息，请确保输出窗格是可见。 否则为从**视图**菜单上，选择**输出**。  
  
**若要将数据迁移**  
  
1.  检查下列各项：  
  
    -   正在运行 SSMA 计算机上安装 MySQL 提供程序。  
  
    -   你已与目标数据库同步已转换的对象 (SQL Server / SQL Azure)。  
  
2.  在 MySQL 元数据资源管理器，选择包含你想要迁移的数据的对象：  
  
    -   若要迁移的所有架构的数据，请旁边选中的复选框**架构**。  
  
    -   若要将数据迁移或省略各个表，首先展开架构，展开**表**，然后选择或清除的表旁边的复选框。  
  
3.  若要将数据迁移，两种情况下出现：  
  
    **客户端将数据迁移：**  
  
    -   用于执行**客户机端数据迁移**，选择**客户端数据迁移引擎**选项**项目设置**对话框。  
  
    **服务器端数据迁移：**  
  
    -   在服务器端执行数据迁移，请确保：  
  
        1.  SSMA for MySQL 扩展包的 SQL Server 实例上安装。  
  
        2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]代理服务正在 SQL Server 实例上运行  
  
    -   用于执行**服务器端数据迁移**，选择**服务器端数据迁移引擎**选项**项目设置**对话框。  
  
4.  右键单击**架构**在 MySQL 元数据资源管理器，然后单击**迁移数据**。 此外可以将迁移为单个对象或对象的类别的数据： 右键单击该对象或其父文件夹;选择**迁移数据**选项。  
  
    > [!NOTE]  
    > 如果 SQL Server 实例上不安装 MySQL 扩展包的 SSMA 并且**服务器端数据迁移引擎**选中，那么在将数据迁移到目标数据库，遇到以下错误: SSMA 数据迁移组件上未找到 SQL Server，将无法进行服务器端数据迁移。 请检查是否正确安装了扩展包。 单击**取消**终止数据迁移。  
  
5.  在**连接到 MySQL**对话框中，输入连接凭据，，然后单击**连接**。 连接到 MySQL 的详细信息，请参阅[连接到 MySQL &#40;MySQLToSQL &#41;](../../ssma/mysql/connect-to-mysql-mysqltosql.md)  
  
    如果目标数据库是 SQL Server，然后，输入中的连接凭据**连接到 SQL Server**对话框中，单击**连接**。 连接到 SQL Server 的详细信息，请参阅[连接到 SQL Server](http://msdn.microsoft.com/en-us/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)  
  
    如果目标数据库是 SQL Azure，然后输入中的连接凭据**连接到 SQL Azure**对话框中，单击**连接**。 连接到 SQL Azure 的详细信息，请参阅[连接到 Azure SQL DB &#40;MySQLToSQL &#41;](../../ssma/mysql/connect-to-azure-sql-db-mysqltosql.md)  
  
    消息将出现在**输出**窗格。 在迁移完成后，**数据迁移报告**显示。 如果任何数据未迁移，单击包含错误的行，然后单击**详细信息**。 在完成与报表，请单击**关闭**。 有关数据迁移报表的详细信息，请参阅[（SSMA 常见） 的数据迁移报告](http://msdn.microsoft.com/en-us/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> 当为目标数据库使用 SQL Express edition 时，允许仅限客户端数据迁移，并且不支持服务器端数据迁移。  
  
## <a name="see-also"></a>另请参阅  
[将 MySQL 数据库迁移到 SQL Server 的 Azure SQL DB &#40;MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
