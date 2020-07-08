---
title: managed_backup sp_backup_config_schedule （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 02/20/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 04e152b8ae15e4e0a810fb5ed945b4c8c69afe5b
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "86053450"
---
# <a name="managed_backupsp_backup_config_schedule-transact-sql"></a>managed_backup sp_backup_config_schedule （Transact-sql）
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  为配置自动或自定义计划选项 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 。  
    
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
  
##  <a name="arguments"></a><a name="Arguments"></a>形参  
 @database_name  
 用于在特定数据库上启用托管备份的数据库名称。 如果为 NULL 或 *，则此托管备份适用于服务器上的所有数据库。  
  
 @scheduling_option  
 为系统控制的备份计划指定 "系统"。 指定由其他均定义的自定义计划的 "自定义"。  
  
 @full_backup_freq_type  
 托管备份操作的频率类型，可以设置为 "每日" 或 "每周"。  
  
 @days_of_week  
 @full_backup_freq_type将备份设置为 "每周" 时的备份日期。 指定完整的字符串名称，如 "Monday"。  还可以指定多个以竖线分隔的星期名称。 例如 N'Monday |星期三 |星期五 "。  
  
 @backup_begin_time  
 备份窗口的开始时间。 不会在时间范围之外启动备份，这是由和的组合定义的 @backup_begin_time @backup_duration 。  
  
 @backup_duration  
 备份时间窗口的持续时间。 请注意，不能保证在和定义的时间范围内完成备份 @backup_begin_time @backup_duration 。 在此时间窗口中启动但超过窗口持续时间的备份操作不会被取消。  
  
 @log_backup_freq  
 这会确定事务日志备份的频率。 这些备份定期发生，而不是按为数据库备份指定的计划进行。 @log_backup_freq可以是分钟或小时，并且 `0:00` 有效，表示没有日志备份。 禁用日志备份仅适用于具有简单恢复模式的数据库。  
  
> [!NOTE]  
>  如果恢复模式从 simple 更改为 full，则需要将 log_backup_freq 从重新配置 `0:00` 为非零值。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>权限  
 要求具有**db_backupoperator**数据库角色的成员身份，具有**ALTER ANY CREDENTIAL**权限以及对**sp_delete_backuphistory**存储过程的**EXECUTE**权限。  
  
## <a name="see-also"></a>另请参阅  
 [managed_backup sp_backup_config_basic （Transact-sql）](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup.sp_backup_config_advanced (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)  
  
  
