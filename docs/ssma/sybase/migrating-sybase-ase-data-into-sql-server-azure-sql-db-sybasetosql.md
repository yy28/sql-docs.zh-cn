---
title: "将 Sybase ASE 数据迁移到 SQL Server 的 Azure SQL DB |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
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
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2e30171c86c56f232d17ed159eb53d0eaddae79c
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="migrating-sybase-ase-data-into-sql-server---azure-sql-db--sybasetosql"></a>将 Sybase ASE 数据迁移到 SQL Server 的 Azure SQL DB (SybaseToSQL)
你已成功加载到 Sybase 自适应 Server Enterprise (ASE) 数据库对象后[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB，你可以将数据从迁移到的 ASE[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。  
  
> [!IMPORTANT]  
> 如果正在使用的引擎是服务器端数据迁移引擎，则在迁移数据之前必须安装 SSMA Sybase ASE 扩展包和运行 SSMA 的计算机上的 Sybase ASE 提供程序。 也必须运行 SQL Server 代理服务。 有关如何安装扩展包的详细信息，请参阅[安装 SQL Server (SybaseToSQL) 上的 SSMA 组件](http://msdn.microsoft.com/en-us/5ad9e12c-2cdb-4dd2-8703-05a23242d19d)  
  
## <a name="setting-migration-options"></a>设置迁移选项  
在迁移之前，数据插入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB，查看中的项目迁移选项**项目设置**对话框。  
  
-   通过使用此对话框可以设置迁移批大小、 表锁定、 约束检查、 null 值处理和标识值处理等选项。 有关项目迁移设置的详细信息，请参阅[项目设置 （迁移） (Sybase)](http://msdn.microsoft.com/en-us/82f8857f-7ab1-4738-ab6e-b1e95ea94924)。  
  
    有关详细信息**扩展数据迁移设置**，请参阅[数据迁移设置](http://msdn.microsoft.com/en-us/94d7a083-2dbc-4e3d-94dd-92b7ff9d0c2d)  
  
-   **迁移引擎**中**项目设置**对话框中，允许用户执行迁移过程使用两种类型的数据迁移引擎 viz。:  
  
    1.  客户端数据迁移引擎  
  
    2.  服务器端数据迁移引擎  
  
**客户端将数据迁移：**  
  
-   要启动客户端上的数据迁移，请选择选项**客户端数据迁移引擎**中**项目设置**对话框。  
  
-   在**项目设置**、**客户端数据迁移引擎**默认情况下设置选项。  
  
    > [!NOTE]  
    > 客户端数据迁移引擎驻留在 SSMA 应用程序内，因此，不依赖于扩展包的可用性。  
  
**服务器端数据迁移：**  
  
-   服务器端数据在迁移期间，引擎驻留在目标数据库。 通过扩展包安装它。 有关如何安装扩展包的详细信息，请参阅[安装 SQL Server (SybaseToSQL) 上的 SSMA 组件](http://msdn.microsoft.com/en-us/5ad9e12c-2cdb-4dd2-8703-05a23242d19d)  
  
-   若要启动的服务器端上的迁移，选择**服务器端数据迁移引擎**选项**项目设置**对话框。  
  
> [!NOTE]  
> Azure SQL DB 用作目标数据库，仅**客户机端数据迁移**允许和不支持服务器端数据迁移。  
  
## <a name="migrating-data-to-sql-server-or-azure-sql-db"></a>将数据迁移到 SQL Server 或 Azure SQL 数据库  
迁移数据是将数据的行从 ASE 表移到在事务中的 SQL Server 表大容量加载操作。 加载到 SQL Server 或 Azure SQL DB 在各事务中的行数是在项目设置中配置的。  
  
若要查看迁移消息，请确保输出窗格是可见。 否则，请选择**输出**从**视图**菜单。  
  
**若要将数据迁移**  
  
1.  检查下列各项：  
  
    -   ASE 提供程序安装在运行 SSMA 的计算机上。  
  
    -   你已与目标数据库 （SQL Server 或 Azure SQL DB） 同步已转换的对象。  
  
2.  在 Sybase 元数据资源管理器，选择包含你想要迁移的数据的对象：  
  
    -   若要迁移的所有架构的数据，请旁边选中的复选框**架构**。  
  
    -   若要将数据迁移或省略各个表，首先展开架构，展开**表**，然后选择或清除的表旁边的复选框。  
  
3.  若要将数据迁移，两种情况下出现：  
  
    **客户端将数据迁移：**  
  
    用于执行**客户机端数据迁移**，选择**客户端数据迁移引擎**选项**项目设置**对话框。  
  
    **服务器端数据迁移：**  
  
    -   在执行服务器端数据迁移，请确保：  
  
        1.  SSMA for Sybase 扩展包的 SQL Server 实例上安装。  
  
        2.  SQL server 实例上运行的 SQL Server 代理服务  
  
    -   用于执行**服务器端数据迁移**，选择**服务器端数据迁移引擎**选项**项目设置**对话框。  
  
4.  右键单击**架构**在 Sybase 元数据资源管理器，然后单击**迁移数据**。 此外可以将迁移为单个对象或对象的类别的数据： 右键单击对象或其父文件夹，然后选择**迁移数据**选项。  
  
    > [!NOTE]  
    > 如果 SQL Server 实例上未安装 SSMA for Sybase 扩展包并且**服务器端数据迁移引擎**选中，那么在将数据迁移到目标数据库，遇到以下错误: SSMA 数据迁移组件上未找到 SQL Server，将无法进行服务器端数据迁移。 请检查是否正确安装了扩展包。 单击**取消**终止数据迁移。  
  
5.  在**连接到 Sybase ASE**对话框中，输入连接凭据，，然后单击**连接**。 连接到 Sybase ASE 的详细信息，请参阅[连接到 Sybase &#40;SybaseToSQL &#41;](../../ssma/sybase/connect-to-sybase-sybasetosql.md)  
  
    如果目标数据库是 SQL Server，然后，输入中的连接凭据**连接到 SQL Server**对话框中，单击**连接**。 连接到 SQL Server 的详细信息，请参阅[连接到 SQL Server(SybaseToSQL)](http://msdn.microsoft.com/en-us/dd368a1a-45b0-40e9-b4d3-5cdb48c26606)  
  
    如果目标数据库是 Azure SQL DB，然后输入中的连接凭据**连接到 Azure SQL DB**对话框中，单击**连接**。 连接到 Azure SQL DB 的详细信息，请参阅[连接到 Azure SQL DB &#40;SybaseToSQL &#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)  
  
    消息将出现在**输出**窗格。 在迁移完成后，**数据迁移报告**显示。 如果任何数据未迁移，单击包含错误的行，然后单击**详细信息**。 在完成与报表，请单击**关闭**。 有关数据迁移报表的详细信息，请参阅[（SSMA 常见） 的数据迁移报告](http://msdn.microsoft.com/en-us/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> 当为目标数据库使用 SQL Express edition 时，允许仅限客户端数据迁移，并且不支持服务器端数据迁移。  
  
## <a name="see-also"></a>另請參閱  
[Sybase ASE 将数据库迁移到 SQL Server 的 Azure SQL DB &#40;SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

