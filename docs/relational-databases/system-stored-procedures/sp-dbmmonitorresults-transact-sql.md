---
title: sp_dbmmonitorresults (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorresults
- sp_dbmmonitorresults_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorresults
- database mirroring [SQL Server], monitoring
ms.assetid: d575e624-7d30-4eae-b94f-5a7b9fa5427e
caps.latest.revision: 46
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 16061dc41994cd032a9e6124d38abf3acb2e6be5
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33256666"
---
# <a name="spdbmmonitorresults-transact-sql"></a>sp_dbmmonitorresults (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从存储数据库镜像监视历史记录的状态表中返回所监视数据库的状态行，并允许您选择该过程是否预先获得最新状态。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_dbmmonitorresults database_name   
   , rows_to_return  
    , update_status   
```  
  
## <a name="arguments"></a>参数  
 *database_name*  
 指定返回其镜像状态的数据库。  
  
 *rows_to_return*  
 指定返回的行数：  
  
 0 = 最后一行  
  
 1 = 最后两小时的行  
  
 2 = 最后四小时的行  
  
 3 = 最后八小时的行  
  
 4 = 最后一天的行  
  
 5 = 最后两天的行  
  
 6 = 最后一个 100 行  
  
 7 = 最后一个 500 行  
  
 8 = 最后一个 1,000 行  
  
 9 = 最后 1,000,000 行  
  
 *update_status*  
 指定返回结果之前，过程：  
  
 0 = 不更新数据库的状态。 仅使用最后两行计算结果，其保留时间取决于何时刷新状态表。  
  
 1 = 数据库的状态更新通过调用**sp_dbmmonitorupdate**之前计算结果。 但是，如果已更新状态表在前 15 秒或用户不是成员的**sysadmin**固定服务器角色、 **sp_dbmmonitorresults**运行而不更新的状态。  
  
## <a name="return-code-values"></a>返回代码值  
 InclusionThresholdSetting  
  
## <a name="result-sets"></a>结果集  
 返回指定数据库的所请求行数的历史记录状态。 每一行包含以下信息：  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**sysname**|镜像数据库的名称。|  
|**角色**|**int**|服务器实例的当前镜像角色：<br /><br /> 1 = 主体<br /><br /> 2 = 镜像|  
|**mirroring_state**|**int**|数据库的状态：<br /><br /> 0 = 已挂起<br /><br /> 1 = 已断开连接<br /><br /> 2 = 正在同步<br /><br /> 3 = 挂起故障转移<br /><br /> 4 = 已同步|  
|**witness_status**|**int**|在数据库的数据库镜像会话中见证服务器的连接状态，可以是：<br /><br /> 0 = 未知<br /><br /> 1 = 已连接<br /><br /> 2 = 已断开|  
|**log_generation_rate**|**int**|自上次更新此数据库的镜像状态以来生成的日志量（KB/秒）。|  
|**unsent_log**|**int**|在主体的发送队列中未发送日志的大小 (KB)。|  
|**send_rate**|**int**|从主体向镜像发送日志的速度（KB/秒）。|  
|**unrestored_log**|**int**|镜像中重做队列的大小 (KB)。|  
|**recovery_rate**|**int**|镜像中的重做速度（KB/秒）。|  
|**transaction_delay**|**int**|所有事务的总计延迟（毫秒）。|  
|**transactions_per_sec**|**int**|在主体服务器实例上每秒发生的事务数。|  
|**average_delay**|**int**|由于数据库镜像的原因，每个事务在主体服务器实例上的平均延迟。 在高性能模式（即 SAFETY 属性设置为 OFF 时）中，此值通常是 0。|  
|**time_recorded**|**datetime**|数据库镜像监视器记录行的时间。 这是主体的系统时钟时间。|  
|**time_behind**|**datetime**|镜像数据库当前跟踪的主体的近似系统时钟时间。 此值只有在主体服务器实例上才有意义。|  
|**local_time**|**datetime**|更新此行时本地服务器实例上的系统时钟时间。|  
  
## <a name="remarks"></a>注释  
 **sp_dbmmonitorresults**可以仅在上下文中执行**msdb**数据库。  
  
## <a name="permissions"></a>权限  
 要求的成员身份**sysadmin**固定的服务器角色或在**dbm_monitor**中的固定的数据库角色**msdb**数据库。 **Dbm_monitor**角色可让其成员，若要查看数据库镜像状态，但不是更新它，但不是查看或配置数据库镜像事件。  
  
> [!NOTE]  
>  第一次**sp_dbmmonitorupdate**执行，它会创建**dbm_monitor**中的固定的数据库角色**msdb**数据库。 成员**sysadmin**固定的服务器角色可以添加到任何用户**dbm_monitor**固定的数据库角色。  
  
## <a name="examples"></a>示例  
 以下示例返回在前面两个小时内记录的行，但不更新数据库状态。  
  
```  
USE msdb;  
EXEC sp_dbmmonitorresults AdventureWorks2012, 2, 0;  
```  
  
## <a name="see-also"></a>另请参阅  
 [监视数据库镜像 (SQL Server)](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorchangemonitoring &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [sp_dbmmonitoraddmonitoring &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql.md)   
 [sp_dbmmonitordropmonitoring &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)   
 [sp_dbmmonitorhelpmonitoring &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorupdate (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dbmmonitorupdate-transact-sql.md)  
  
  
