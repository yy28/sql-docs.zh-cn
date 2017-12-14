---
title: "还原数据库并将它绑定到资源池 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0d20a569-8a27-409c-bcab-0effefb48013
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0123a452a34fc5d445499fa1ba372a458cdcff60
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="restore-a-database-and-bind-it-to-a-resource-pool"></a>还原数据库并将它绑定到资源池
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]即使有足够的内存来还原带有内存优化表的数据库，也会想采用最佳做法，并将数据库绑定到命名资源池。 因为数据库在绑定到池之前必须存在，所以还原数据库这个过程分为几个步骤。 本主题将演练这一过程。  
  
## <a name="restoring-a-database-with-memory-optimized-tables"></a>还原带有内存优化表的数据库  
 以下步骤将完全还原数据库 IMOLTP_DB 并将其绑定到 Pool_IMOLTP。  
  
1.  [使用 NORECOVERY 还原](../../relational-databases/in-memory-oltp/restore-a-database-and-bind-it-to-a-resource-pool.md#bkmk_NORECOVERY)  
  
2.  [创建资源池](../../relational-databases/in-memory-oltp/restore-a-database-and-bind-it-to-a-resource-pool.md#bkmk_createPool)  
  
3.  [绑定数据库和资源池](../../relational-databases/in-memory-oltp/restore-a-database-and-bind-it-to-a-resource-pool.md#bkmk_bind)  
  
4.  [使用 RECOVERY 还原](../../relational-databases/in-memory-oltp/restore-a-database-and-bind-it-to-a-resource-pool.md#bkmk_RECOVERY)  
  
5.  [监视资源池性能](../../relational-databases/in-memory-oltp/restore-a-database-and-bind-it-to-a-resource-pool.md#bkmk_Monitor)  
  
###  <a name="bkmk_NORECOVERY"></a> 使用 NORECOVERY 还原  
 还原数据库时 ，NORECOVERY 将创建数据库并在不使用内存的情况下还原磁盘映像。  
  
```tsql  
RESTORE DATABASE IMOLTP_DB   
   FROM DISK = 'C:\IMOLTP_test\IMOLTP_DB.bak'  
   WITH NORECOVERY  
```  
  
###  <a name="bkmk_createPool"></a> 创建资源池  
 以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 创建了名为 Pool_IMOLTP 的资源池，有 50% 内存可供其使用。  创建该池后，资源调控器重新配置为包括 Pool_IMOLTP。  
  
```tsql  
CREATE RESOURCE POOL Pool_IMOLTP WITH (MAX_MEMORY_PERCENT = 50);  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
###  <a name="bkmk_bind"></a> 绑定数据库和资源池  
 使用系统函数 `sp_xtp_bind_db_resource_pool` 将数据库绑定到资源池。 该函数使用两个参数：数据库名称，然后是资源池名称。  
  
 以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 定义数据库 IMOLTP_DB 与资源池 Pool_IMOLTP 的绑定。 完成下一步骤后，绑定才生效。  
  
```tsql  
EXEC sp_xtp_bind_db_resource_pool 'IMOLTP_DB', 'Pool_IMOLTP'  
GO  
```  
  
###  <a name="bkmk_RECOVERY"></a> 使用 RECOVERY 还原  
 使用 RECOVERY 还原数据库时，数据库将联机并还原所有数据。  
  
```tsql  
RESTORE DATABASE IMOLTP_DB   
   WITH RECOVERY  
```  
  
###  <a name="bkmk_Monitor"></a> 监视资源池性能  
 一旦数据库绑定到命名的资源池并使用 RECOVERY 还原，请监视 Resource Pool Stats 对象 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅 [SQL Server, Resource Pool Stats 对象](../../relational-databases/performance-monitor/sql-server-resource-pool-stats-object.md)。  
  
## <a name="see-also"></a>另请参阅  
 [将具有内存优化表的数据库绑定至资源池](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [sys.sp_xtp_bind_db_resource_pool (Transact-SQL)](../../relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql.md)   
 [SQL Server, Resource Pool Stats 对象](../../relational-databases/performance-monitor/sql-server-resource-pool-stats-object.md)   
 [sys.dm_resource_governor_resource_pools](../../relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql.md)  
  
  
