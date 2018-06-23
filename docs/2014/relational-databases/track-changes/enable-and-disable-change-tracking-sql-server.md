---
title: 启用和禁用更改跟踪 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- change tracking [SQL Server], disabling
- data changes [SQL Server]
- change tracking [SQL Server], enabling
- tracking data changes [SQL Server]
- change tracking [SQL Server], configuring
- data [SQL Server], changing
ms.assetid: 1c92ec7e-ae53-4498-8bfd-c66a42a24d54
caps.latest.revision: 33
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 3255499badecbba1ac0c87b7ba499fef1ca210aa
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015651"
---
# <a name="enable-and-disable-change-tracking-sql-server"></a>启用和禁用更改跟踪 (SQL Server)
  本主题说明如何对数据库和表启用和禁用更改跟踪。  
  
## <a name="enable-change-tracking-for-a-database"></a>对数据库启用更改跟踪  
 您必须先在数据库级别启用更改跟踪，然后才能使用更改跟踪。 下面的示例显示了如何使用 [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-options)来启用更改跟踪。  
  
```tsql  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = ON  
(CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON)  
```  
  
 你还可以通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 数据库属性（“ChangeTracking”页） [数据库属性（“ChangeTracking”页）](../databases/database-properties-changetracking-page.md) 中启用更改跟踪。  
  
 可以在启用更改跟踪时指定 CHANGE_RETENTION 和 AUTO_CLEANUP 选项，并且可以在启用更改跟踪后随时更改这些值。  
  
 更改保持期值指定了更改跟踪信息的保留时间。 早于此时间的更改跟踪信息将被定期删除。 设置该值时，应考虑应用程序与数据库中的表进行同步的频率。 指定的保持期必须至少等于最大同步时间间隔。 如果应用程序获取更改的时间间隔过长，则返回的结果可能不正确，因为某些更改信息可能已被删除。 若要避免获取错误的结果，应用程序可以使用 CHANGE_TRACKING_MIN_VALID_VERSION 系统函数来确定同步之间的时间间隔是否已太长。  
  
 可使用 AUTO_CLEANUP 选项来启用或禁用删除陈旧的更改跟踪信息的清除任务。 如果出现临时性问题使得应用程序无法同步，并且在问题解决之前必须暂停用于删除早于保持期的更改跟踪信息的进程，则该设置会很有用。  
  
 对于使用更改跟踪的任何数据库，请注意以下事项：  
  
-   若要使用更改跟踪，必须将数据库兼容级别设为 90 或更高。 如果数据库的兼容级别低于 90，则可以配置更改跟踪。 但是，用于获取更改跟踪信息的 CHANGETABLE 函数将返回错误。  
  
-   使用快照隔离是帮助确保所有更改跟踪信息保持一致的最简单方式。 因此，我们强烈建议将数据库的快照隔离设为 ON。 有关详细信息，请参阅[处理更改跟踪 (SQL Server)](work-with-change-tracking-sql-server.md)。  
  
## <a name="enable-change-tracking-for-a-table"></a>对表启用更改跟踪  
 对于要跟踪的每个表都必须启用更改跟踪。 启用更改跟踪后，将会为表中受 DML 操作影响的所有行保留更改跟踪信息。  
  
 下面的示例显示了如何使用 [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql)来对表启用更改跟踪。  
  
```tsql  
ALTER TABLE Person.Contact  
ENABLE CHANGE_TRACKING  
WITH (TRACK_COLUMNS_UPDATED = ON)  
```  
  
 你还可以通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 数据库属性（“ChangeTracking”页） [数据库属性（“ChangeTracking”页）](../databases/database-properties-changetracking-page.md) 中启用更改跟踪。  
  
 当 TRACK_COLUMNS_UPDATED 选项设为 ON 时， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 会将有关哪些列已更新的额外信息存储到内部更改跟踪表中。 列跟踪使应用程序可以只同步那些已更新的列。 这可以提高效率和性能。 但是，由于保留列跟踪信息增加了一些额外的存储开销，因而默认情况下此选项设为 OFF。  
  
## <a name="disable-change-tracking-for-a-database-or-table"></a>为数据库或表禁用更改跟踪  
 必须首先为所有启用了更改跟踪的表禁用更改跟踪，然后才能将数据库的更改跟踪设为 OFF。 若要确定数据库中哪些表启用了更改跟踪，请使用 [sys.change_tracking_tables](/sql/relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables) 目录视图。  
  
 当数据库中没有用于跟踪更改的表时，便可以禁用数据库的更改跟踪。 下面的示例显示如何使用 [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-options)对数据库禁用更改跟踪。  
  
```tsql  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = OFF  
```  
  
 下面的示例显示了如何使用 [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql)对表禁用更改跟踪。  
  
```tsql  
ALTER TABLE Person.Contact  
DISABLE CHANGE_TRACKING;  
```  
  
## <a name="see-also"></a>请参阅  
 [数据库属性（“ChangeTracking”页）](../databases/database-properties-changetracking-page.md)   
 [ALTER DATABASE SET 选项 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-set-options)   
 [sys.change_tracking_databases (Transact-SQL)](/sql/relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-databases)   
 [sys.change_tracking_tables (Transact-SQL)](/sql/relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables)   
 [跟踪数据更改 (SQL Server)](track-data-changes-sql-server.md)   
 [关于更改跟踪 (SQL Server)](../track-changes/about-change-tracking-sql-server.md)   
 [处理变更数据 (SQL Server)](work-with-change-data-sql-server.md)   
 [管理更改跟踪 (SQL Server)](manage-change-tracking-sql-server.md)  
  
  
