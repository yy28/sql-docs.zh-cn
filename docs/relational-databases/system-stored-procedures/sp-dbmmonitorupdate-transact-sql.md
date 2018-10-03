---
title: sp_dbmmonitorupdate (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorupdate
- sp_dbmmonitorupdate_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorupdate
- database mirroring [SQL Server], monitoring
ms.assetid: 9ceb9611-4929-44ee-a406-c39ba2720fd5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f8ee54383074e624d082d2ab782d6b038fd03d06
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47817056"
---
# <a name="spdbmmonitorupdate-transact-sql"></a>sp_dbmmonitorupdate (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  通过为每个镜像数据库插入新的表行来更新数据库镜像监视器状态表，并截断早于当前保持期的行。 默认保持期是 7 天（168 小时）。 更新表时**sp_dbmmonitorupdate**计算性能指标。  
  
> [!NOTE]  
>  第一次**sp_dbmmonitorupdate**运行时，它将创建数据库镜像状态表并**dbm_monitor**固定的数据库角色的**msdb**数据库。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_dbmmonitorupdate [ database_name ]  
```  
  
## <a name="arguments"></a>参数  
 *database_name*  
 要更新镜像状态的数据库的名称。 如果*database_name*未指定，则该过程会更新状态表中每个镜像数据库的服务器实例上。  
  
## <a name="return-code-values"></a>返回代码值  
 None  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>备注  
 **sp_dbmmonitorupdate**可以执行的上下文中仅**msdb**数据库。  
  
 如果状态表的某一列不适用于伙伴的角色，则该值在此伙伴上为 NULL。 如果列中的相关信息不可用（例如，在故障转移或服务器重新启动期间），该列也会有 NULL 值。  
  
 之后**sp_dbmmonitorupdate**创建**dbm_monitor**固定的数据库角色的**msdb**数据库的成员**sysadmin**固定的服务器角色可以添加到任何用户**dbm_monitor**固定的数据库角色。 **Dbm_monitor**角色使其成员可以查看数据库镜像状态，但不是更新它，但不是查看或配置数据库镜像事件。  
  
 更新数据库的镜像状态时**sp_dbmmonitorupdate**检查已为其任何镜像性能指标的指定警告阈值的最新值。 如果该值超过阈值，则该过程会向事件日志中添加信息性事件。 所有汇率都是自最后一次更新以来的平均值。 有关详细信息，请参阅 [使用镜像性能度量的警告阈值和警报 (SQL Server)](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)。  
  
## <a name="permissions"></a>Permissions  
 要求具有 **sysadmin** 固定服务器角色的成员身份。  
  
## <a name="examples"></a>示例  
 以下示例将只更新 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库的镜像状态。  
  
```  
USE msdb;  
EXEC sp_dbmmonitorupdate AdventureWorks2012 ;  
```  
  
## <a name="see-also"></a>请参阅  
 [监视数据库镜像 (SQL Server)](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorchangealert &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)   
 [sp_dbmmonitorchangemonitoring &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [sp_dbmmonitordropalert &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)   
 [sp_dbmmonitorhelpalert &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpalert-transact-sql.md)   
 [sp_dbmmonitorhelpmonitoring &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorresults (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
