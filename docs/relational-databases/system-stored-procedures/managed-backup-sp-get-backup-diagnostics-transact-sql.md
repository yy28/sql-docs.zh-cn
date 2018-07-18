---
title: managed_backup.sp_get_backup_diagnostics (TRANSACT-SQL) |Microsoft Docs
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
- sp_get_backup_diagnostics_TSQL
- sp_get_backup_diagnostics
- smart_admin.sp_get_backup_diagnostics_TSQL
- smart_admin.sp_get_backup_diagnostics
dev_langs:
- TSQL
helpviewer_keywords:
- sp_get_backup_diagnostics
- smart_admin.sp_get_backup_diagnostics
ms.assetid: 2266a233-6354-464b-91ec-824ca4eb9ceb
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e2b2f8c78b1802ff177040352cd7342b51b035c6
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38051315"
---
# <a name="managedbackupspgetbackupdiagnostics-transact-sql"></a>managed_backup.sp_get_backup_diagnostics (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  返回由智能管理记录的扩展事件。  
  
 使用此存储的过程来监视由智能管理记录的扩展事件[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]事件记录在此系统并可以查看和使用此存储的过程监视。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql  
managed_backup.sp_get_backup_diagnostics [@xevent_channel = ] 'event type' [, [@begin_time = ] 'time1' ] [, [@end_time = ] 'time2'VARCHAR(255) = 'Xevent',@begin_time DATETIME = NULL,@end_time DATETIME = NULL  
```  
  
##  <a name="Arguments"></a> 参数  
 @xevent_channel  
 扩展事件的类型。 默认值设置为返回之前 30 分钟内记录的所有事件。 记录的事件取决于所启用扩展事件的类型。 您可以使用此参数对存储过程进行筛选，仅显示特定类型的事件。 您可以指定完整的事件名称，也可以指定子字符串，如：**管理员**， **Analytic**， **Operational**，以及 **'Debug'**. @event_channel是**VARCHAR (255)**。  
  
 若要获取的事件类型当前启用了使用列表**managed_backup.fn_get_current_xevent_settings**函数。  
  
 [@begin_time  
 应显示的事件对应的时间段的开始时间。 @begin_time参数是 DATETIME，默认值为 NULL。 如果不指定，则将显示过去 30 分钟的事件。  
  
 @end_time  
 应显示的事件对应的时间段的结束时间。 @end_time参数是 DATATIME，默认值为 NULL。  如果不指定，则将显示截止到当前时间的事件。  
  
## <a name="table-returned"></a>返回的表  
 此存储过程返回包含以下信息的表：  
  
||||  
|-|-|-|  
|列名|数据类型|Description|  
|event_type|NVARCHAR(512)|扩展事件的类型。|  
|事件|NVARCHAR(512)|事件日志的摘要。|  
|时间戳|timestamp|显示事件发生时间的事件时间戳。|  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>权限  
 需要**EXECUTE**存储过程的权限。 它还需要**VIEW SERVER STATE**权限，因为它在内部调用其他系统对象的需要此权限。  
  
## <a name="examples"></a>示例  
 以下示例返回过去 30 分钟内记录的所有事件  
  
```  
Use msdb  
Go  
EXEC managed_backup.sp_get_backup_diagnostics  
  
```  
  
 以下示例返回某一特定时间范围内记录的所有事件。  
  
```  
Use msdb  
Go  
EXEC managed_backup.sp_get_backup_diagnostics @xevent_channel = 'Admin',  
  @begin_time = '2013-06-01', @end_time = '2013-06-10'  
  
```  
  
 以下示例返回过去 30 分钟内记录的所有分析事件  
  
```  
Use msdb  
Go  
EXEC managed_backup.sp_get_backup_diagnostics @xevent_channel = 'Analytic'  
  
```  
  
  
