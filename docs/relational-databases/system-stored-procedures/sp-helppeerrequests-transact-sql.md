---
title: sp_helppeerrequests (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppeerrequests_TSQL
- sp_helppeerrequests
helpviewer_keywords:
- sp_helppeerrequests
ms.assetid: 37bd503e-46c4-47c6-996e-be7ffe636fe8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9a51015d8c1e6e6df7f23f32fc7febf7fe9e429f
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58537159"
---
# <a name="sphelppeerrequests-transact-sql"></a>sp_helppeerrequests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回通过执行其中启动这些请求的对等复制拓扑中参与者收到的所有状态请求的信息[sp_requestpeerresponse &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)随时在拓扑中的已发布的数据库。 此存储过程将对参与对等复制拓扑的发布服务器上的发布数据库执行。 有关详细信息，请参阅 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helppeerrequests [ @publication = ] 'publication'  
    [ , [ @description = ] 'description'  
```  
  
## <a name="arguments"></a>参数  
`[ @publication = ] 'publication'` 是为其发送状态请求的对等拓扑中发布的名称。 *发布*是**sysname**，无默认值。  
  
`[ @description = ] 'description'` 可用于标识各个状态请求，它使您可以筛选返回的响应基于用户定义的信息调用时提供的值[sp_requestpeerresponse &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)。 *描述*是**nvarchar(4000)**，默认值为**%**。 默认情况下，返回发布的所有状态请求。 使用此参数仅状态请求返回匹配中提供的值的说明*描述*，其中使用匹配字符字符串[如&#40;TRANSACT-SQL&#41; ](../../t-sql/language-elements/like-transact-sql.md)子句。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|标识一个请求。|  
|**publication**|**sysname**|为之发送状态请求的发布的名称。|  
|**sent_date**|**datetime**|发送状态请求的日期和时间。|  
|**description**|**nvarchar(4000)**|可用于标识各个状态请求的用户定义的信息。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_helppeerrequests**对等事务复制中使用。  
  
 **sp_helppeerrequests**时还原发布的数据库在对等拓扑中使用。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_helppeerrequests**。  
  
## <a name="see-also"></a>请参阅  
 [sp_deletepeerrequesthistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerresponses &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)  
  
  
