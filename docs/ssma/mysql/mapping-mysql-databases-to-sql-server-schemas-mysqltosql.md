---
title: 将 MySQL 数据库映射到 SQL Server 架构 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Mapping, Modifying target database and schema
- Mapping, reverting to default database and schema
ms.assetid: 5c6fb445-92ae-4933-b77d-80230931c024
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 215833c96fae02ae7877e00173fb5a920a47ee0c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67908981"
---
# <a name="mapping-mysql-databases-to-sql-server-schemas-mysqltosql"></a>将 MySQL 数据库映射到 SQL Server 架构 (MySQLToSQL)
默认情况下，适用于 MySQL 的 SSMA 将迁移到 MySQL 架构中的所有对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或架构名为 SQL Azure 数据库。 但是，自定义 MySQL 架构之间的映射和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 数据库。  
  
## <a name="mysql-and-sql-server-or-sql-azure-schemas"></a>MySQL 和 SQL Server 或 SQL Azure 架构  
MySQL 架构概念的将映射到 SQL Server 数据库和其架构中的一个概念。 SSMA 是指数据库和架构的 SQL Server 组合为一个架构。  
  
MySQL 架构概念的将映射到 SQL Server 数据库和其架构中的一个概念。 例如，MySQL 可能具有名为的架构**HR**。 SQL Server 的实例可能拥有一个名为数据库**HR**，并在该数据库是架构。 一个架构**dbo** （或数据库所有者） 架构。 默认情况下，MySQL 架构**HR**将映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库和架构**HR.dbo**。 SSMA 是指[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]架构数据库和架构的组合。  
  
您可以修改 MySQL 之间的映射和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure 的架构。  
  
## <a name="modifying-the-target-database-and-schema"></a>修改目标数据库和架构  
在 SSMA 中，可以将 MySQL 架构映射到任何可用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 架构。  
  
**若要修改的数据库和架构**  
  
1.  在 MySQL 的元数据资源管理器中，选择**架构**。  
  
    **架构映射**时选择的单个架构，可能也是可用选项卡。 中的列表**架构映射**所选对象的自定义选项卡。  
  
2.  在右窗格中，单击**架构映射**选项卡。  
  
    您将看到所有 MySQL 架构后, 跟一个目标值的列表。 此目标中的两个部分表示法表示 (*database.schema*) 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 对象和数据都迁移。  
  
3.  选择包含你想要更改，然后单击的映射的行**修改**。  
  
    在**选择目标架构**对话框，可以浏览可用的目标数据库和架构或类型的数据库和架构两个部件表示法 (database.schema) 的文本框中的名称，然后单击**确定**.  
  
4.  在目标上的更改**架构映射**选项卡。  
  
**模式的映射**  
  
-   映射到 SQL Server  
  
您可以将源数据库映射到任何目标数据库。 默认情况下映射源数据库与目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]与之有连接使用 SSMA 数据库。 是否要映射的目标数据库上不存在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，然后将会有一条消息提示 **"目标中不存在的数据库和/或架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元数据。在同步过程中将创建它。是否想要继续？"** 单击是。 同样，您可以映射到目标下不存在架构的架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将在同步过程中创建的数据库。  
  
-   映射到 SQL Azure  
  
您可以将源数据库映射到连接目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库或连接的目标中的任何架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。 如果将源架构映射到已连接的目标数据库下的任何不存在架构，则将会有一条消息提示 **"架构中不存在目标元数据。在同步过程中将创建它。你想要继续吗？"** 单击是。  
  
## <a name="reverting-to-the-default-database-and-schema"></a>还原为默认数据库和架构  
如果自定义 MySQL 架构和 SQL Server 架构之间的映射，可以还原为默认值的映射。  
  
**若要恢复为默认数据库和架构**  
  
1.  在架构映射选项卡下选择任何行，然后单击**重置为默认值**还原为默认数据库和架构。  
  
## <a name="next-steps"></a>后续步骤  
如果你想要分析的 MySQL 对象转换为 SQL Server 或 SQL Azure 对象，则可以[创建转换报告](assessing-mysql-databases-for-conversion-mysqltosql.md)否则可以[转换的 MySQL 数据库对象定义](converting-mysql-databases-mysqltosql.md)到 SQLServer 或 SQL Azure 架构  
  
## <a name="see-also"></a>请参阅  
[项目设置&#40;转换&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
[连接到 Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
[迁移 MySQL 数据库移到 SQL Server-Azure SQL 数据库&#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[连接到 SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
