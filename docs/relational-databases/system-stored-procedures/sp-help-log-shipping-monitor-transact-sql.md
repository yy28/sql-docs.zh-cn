---
title: sp_help_log_shipping_monitor (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_monitor_TSQL
- sp_help_log_shipping_monitor
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_monitor
ms.assetid: a4e96c45-6dcd-471a-a494-b5c619459855
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e1f51b575ff8ee40db402fe48cacf8396b89ac45
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43027075"
---
# <a name="sphelplogshippingmonitor-transact-sql"></a>sp_help_log_shipping_monitor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回一个结果集，其中包含主服务器、辅助服务器或监视服务器上注册的主数据库和辅助数据库的状态和其他信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_help_log_shipping_monitor  
```  
  
## <a name="arguments"></a>参数  
 无。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**status**|**bit**|日志传送数据库代理的共同状态。<br /><br /> **0** = 正常运行，无代理失败。<br /><br /> **1** = 其他。|  
|**is_primary**|**bit**|指示该行是否用于主数据库：<br /><br /> **1** = 行是主数据库。<br /><br /> **0** = 行是针对辅助数据库。|  
|服务器|**sysname**|此数据库所在的主服务器或辅助服务器的名称。|  
|**database_name**|**sysname**|数据库名称。|  
|**time_since_last_backup**|**int**|最后一次备份日志以来的时间，以分钟为单位。<br /><br /> NULL = 信息不可用或者不相关。|  
|**last_backup_file**|**nvarchar(500)**|上一个成功的备份日志文件的名称。<br /><br /> NULL = 信息不可用或者不相关。|  
|**backup_threshold**|**int**|上一次备份到引发 threshold_alert 错误之间的时间，以分钟为单位。 **backup_threshold**是**int**，默认值为**60 分钟**。<br /><br /> NULL = 信息不可用或者不相关。<br /><br /> 可以使用更改该值[sp_add_log_shipping_primary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)。|  
|**is_backup_alert_enabled**|**bit**|指定是否将是警报时引发**backup_threshold**超出。 一个值 (**1**)，默认值，表示将会引发警报。<br /><br /> NULL = 信息不可用或者不相关。<br /><br /> 可以使用更改该值[sp_add_log_shipping_primary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)。|  
|**time_since_last_copy**|**int**|上次复制日志备份以来的时间，以分钟为单位。<br /><br /> NULL = 信息不可用或者不相关。|  
|**last_copied_file**|**nvarchar(500)**|上一次成功复制的日志备份文件的名称。<br /><br /> NULL = 信息不可用或者不相关。|  
|**time_since_last_restore**|**int**|上一次还原日志备份以来的时间，以分钟为单位。<br /><br /> NULL = 信息不可用或者不相关。|  
|**last_restored_file**|**nvarchar(500).**|上一次成功还原的日志备份文件的名称。<br /><br /> NULL = 信息不可用或者不相关。|  
|**last_restored_latency**|**int**|上一次创建备份到还原该备份的时间，以分钟为单位。<br /><br /> NULL = 信息不可用或者不相关。|  
|**restore_threshold**|**int**|两次还原操作之间允许的间隔时间（分钟），一旦超过此值，就会生成警报。 **restore_threshold**不能为 NULL。|  
|**is_restore_alert_enabled**|**bit**|指定是否引发警报时**restore_threshold**超出。 一个值 (**1**)，默认值，表示要引发警报。<br /><br /> NULL = 信息不可用或者不相关。<br /><br /> 若要设置还原阈值，请使用[sp_add_log_shipping_secondary_database](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md)。|  
  
## <a name="remarks"></a>Remarks  
 **sp_help_log_shipping_monitor**必须从运行**主**在监视服务器上的数据库。  
  
## <a name="permissions"></a>Permissions  
 要求具有 **sysadmin** 固定服务器角色的成员身份。  
  
## <a name="see-also"></a>请参阅  
 [关于日志传送 (SQL Server)](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
