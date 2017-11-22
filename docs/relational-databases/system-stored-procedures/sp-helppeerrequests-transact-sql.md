---
title: "sp_helppeerrequests (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_helppeerrequests_TSQL
- sp_helppeerrequests
helpviewer_keywords: sp_helppeerrequests
ms.assetid: 37bd503e-46c4-47c6-996e-be7ffe636fe8
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3d2ea35c01385de46ded538c98faf701e34d3892
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sphelppeerrequests-transact-sql"></a>sp_helppeerrequests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关由对等复制拓扑，其中通过执行启动这些请求中的参与者接收到的所有状态请求信息[sp_requestpeerresponse &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)在拓扑中任何已发布的数据库。 此存储过程将对参与对等复制拓扑的发布服务器上的发布数据库执行。 有关详细信息，请参阅 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helppeerrequests [ @publication = ] 'publication'  
    [ , [ @description = ] 'description'  
```  
  
## <a name="arguments"></a>参数  
 [  **@publication** =] *发布*  
 对等拓扑中为之发送状态请求的发布名称。 *发布*是**sysname**，无默认值。  
  
 [  **@description** =] *说明*  
 可以用于标识各个状态请求可用于筛选返回的响应的值根据定义的用户信息时调用提供[sp_requestpeerresponse &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md). *说明*是**nvarchar （4000)**，默认值为 **%** 。 默认情况下，返回发布的所有状态请求。 使用此参数用于匹配中提供的值的说明返回仅状态请求*说明*，其中匹配使用的字符字符串[如 &#40;Transact SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)子句。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|标识一个请求。|  
|**发布**|**sysname**|为之发送状态请求的发布的名称。|  
|**sent_date**|**datetime**|发送状态请求的日期和时间。|  
|**说明**|**nvarchar(4000)**|可用于标识各个状态请求的用户定义的信息。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_helppeerrequests**用于对等事务复制中。  
  
 **sp_helppeerrequests**时还原数据库发布的对等拓扑中使用。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_helppeerrequests**。  
  
## <a name="see-also"></a>另请参阅  
 [sp_deletepeerrequesthistory &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerresponses &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)  
  
  
