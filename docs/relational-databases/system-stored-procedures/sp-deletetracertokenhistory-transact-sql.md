---
title: sp_deletetracertokenhistory (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_deletetracertokenhistory
- sp_deletetracertokenhistory_TSQL
helpviewer_keywords:
- sp_deletetracertokenhistory
ms.assetid: 9ae1be14-0d2f-40b1-9d6e-22d79726abf4
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: fdfe59e931fe224106eddb9358a5cba06e57c61a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spdeletetracertokenhistory-transact-sql"></a>sp_deletetracertokenhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除跟踪令牌记录从[MStracer_tokens &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md)和[MStracer_history &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/mstracer-history-transact-sql.md)系统表。 此存储过程在发布服务器上的发布数据库中执行，或者在分发服务器上的分发数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_deletetracertokenhistory [ @publication = ] 'publication'   
    [ , [ @tracer_id = ] tracer_id ]  
    [ , [ @cutoff_date = ] cutoff_date ]  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@publication=** ] *****发布*****  
 已插入跟踪令牌的发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@tracer_id=** ] *tracer_id*  
 要删除的跟踪令牌的 ID。 *tracer_id*是**int**，默认值为 NULL。 如果**null**，则将删除属于该发布的所有跟踪令牌。  
  
 [  **@cutoff_date=** ] *cutoff_date*  
 指定一个截止日期，以便删除在该日期之前插入发布的所有跟踪令牌。 *cutoff_date*是日期时间，默认值为 NULL。  
  
 [  **@publisher=** ] *****发布服务器*****  
 发布服务器的名称。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  此参数应仅为指定非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
 [  **@publisher_db=** ] *****publisher_db*****  
 发布数据库的名称。 *publisher_db*是**sysname**，默认值为 NULL。 如果在发布服务器上执行该存储过程，将忽略此参数。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_deletetracertokenhistory**事务复制中使用。  
  
 在执行时**sp_deletetracertokenhistory**，您可以仅指定其中一个*tracer_id*或*cutoff_date*。 如果同时指定了这两个参数，便会发生错误。  
  
 如果你不会执行**sp_deletetracertokenhistory**若要删除跟踪令牌元数据，信息将被删除时执行定期计划历史记录清理。  
  
 跟踪令牌 Id 可以由执行[sp_helptracertokens &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md)也可以通过查询[MStracer_tokens &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md)系统表。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定服务器角色、 **db_owner**在发布数据库中，固定数据库角色或**db_owner**固定的数据库或**replmonitor**分发数据库中的角色可以执行**sp_deletetracertokenhistory**。  
  
## <a name="see-also"></a>另请参阅  
 [为事务复制测量滞后时间和验证连接](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [sp_helptracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)  
  
  
