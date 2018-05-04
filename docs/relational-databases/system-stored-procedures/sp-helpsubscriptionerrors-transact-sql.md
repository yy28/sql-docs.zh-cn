---
title: sp_helpsubscriptionerrors (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_helpsubscriptionerrors_TSQL
- sp_helpsubscriptionerrors
helpviewer_keywords:
- sp_helpsubscriptionerrors
ms.assetid: 01c8bc21-939e-490d-8cc8-219c068be31e
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 87d33a74c37aaf101c9afd04a94b14939cbfb410
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpsubscriptionerrors-transact-sql"></a>sp_helpsubscriptionerrors (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回给定订阅的所有事务复制错误。 此存储过程在分发服务器上对分发数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpsubscriptionerrors [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'   
        , [ @publication = ] 'publication'   
        , [ @subscriber = ] 'subscriber'   
        , [ @subscriber_db = ] 'subscriber_db'  
```  
  
## <a name="arguments"></a>参数  
 [  **@publisher=** ] *****发布服务器*****  
 发布服务器的名称。 *发布服务器*是**sysname**，无默认值。  
  
 [  **@publisher_db=** ] *****publisher_db*****  
 发布数据库的名称。 *publisher_db*是**sysname**，无默认值。  
  
 [  **@publication=** ] *****发布*****  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@subscriber=** ] *****订阅服务器*****  
 订阅服务器的名称。 *订阅服务器*是**sysname**，无默认值。  
  
 [  **@subscriber_db=** ] *****subscriber_db*****  
 是订阅数据库的名称。 *subscriber_db*是**sysname**，无默认值。  
  
## <a name="result-set"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|错误 ID。|  
|**time**|**datetime**|发生错误时。|  
|**error_type_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**source_type_id**|**int**|错误源类型 ID。|  
|**source_name**|**nvarchar(100)**|错误源的名称。|  
|**error_code**|**sysname**|错误代码。|  
|**error_text**|**ntext**|错误消息。|  
|**xact_seqno**|**varbinary(16)**|失败的执行批处理的起始事务日志序列号。 仅由分发代理使用，是失败的执行批处理中第一个事务的日志序列号。|  
|**command_id**|**int**|失败的执行批处理的命令 ID。 仅由分发代理使用，是执行失败的批次中的第一个命令的 ID。|  
|**session_id**|**int**|发生了错误的代理会话的 ID。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_helpsubscriptionerrors**与快照和事务复制一起使用。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_helpsubscriptionerrors**。  
  
## <a name="see-also"></a>另请参阅  
 [sp_helpsubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [sp_helpsubscription_properties (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
