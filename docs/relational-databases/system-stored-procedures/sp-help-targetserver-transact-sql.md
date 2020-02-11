---
title: sp_help_targetserver （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_targetserver_TSQL
- sp_help_targetserver
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_targetserver
ms.assetid: f841d3bd-901a-4980-ad0b-1c6eeba3f717
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1eb9a4d1a19f54f9e57e988b350594ce6031b243
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68085072"
---
# <a name="sp_help_targetserver-transact-sql"></a>sp_help_targetserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出所有的目标服务器。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_help_targetserver   
     [ [ @server_name = ] 'server_name' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @server_name = ] 'server_name'`要返回其信息的服务器的名称。 *server_name*为**nvarchar （30）**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 如果未指定*server_name* ， **sp_help_targetserver**返回此结果集。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|服务器标识号。|  
|server_name |**nvarchar （30）**|服务器名称。|  
|**位置**|**nvarchar （200）**|指定的服务器的位置。|  
|**time_zone_adjustment**|**int**|根据格林尼治标准时间 (GMT) 进行的时区调整，以小时为单位。|  
|**enlist_date**|**datetime**|指定的服务器的登记日期。|  
|**last_poll_date**|**datetime**|上一次为作业轮询服务器的日期。|  
|**状态值**|**int**|指定的服务器的状态。|  
|**unread_instructions**|**int**|指示服务器是否有未读指令。 如果已下载所有行，则此列为**0**。|  
|**local_time**|**datetime**|目标服务器上的本地日期和时间，基于主服务器上一次轮询时目标服务器上的本地时间。|  
|**enlisted_by_nt_user**|**nvarchar （100）**|登记了目标服务器的 Microsoft Windows 用户。|  
|**poll_interval**|**int**|目标服务器为下载作业和上载作业状态而对 Master SQLServerAgent 服务进行轮询的频率（秒）。|  
  
## <a name="permissions"></a>权限  
 若要执行此存储过程，用户必须为 **sysadmin** 固定服务器角色的成员。  
  
## <a name="examples"></a>示例  
  
### <a name="a-listing-information-for-all-registered-target-servers"></a>A. 列出所有已注册的目标服务器的信息  
 以下示例将列出所有已注册的目标服务器的信息。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_targetserver ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-target-server"></a>B. 列出特定目标服务器的信息  
 以下示例将列出目标服务器 `SEATTLE2` 的信息。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_targetserver N'SEATTLE2' ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_add_targetservergroup &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql.md)   
 [sp_delete_targetserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)   
 [sp_delete_targetservergroup &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql.md)   
 [sp_update_targetservergroup &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql.md)   
 [sysdownloadlist &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysdownloadlist-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
