---
title: sp_helptracertokenhistory (Transact SQL) |Microsoft 文档
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
- sp_helptracertokenhistory_TSQL
- sp_helptracertokenhistory
helpviewer_keywords:
- sp_helptracertokenhistory
ms.assetid: 96910d1c-be76-43eb-9c93-4477e6761749
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 6cab0dacd02e57cead03cdb0aeef35a385afb349
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32996684"
---
# <a name="sphelptracertokenhistory-transact-sql"></a>sp_helptracertokenhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回指定跟踪令牌的详细滞后时间信息，为每个订阅服务器返回一行。 此存储过程在发布服务器上的发布数据库中执行，或者在分发服务器上的分发数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helptracertokenhistory [ @publication = ] 'publication'   
        , [ @tracer_id = ] tracer_id  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@publication=** ] *****发布*****  
 已插入跟踪令牌的发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@tracer_id=** ] *tracer_id*  
 是中的跟踪令牌 ID [MStracer_tokens &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md)信息返回历史记录表。 *tracer_id*是**int**，无默认值。  
  
 [  **@publisher=** ] *****发布服务器*****  
 发布服务器的名称。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  此参数应仅为指定非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
 [  **@publisher_db=** ] *****publisher_db*****  
 发布数据库的名称。 *publisher_db*是**sysname**，默认值为 NULL。 如果在发布服务器上执行该存储过程，将忽略此参数。  
  
## <a name="result-set"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**distributor_latency**|**bigint**|在发布服务器上提交的跟踪令牌记录和在分发服务器上提交的记录之间的秒数。|  
|**订阅服务器**|**sysname**|收到跟踪令牌的订阅服务器的名称。|  
|**subscriber_db**|**sysname**|在其中插入跟踪令牌记录的订阅数据库的名称。|  
|**subscriber_latency**|**bigint**|在分发服务器上提交的跟踪令牌记录和在订阅服务器上提交的记录间隔的秒数。|  
|**overall_latency**|**bigint**|在发布服务器上提交的跟踪令牌记录和在订阅服务器上提交的令牌记录间隔的秒数。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_helptracertokenhistory**事务复制中使用。  
  
 执行[sp_helptracertokens &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md)以获取发布的跟踪令牌的列表。  
  
 结果集中的 NULL 值意味着无法计算滞后时间统计信息。 这是因为分发服务器或其中一个订阅服务器尚未接收到跟踪令牌。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-helptracertokenhistor_1.sql)]  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定服务器角色、 **db_owner**在发布数据库中，固定数据库角色或**db_owner**固定的数据库或**replmonitor**分发数据库中的角色可以执行**sp_helptracertokenhistory**。  
  
## <a name="see-also"></a>另请参阅  
 [为事务复制测量滞后时间和验证连接](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [sp_deletetracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md)  
  
  
