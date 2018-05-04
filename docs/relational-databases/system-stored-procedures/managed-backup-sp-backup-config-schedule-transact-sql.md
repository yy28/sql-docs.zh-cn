---
title: managed_backup.sp_backup_config_schedule (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_backup_config_schedule_TSQL
- managed_backup.sp_backup_config_schedule
- managed_backup.sp_backup_config_schedule_TSQL
- sp_backup_config_schedule
dev_langs:
- TSQL
helpviewer_keywords:
- managed_backup.sp_backup_config_schedule
- sp_backup_config_schedule
ms.assetid: 82541160-d1df-4061-91a5-6868dd85743a
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a5f34d87103921bab2a583ce0356a45eea63ab53
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="managedbackupspbackupconfigschedule-transact-sql"></a>managed_backup.sp_backup_config_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  配置自动或自定义计划选项[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。  
    
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```vb  
EXEC managed_backup.sp_backup_config_schedule   
    [@database_name = ] 'database_name'
    ,[@scheduling_option = ] {'Custom' | 'System'}  
    ,[@full_backup_freq_type = ] {'Daily' | 'Weekly'}  
    ,[@days_of_week = ] 'days_of_the_week'  
    ,[@backup_begin_time = ] 'begin time of the backup window'  
    ,[@backup_duration = ] 'backup window length'  
    ,[@log_backup_freq = ] 'frequency of log backup'  
```  
  
##  <a name="Arguments"></a> 参数  
 @database_name  
 启用对特定数据库的托管的备份的数据库名称。 如果为 NULL 或 *，则此托管的备份适用于服务器上的所有数据库。  
  
 @scheduling_option  
 指定用于控制系统的备份计划的系统。 指定所定义的其他参数的自定义计划 Custom。  
  
 @full_backup_freq_type  
 托管备份操作，可以将设置为 Daily 或每周频率类型。  
  
 @days_of_week  
 备份每周天数时@full_backup_freq_type设置为每周。 指定类似星期一的完整字符串名称。  此外可以指定多个由竖线分隔的一天名称。 例如 N'Monday |星期三 |星期五。  
  
 @backup_begin_time  
 备份窗口开始时间。 备份将不会启动时间窗口，其中的组合来定义外部@backup_begin_time和@backup_duration。  
  
 @backup_duration  
 备份时间窗口的持续时间。 请注意，没有将由定义时间窗口内已完成备份不能保证@backup_begin_time和@backup_duration。 在此时间窗口中启动但超过时段的持续时间的备份操作将不会被取消。  
  
 @log_backup_freq  
 这将确定的事务日志备份的频率。 这些备份发生固定时间间隔中，而不是在数据库备份指定的计划。 @log_backup_freq 可以在几分钟或小时数，0 是有效的指示未执行日志备份。 禁用日志备份仅将适用于使用简单恢复模式的数据库。  
  
> [!NOTE]  
>  如果恢复模式从简单更改为完整，你需要重新配置为非零值从 0 log_backup_freq。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>权限  
 要求的成员身份**db_backupoperator**与数据库角色， **ALTER ANY CREDENTIAL**权限，和**执行**权限**sp_delete_backuphistory**存储过程。  
  
## <a name="see-also"></a>另请参阅  
 [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup.sp_backup_config_advanced (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)  
  
  
