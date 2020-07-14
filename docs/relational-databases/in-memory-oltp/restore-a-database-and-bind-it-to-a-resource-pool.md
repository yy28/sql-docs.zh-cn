---
title: 还原数据库并将它绑定到资源池 | Microsoft Docs
description: 了解如何在 SQL Server 中还原带有内存优化表的数据库。 按照最佳做法将数据库绑定到命名资源池。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 0d20a569-8a27-409c-bcab-0effefb48013
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6a04204d4c3b5c637b4c3aac324bfe4b02265b39
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85722346"
---
# <a name="restore-a-database-and-bind-it-to-a-resource-pool"></a>还原数据库并将它绑定到资源池
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  即使有足够的内存来还原带有内存优化表的数据库，也想要采用最佳做法，将数据库绑定到命名资源池。 因为数据库在绑定到池之前必须存在，所以还原数据库这个过程分为几个步骤。 本主题将演练这一过程。  
  
## <a name="restoring-a-database-with-memory-optimized-tables"></a>还原带有内存优化表的数据库  
 以下步骤将完全还原数据库 IMOLTP_DB 并将其绑定到 Pool_IMOLTP。  
  
1.  [使用 NORECOVERY 还原](../../relational-databases/in-memory-oltp/restore-a-database-and-bind-it-to-a-resource-pool.md#bkmk_NORECOVERY)  
  
2.  [创建资源池](../../relational-databases/in-memory-oltp/restore-a-database-and-bind-it-to-a-resource-pool.md#bkmk_createPool)  
  
3.  [绑定数据库和资源池](../../relational-databases/in-memory-oltp/restore-a-database-and-bind-it-to-a-resource-pool.md#bkmk_bind)  
  
4.  [使用 RECOVERY 还原](../../relational-databases/in-memory-oltp/restore-a-database-and-bind-it-to-a-resource-pool.md#bkmk_RECOVERY)  
  
5.  [监视资源池性能](../../relational-databases/in-memory-oltp/restore-a-database-and-bind-it-to-a-resource-pool.md#bkmk_Monitor)  
  
###  <a name="restore-with-norecovery"></a><a name="bkmk_NORECOVERY"></a> 使用 NORECOVERY 还原  
 还原数据库时 ，NORECOVERY 将创建数据库并在不使用内存的情况下还原磁盘映像。  
  
```sql  
RESTORE DATABASE IMOLTP_DB   
   FROM DISK = 'C:\IMOLTP_test\IMOLTP_DB.bak'  
   WITH NORECOVERY  
```  
  
###  <a name="create-the-resource-pool"></a><a name="bkmk_createPool"></a> 创建资源池  
 以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 创建了名为 Pool_IMOLTP 的资源池，有 50% 内存可供其使用。  创建该池后，资源调控器重新配置为包括 Pool_IMOLTP。  
  
```sql  
CREATE RESOURCE POOL Pool_IMOLTP WITH (MAX_MEMORY_PERCENT = 50);  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
###  <a name="bind-the-database-and-resource-pool"></a><a name="bkmk_bind"></a> 绑定数据库和资源池  
 使用系统函数 `sp_xtp_bind_db_resource_pool` 将数据库绑定到资源池。 该函数使用两个参数：数据库名称，然后是资源池名称。  
  
 以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 定义数据库 IMOLTP_DB 与资源池 Pool_IMOLTP 的绑定。 完成下一步骤后，绑定才生效。  
  
```sql  
EXEC sp_xtp_bind_db_resource_pool 'IMOLTP_DB', 'Pool_IMOLTP'  
GO  
```  
  
###  <a name="restore-with-recovery"></a><a name="bkmk_RECOVERY"></a> 使用 RECOVERY 还原  
 使用 RECOVERY 还原数据库时，数据库将联机并还原所有数据。  
  
```sql  
RESTORE DATABASE IMOLTP_DB   
   WITH RECOVERY  
```  
  
###  <a name="monitor-the-resource-pool-performance"></a><a name="bkmk_Monitor"></a> 监视资源池性能  
 一旦数据库绑定到命名的资源池并使用 RECOVERY 还原，请监视 Resource Pool Stats 对象 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅 [SQL Server, Resource Pool Stats 对象](../../relational-databases/performance-monitor/sql-server-resource-pool-stats-object.md)。  
  
## <a name="see-also"></a>另请参阅  
 [数据库与资源池绑定的指南，请参阅主题](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [sys.sp_xtp_bind_db_resource_pool (Transact-SQL)](../../relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql.md)   
 [SQL Server，Resource Pool Stats 对象](../../relational-databases/performance-monitor/sql-server-resource-pool-stats-object.md)   
 [sys.dm_resource_governor_resource_pools](../../relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql.md)  
  
  
