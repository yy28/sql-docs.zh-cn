---
title: sp_dropanonymousagent (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropanonymousagent
- sp_dropanonymousagent_TSQL
helpviewer_keywords:
- sp_dropanonymousagent
ms.assetid: 4cb96efa-9358-44a3-a8ee-a7e181bed089
ms.author: vanto
manager: craigg
ms.openlocfilehash: 82519f069aaa59020e2dccb760df5d2a24c9178b
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58537879"
---
# <a name="spdropanonymousagent-transact-sql"></a>sp_dropanonymousagent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从发布服务器中删除分发服务器上进行复制监视的匿名代理。 此存储过程在发布服务器的任何数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_dropanonymousagent [ @subid= ] sub_id    , [ @type= ] type  
```  
  
## <a name="arguments"></a>参数  
`[ @subid = ] sub_id` 是匿名订阅的全局标识符。 *sub_id*是**uniqueidentifier**，无默认值。 此标识符可以检索订阅服务器上使用**sp_helppullsubscription**。 中的值**subid**返回的结果集字段是该全局标识符。  
  
`[ @type = ] type` 是订阅的类型。 *类型*是**int**，无默认值。 有效的值为**1**或**2**。 指定**1**，如果快照复制或事务复制使用分发代理。 指定**2**，则合并复制使用合并代理。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_dropanonymousagent**用于所有类型的复制。  
  
 此存储过程只用于删除匿名订阅代理，而不能用于删除众所周知的订阅。  
  
## <a name="permissions"></a>权限  
 只有的成员**db_owner**分发数据库中的固定的数据库角色可以执行**sp_dropanonymousagent**。  
  
## <a name="see-also"></a>请参阅  
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
