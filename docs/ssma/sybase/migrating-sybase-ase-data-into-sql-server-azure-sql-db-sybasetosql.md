---
title: 将 Sybase ASE 数据迁移到 SQL Server-Azure SQL 数据库 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Migrating data,Client Side Data Migration
- Migrating data,Server Side Data Migration
ms.assetid: 54a39f5e-9250-4387-a3ae-eae47c799811
caps.latest.revision: 15
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: e39d74143e21d6b75a5a35a1f8dbde4f62f285f4
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "40395664"
---
# <a name="migrating-sybase-ase-data-into-sql-server---azure-sql-db--sybasetosql"></a>Sybase ASE 数据迁移到 SQL Server-Azure SQL DB (SybaseToSQL)
已成功加载到 Sybase Adaptive Server Enterprise (ASE) 数据库对象后[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 中，您可以将数据从迁移到 ASE[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。  
  
> [!IMPORTANT]  
> 如果正在使用的引擎是服务器端数据迁移引擎，则在迁移数据之前必须安装 SSMA Sybase ASE 的扩展包，和运行 SSMA 的计算机上的 Sybase ASE 提供程序。 此外必须运行 SQL Server 代理服务。 有关如何安装扩展包的详细信息，请参阅[SQL Server (SybaseToSQL) 上安装 SSMA 组件](http://msdn.microsoft.com/5ad9e12c-2cdb-4dd2-8703-05a23242d19d)  
  
## <a name="setting-migration-options"></a>设置迁移选项  
在迁移之前，数据读入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB，查看中的项目迁移选项**项目设置**对话框。  
  
-   通过使用此对话框可以设置选项，如迁移批大小、 表锁定、 约束检查，null 值处理和标识值处理。 有关项目迁移设置的详细信息，请参阅[项目设置 （迁移） (Sybase)](http://msdn.microsoft.com/82f8857f-7ab1-4738-ab6e-b1e95ea94924)。  
  
    有关详细信息**扩展数据迁移设置**，请参阅[数据迁移设置](data-migration-settings-sybasetosql.md)  
  
-   **迁移引擎**中**项目设置**对话框，允许用户执行迁移过程使用两种类型的数据迁移引擎报道。:  
  
    1.  客户端数据迁移引擎  
  
    2.  服务器端数据迁移引擎  
  
**客户端将数据迁移：**  
  
-   若要启动客户端上的数据迁移，选择选项**客户端数据迁移引擎**中**项目设置**对话框。  
  
-   在中**项目设置**，则**客户端数据迁移引擎**默认情况下设置选项。  
  
    > [!NOTE]  
    > 客户端的数据迁移引擎驻留在 SSMA 应用程序内，因此，不依赖于扩展包的可用性。  
  
**服务器端数据迁移：**  
  
-   服务器端数据在迁移期间，该引擎驻留在目标数据库上。 它通过扩展包安装。 有关如何安装扩展包的详细信息，请参阅[SQL Server (SybaseToSQL) 上安装 SSMA 组件](http://msdn.microsoft.com/5ad9e12c-2cdb-4dd2-8703-05a23242d19d)  
  
-   若要启动的服务器端上的迁移，选择**服务器端数据迁移引擎**选项**项目设置**对话框。  
  
> [!NOTE]  
> Azure SQL DB 用作目标数据库，仅**客户端数据迁移**允许和不支持服务器端数据迁移。  
  
## <a name="migrating-data-to-sql-server-or-azure-sql-db"></a>将数据迁移到 SQL Server 或 Azure SQL DB  
迁移数据是大容量加载操作，将数据行从 ASE 表移到 SQL Server 表中的事务。 在项目设置中配置加载到 SQL Server 或 Azure SQL DB 中的每个事务的行数。  
  
若要查看迁移消息，请确保输出窗格可见。 否则，请选择**输出**从**视图**菜单。  
  
**若要将数据迁移**  
  
1.  检查下列各项：  
  
    -   ASE 提供程序安装在正在运行的 SSMA 的计算机上。  
  
    -   你已与目标数据库 （SQL Server 或 Azure SQL 数据库） 同步已转换的对象。  
  
2.  Sybase 元数据资源管理器中选择包含你想要迁移的数据的对象：  
  
    -   若要迁移的所有架构的数据，选择复选框旁边**架构**。  
  
    -   若要将数据迁移或忽略各个表，首先展开架构，展开**表**，然后选中或清除表旁边的复选框。  
  
3.  若要将数据迁移，两种情况下出现：  
  
    **客户端将数据迁移：**  
  
    用于执行**客户端数据迁移**，选择**客户端数据迁移引擎**选项**项目设置**对话框。  
  
    **服务器端数据迁移：**  
  
    -   之前执行服务器端数据迁移，请确保：  
  
        1.  SQL Server 实例上安装 SSMA for Sybase 的扩展包。  
  
        2.  SQL Server 实例上运行的 SQL Server 代理服务  
  
    -   用于执行**服务器端数据迁移**，选择**服务器端数据迁移引擎**选项**项目设置**对话框。  
  
4.  右键单击**架构**在 Sybase 元数据资源管理器，然后单击**迁移数据**。 此外可以将迁移为单个对象或类别的对象的数据： 右键单击该对象或其父文件夹，然后选择**迁移数据**选项。  
  
    > [!NOTE]  
    > 如果 SQL Server 实例上未安装 SSMA for Sybase 的扩展包，并且如果**服务器端数据迁移引擎**选中，那么在将数据迁移到目标数据库，时遇到以下错误: SSMASQL Server 上找不到数据的迁移组件，无法在服务器端数据迁移。 请检查是否正确安装的扩展包。 单击**取消**终止数据迁移。  
  
5.  在中**连接到 Sybase ASE**对话框中，输入连接凭据，然后单击**Connect**。 连接到 Sybase ASE 的详细信息，请参阅[连接到 Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/connect-to-sybase-sybasetosql.md)  
  
    如果目标数据库为 SQL Server，然后，输入中的连接凭据**连接到 SQL Server**对话框中，单击**Connect**。 连接到 SQL Server 的详细信息，请参阅[连接到 SQL Server(SybaseToSQL)](http://msdn.microsoft.com/dd368a1a-45b0-40e9-b4d3-5cdb48c26606)  
  
    如果目标数据库为 Azure SQL DB，然后输入中的连接凭据**连接到 Azure SQL DB**对话框中，单击**Connect**。 连接到 Azure SQL DB 的详细信息，请参阅[连接到 Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)  
  
    消息将出现在**输出**窗格。 在迁移完成后，**数据迁移报表**出现。 如果未迁移的任何数据，单击包含错误的行，然后单击**详细信息**。 与报表一起完成后，单击**关闭**。 数据迁移报表的详细信息，请参阅[数据迁移报表 （SSMA 常见）](http://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> 如果 SQL Express 版本用作目标数据库，则允许仅限客户端数据迁移，并且不支持服务器端数据迁移。  
  
## <a name="see-also"></a>请参阅  
[将 Sybase ASE 数据库迁移到 SQL Server-Azure SQL 数据库&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
