---
title: managed_backup.sp_backup_config_schedule (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
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
ms.openlocfilehash: 8ebeca4b0a1c9079f8786303207bcbae4dfe74c3
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38035275"
---
# <a name="managedbackupspbackupconfigschedule-transact-sql"></a>managed_backup.sp_backup_config_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  将配置为自动或自定义计划选项[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。  
    
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
 启用托管的备份上特定数据库的数据库名称。 如果为 NULL 或 *，则此托管的备份适用于服务器上的所有数据库。  
  
 @scheduling_option  
 为系统控制的备份计划中指定系统。 为自定义计划定义的其他参数指定自定义。  
  
 @full_backup_freq_type  
 托管备份操作，可以设置为 Daily 或每周频率类型。  
  
 @days_of_week  
 备份每周天数时@full_backup_freq_type设置为每周。 指定完整的字符串名称，如星期一。  此外可以指定多个一天的名称，由竖线分隔。 例如 N'Monday |星期三 |星期五。  
  
 @backup_begin_time  
 备份窗口开始时间。 备份将不会启动的组合定义的时间窗口之外@backup_begin_time和@backup_duration。  
  
 @backup_duration  
 备份时间窗口的持续时间。 请注意，没有定义的时间窗口期间将已完成的备份不能保证@backup_begin_time和@backup_duration。 在此时间窗口中启动，但超过时段的持续时间的备份操作不会取消。  
  
 @log_backup_freq  
 这将确定事务日志备份的频率。 这些备份进行按固定间隔，而不是指定数据库备份的计划。 @log_backup_freq 可以为分钟或几小时，0 是有效的这表示未执行日志备份。 禁用日志备份仅将适用于使用简单恢复模式的数据库。  
  
> [!NOTE]  
>  如果恢复模式从简单更改为完整，您需要重新配置为非零值从 0 log_backup_freq。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>权限  
 要求的成员身份**db_backupoperator**数据库角色的**ALTER ANY CREDENTIAL**权限，并且**EXECUTE**权限**sp_delete_backuphistory**存储过程。  
  
## <a name="see-also"></a>请参阅  
 [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup.sp_backup_config_advanced (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)  
  
  
