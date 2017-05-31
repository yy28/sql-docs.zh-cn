---
title: "变更数据捕获和其他 SQL Server 功能 | Microsoft Docs"
ms.custom: 
ms.date: 05/03/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- change data capture [SQL Server], other SQL Server features and
ms.assetid: 7dfcb362-1904-4578-8274-da16681a960e
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 69a41e2138b3b2cc0768dacd0fca4e6363ee18e8
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="change-data-capture-and-other-sql-server-features"></a>变更数据捕获和其他 SQL Server 功能
  本主题说明下列功能如何与变更数据捕获交互：  
  
-   [更改跟踪](#ChangeTracking)  
  
-   [数据库镜像](#DatabaseMirroring)  
  
-   [事务复制](#TransReplication)  
  
-   [还原或附加启用了变更数据捕获的数据库](#RestoreOrAttach)  
  
##  <a name="ChangeTracking"></a> Change Tracking  
 可以对同一数据库启用变更数据捕获和 [更改跟踪](../../relational-databases/track-changes/about-change-tracking-sql-server.md) 。 没有特殊的注意事项。 有关详细信息，请参阅[处理更改跟踪 (SQL Server)](../../relational-databases/track-changes/work-with-change-tracking-sql-server.md)。  
  
##  <a name="DatabaseMirroring"></a> 数据库镜像  
 可以对启用变更数据捕获的数据库进行镜像。 为确保捕获和清除操作可在故障转移之后自动发生，请执行以下步骤：  
  
1.  确保在新的主体服务器实例上运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理。  
  
2.  在新的主体数据库（以前的镜像数据库）上创建捕获作业和清除作业。 若要创建作业，请使用 [sp_cdc_add_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md) 存储过程。  
  
 若要查看清除作业或捕获作业的当前配置，请在新的主体服务器实例上使用 [sys.sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md) 存储过程。 对于给定数据库，捕获作业名为 cdc.*database_name*_capture，清除作业名为 cdc.*database_name*_cleanup，其中 *database_name* 为数据库的名称。  
  
 若要更改作业的配置，请使用 [sys.sp_cdc_change_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql.md) 存储过程。  
  
 有关数据库镜像的信息，请参阅[数据库镜像 (SQL Server)](../../database-engine/database-mirroring/database-mirroring-sql-server.md)。  
  
##  <a name="TransReplication"></a> Transactional Replication  
 变更数据捕获和事务复制可以共存于同一数据库中，但在启用这两项功能后，更改表的填充处理方式将发生变化。 变更数据捕获和事务复制始终使用相同的过程 [sp_replcmds](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)从事务日志读取更改。 当单独启用变更数据捕获时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业会调用 **sp_replcmds**。 在同一数据库中启用这两项功能时，日志读取器代理会调用 **sp_replcmds**。 此代理将填充更改表和分发数据库表。 有关详细信息，请参阅 [Replication Log Reader Agent](../../relational-databases/replication/agents/replication-log-reader-agent.md)。  
  
 假设为 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库启用了变更数据捕获，并为捕获启用了两个表。 为了填充更改表，捕获作业将调用 **sp_replcmds**。 此外，还为该数据库启用了事务复制，并会创建发布。 此时，将为该数据库创建日志读取器代理，并删除捕获作业。 日志读取器代理继续从提交到更改表的最后一个日志序列号开始扫描日志。 这样将确保更改表中的数据一致性。 如果在此数据库中禁用事务复制，则会删除日志读取器代理，并重新创建捕获作业。  
  
> [!NOTE]  
>  当日志读取器代理同时用于变更数据捕获和事务复制时，复制的更改将首先写入分发数据库。 然后，捕获的更改会写入更改表。 两项操作会一起提交。 如果在写入分发数据库时有任何滞后时间，则在更改显示在更改表中之前，将有对应的滞后时间。  
  
 在启用了变更数据捕获的情况下，无法使用事务性复制的 **proc exec** 选项。  
  
##  <a name="RestoreOrAttach"></a> 还原或附加启用了变更数据捕获的数据库  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用以下逻辑确定还原或附加数据库后变更数据捕获是否继续保持启用状态：  
  
-   如果数据库以同一数据库名称还原到同一服务器，变更数据捕获将保持启用状态。  
  
-   如果数据库还原到其他服务器，默认情况下将禁用变更数据捕获，并删除所有相关的元数据。  
  
     若要保留变更数据捕获，请在还原数据库时使用 **KEEP_CDC** 选项。 有关此选项的详细信息，请参阅 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)。  
  
-   如果数据库在分离后附加到同一服务器或其他服务器，变更数据捕获将保持启用状态。  
  
-   如果使用 **KEEP_CDC** 选项将数据库附加或还原到企业版以外的任何版本，操作将被阻止，因为变更数据捕获需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 企业版。 将显示错误消息 934：  
  
     `SQL Server cannot load database '%.*ls' because Change Data Capture is enabled. The currently installed edition of SQL Server does not support Change Data Capture. Either restore database without KEEP_CDC option, or upgrade the instance to one that supports Change Data Capture.`  
  
 可以使用 [sys.sp_cdc_disable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md) 从还原或附加的数据库中删除变更数据捕获。  
  
## <a name="change-data-capture-and-always-on"></a>变更数据捕获和 Always On  
 使用 Always On 时，应在次要副本上更改枚举以减少主要副本的磁盘负荷。  
  
## <a name="see-also"></a>另请参阅  
 [管理和监视变更数据捕获 (SQL Server)](../../relational-databases/track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  

