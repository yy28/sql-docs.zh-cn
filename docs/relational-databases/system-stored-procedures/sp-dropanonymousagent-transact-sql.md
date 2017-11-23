---
title: "sp_dropanonymousagent (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
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
- sp_dropanonymousagent
- sp_dropanonymousagent_TSQL
helpviewer_keywords: sp_dropanonymousagent
ms.assetid: 4cb96efa-9358-44a3-a8ee-a7e181bed089
caps.latest.revision: "25"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 53f1cf56d422f615bca142276cf94306ada58a16
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
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
 [  **@subid=**] *sub_id*  
 是一个匿名订阅的全局标识符。 *sub_id*是**uniqueidentifier**，无默认值。 此标识符可以检索订阅服务器上使用**sp_helppullsubscription**。 中的值**subid**返回的结果集的字段是此全局标识符。  
  
 [  **@type=**]*类型*  
 是一种订阅。 *类型*是**int**，无默认值。 有效值为**1**或**2**。 指定**1**，如果快照复制或事务复制使用分发代理。 指定**2**，如果合并复制使用合并代理。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_dropanonymousagent**在所有类型的复制中使用。  
  
 此存储过程只用于删除匿名订阅代理，而不能用于删除众所周知的订阅。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**db_owner**分发数据库中的固定的数据库角色可以执行**sp_dropanonymousagent**。  
  
## <a name="see-also"></a>另请参阅  
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
