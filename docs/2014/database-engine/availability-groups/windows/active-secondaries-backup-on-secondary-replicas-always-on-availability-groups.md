---
title: 活动次要副本：辅助副本 (Always On 可用性组） 上的备份 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- backup priority
- backup on secondary replicas
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], backup on secondary replicas
- active secondary replicas [SQL Server], backup on
- automated backup preference
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 82afe51b-71d1-4d5b-b20a-b57afc002405
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a94db154042f2cc6314459b6af4b52a43c2c9966
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62790676"
---
# <a name="active-secondaries-backup-on-secondary-replicas-always-on-availability-groups"></a>活动次要副本：(Always On 可用性组） 的辅助副本备份
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 活动辅助功能包括支持在辅助副本上执行备份操作。 备份操作可能会给 I/O 和 CPU 带来很大的压力（使用备份压缩）。 将备份负荷转移到已同步或正在同步的辅助副本后，您可以使用承载第一层工作负荷的主副本的服务器实例上的资源。  
  
> [!NOTE]  
>  在可用性组的主数据库或辅助数据库上不允许 RESTORE 语句。  
  
  
  
##  <a name="SupportedBuTypes"></a> 辅助副本上支持的备份类型  
  
-   `BACKUP DATABASE` 在辅助副本上执行时仅支持数据库、文件或文件组的仅复制完整备份。 请注意，仅复制备份不影响日志链，也不清除差异位图。  
  
-   辅助副本不支持差异备份。  
  
-   **BACKUP LOG** 仅支持常规日志备份（次要副本上的日志备份不支持 COPY_ONLY 选项）。  
  
     对于在任何副本（主副本或辅助副本）上进行的日志备份之间，确保一致的日志链，而与其可用性模式（同步提交或异步提交无关）。  
  
-   若要备份辅助数据库，辅助副本必须能够与主副本进行通信，并且状态必须为 `SYNCHRONIZED` 或 `SYNCHRONIZING`。  
  
##  <a name="WhereBuJobsRun"></a> 配置运行备份作业的位置  
 在辅助副本上执行备份以减轻主生产服务器的备份工作负荷非常有好处。 但是，对辅助副本执行备份会显著增加用于确定应在何处运行备份作业的过程的复杂性。 要解决这个问题，请按如下所示配置备份作业运行的位置：  
  
1.  配置可用性组以便指定要对其执行备份的可用性副本。 有关详细信息，请参阅 [CREATE AVAILABILITY GROUP (Transact-SQL)](/sql/t-sql/statements/create-availability-group-transact-sql) 或 [ALTER AVAILABILITY GROUP (Transact-SQL)](/sql/t-sql/statements/alter-availability-group-transact-sql) 中的 AUTOMATED_BACKUP_PREFERENCE 和 BACKUP_PRIORITY 参数。  
  
2.  为承载作为执行备份候选的可用性副本的每个服务器实例上的每个可用性数据库都创建编写了脚本的备份作业。 有关详细信息，请参阅“跟进：配置次要副本备份之后”部分，见[配置可用性副本备份 (SQL Server)](configure-backup-on-availability-replicas-sql-server.md)。  
  
##  <a name="RelatedTasks"></a> 相关任务  
 **配置辅助副本备份**  
  
-   [配置可用性副本备份 (SQL Server)](configure-backup-on-availability-replicas-sql-server.md)  
  
 **确定当前副本是否为首选备份副本**  
  
-   [sys.fn_hadr_backup_is_preferred_replica](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql)  
  
 **创建备份日志**  
  
-   [使用维护计划向导](../../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
-   [执行作业](../../../ssms/agent/implement-jobs.md)  
  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [仅复制备份 (SQL Server)](../../../relational-databases/backup-restore/copy-only-backups-sql-server.md)   
 [CREATE AVAILABILITY GROUP (Transact-SQL)](/sql/t-sql/statements/create-availability-group-transact-sql)   
 [ALTER AVAILABILITY GROUP (Transact-SQL)](/sql/t-sql/statements/alter-availability-group-transact-sql)  
  
  
