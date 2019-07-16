---
title: sp_help_log_shipping_monitor_secondary (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_monitor_secondary
- sp_help_log_shipping_monitor_secondary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_monitor_secondary
ms.assetid: 3ac091ea-c9a8-4c05-a0b6-1ccf4e001339
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b1acf456bda88eeee0493d3f9d7ccc063a5bda50
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001006"
---
# <a name="sphelplogshippingmonitorsecondary-transact-sql"></a>sp_help_log_shipping_monitor_secondary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从监视表返回关于辅助数据库的信息。  
  
 
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_help_log_shipping_monitor_secondary  
[ @secondary_server = ] 'secondary_server',  
[ @secondary_database = ] 'secondary_database'  
```  
  
## <a name="arguments"></a>参数  
`[ @secondary_server = ] 'secondary_server'` 是辅助服务器的名称。 *secondary_server*是**sysname**，无默认值。  
  
`[ @secondary_database = ] 'secondary_database'` 为辅助数据库的名称。 *secondary_database*是**sysname**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|“列”|描述|  
|------------|-----------------|  
|**secondary_server**|辅助实例的名称[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]日志传送配置中。|  
|**secondary_database**|日志传送配置中辅助数据库的名称。|  
|**secondary_id**|日志传送配置中辅助服务器的 ID。|  
|**primary_server**|日志传送配置中 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]主实例的名称。|  
|**primary_database**|日志传送配置中主数据库的名称。|  
|**restore_threshold**|两次还原操作之间允许的间隔时间（分钟），一旦超过此值，就会生成警报。|  
|**threshold_alert**|超过还原阈值时引发的警报。|  
|**threshold_alert_enabled**|确定是否启用了还原阈值警报。<br /><br /> 1 = 已启用。<br /><br /> 0 = 禁用。|  
|**last_copied_file**|上次复制到辅助服务器的备份文件的文件名。|  
|**last_copied_date**|上次复制到辅助服务器的时间和日期。|  
|**last_copied_date_utc**|上次对辅助服务器执行复制操作的时间和日期，以通用协调时间表示。|  
|**last_restored_file**|上次还原到辅助数据库的备份文件的文件名。|  
|**last_restored_date**|上次对辅助数据库执行还原操作的时间和日期。|  
|**last_restored_date_utc**|上次对辅助数据库执行还原操作的时间和日期，以通用协调时间表示。|  
|**history_retention_period**|日志传送历史记录在删除前保留在给定辅助数据库中的时间（分钟）。|  
  
## <a name="remarks"></a>备注  
 **sp_help_log_shipping_monitor_secondary**必须从运行**主**在监视服务器上的数据库。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以运行此过程。  
  
## <a name="see-also"></a>请参阅  
 [关于日志传送 (SQL Server)](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
