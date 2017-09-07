---
title: "将 MySQL 数据库映射到 SQL Server 架构 (MySQLToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
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
- Mapping, Modifying target database and schema
- Mapping, reverting to default database and schema
ms.assetid: 5c6fb445-92ae-4933-b77d-80230931c024
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6f6472656dbfd31ca64348d066cca19f303b4a5f
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="mapping-mysql-databases-to-sql-server-schemas-mysqltosql"></a>将 MySQL 数据库映射到 SQL Server 架构 (MySQLToSQL)
默认情况下，SSMA for MySQL 将迁移到 MySQL 架构中的所有对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或架构名为的 SQL Azure 数据库。 但是，你可以自定义 MySQL 架构之间的映射和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 数据库。  
  
## <a name="mysql-and-sql-server-or-sql-azure-schemas"></a>MySQL 和 SQL Server 或 SQL Azure 架构  
架构的 MySQL 概念将映射到数据库以及其架构之一的 SQL Server 概念。 SSMA 是指数据库和架构的 SQL Server 组合为一个架构。  
  
架构的 MySQL 概念将映射到数据库以及其架构之一的 SQL Server 概念。 例如，MySQL 可能具有名为的架构**HR**。 SQL server 实例可能具有一个名为数据库**HR**，并且该数据库中的架构。 一个架构**dbo** （或数据库所有者） 架构。 默认情况下，MySQL 架构**HR**将映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库和架构**HR.dbo**。 SSMA 是指[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库和架构的组合为一个架构。  
  
你可以修改 MySQL 之间的映射和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure 的架构。  
  
## <a name="modifying-the-target-database-and-schema"></a>修改目标数据库和架构  
在 SSMA，可以将 MySQL 架构映射到任何可用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 架构。  
  
**若要修改的数据库和架构**  
  
1.  在 MySQL 元数据资源管理器中，选择**架构**。  
  
    **架构映射**时选择单个架构，可能也是可用选项卡。 中的列表**架构映射**选项卡上自定义的所选对象。  
  
2.  在右窗格中，单击**架构映射**选项卡。  
  
    你将看到的所有 MySQL 架构，跟目标值的列表。 此目标中，表示在由两部分表示法 (*database.schema*) 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或对象和数据将迁移的 SQL Azure。  
  
3.  选择包含你想要更改，然后单击的映射的行**修改**。  
  
    在**选择目标架构**对话框中，你可以浏览可用的目标数据库和架构或类型的数据库和架构中由两部分表示法 (database.schema) 的文本框的名称，然后单击**确定**。  
  
4.  目标上的更改**架构映射**选项卡。  
  
**映射模式**  
  
-   将映射到 SQL Server  
  
可以将源数据库映射到任何目标数据库。 默认情况下映射源数据库到目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]具有与其连接使用 SSMA 数据库。 要映射的目标数据库是否不存在上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，则系统将提示你使用的消息**"目标中不存在的数据库和/或架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据。它会在同步期间创建。是否要继续？"** 单击是。 同样，可以架构映射到在目标下不存在架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库将在同步期间创建的。  
  
-   将映射到 SQL Azure  
  
你可以将源数据库映射到已连接的目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库或到连接的目标中的任何架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库。 如果将源架构映射到已连接的目标数据库在任何非现有架构，则系统将提示您提供一条消息**"架构中不存在目标元数据。它会在同步期间创建。你想要继续吗？"**单击是。  
  
## <a name="reverting-to-the-default-database-and-schema"></a>还原为默认数据库和架构  
如果你自定义 MySQL 架构和 SQL Server 架构之间的映射，你可以还原回默认值的映射。  
  
**若要还原到的默认数据库和架构**  
  
1.  在架构映射的选项卡上，选择任何行，然后单击**重置为默认**若要还原到的默认数据库和架构。  
  
## <a name="next-steps"></a>后续步骤  
如果你想要分析的 MySQL 对象转换为 SQL Server 或 SQL Azure 的对象，则可以[创建转换报表](http://msdn.microsoft.com/en-us/2a56a003-3b0f-453a-963c-00c9e40933ec)否则可以[转换的 MySQL 数据库对象定义](http://msdn.microsoft.com/en-us/ac21850b-fb32-4704-9985-5759b7c688c7)到 SQL Server 或 SQL Azure 的架构  
  
## <a name="see-also"></a>另请参阅  
[项目设置 &#40;转换 &#41;&#40;MySQLToSQL &#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
[连接到 Azure SQL DB &#40;MySQLToSQL &#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
[将 MySQL 数据库迁移到 SQL Server 的 Azure SQL DB &#40;MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[连接到 SQL Server &#40;MySQLToSQL &#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  

