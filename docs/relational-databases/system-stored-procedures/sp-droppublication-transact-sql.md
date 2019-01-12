---
title: sp_droppublication (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_droppublication_TSQL
- sp_droppublication
helpviewer_keywords:
- sp_droppublication
ms.assetid: b52b37e6-4fec-40cf-abba-7dce4ff395fd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a05845955116454ae23b2cd97e25250dbb1e6331
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54124087"
---
# <a name="spdroppublication-transact-sql"></a>sp_droppublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除发布及其关联的快照代理。 删除发布之前必须删除全部的订阅。 发布中的项目将自动删除。 在发布服务器上对发布数据库执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_droppublication [ @publication= ] 'publication'   
    [ , [ @ignore_distributor = ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@publication=** ] **'**_发布_  
 要删除的发布的名称。 *发布*是**sysname**，无默认值。 如果**所有**指定，则将从发布数据库，除了那些具有订阅中删除所有发布。  
  
 [ **@ignore_distributor =** ] *ignore_distributor*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_droppublication**快照复制和事务复制中使用。  
  
 **sp_droppublication**以递归方式删除与发布关联的所有项目，然后都删除发布本身。 如果发布包含一个或更多对它的订阅，则不能删除。 有关如何删除订阅的信息，请参阅[Delete a Push Subscription](../../relational-databases/replication/delete-a-push-subscription.md)并[Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md)。  
  
 执行**sp_droppublication**将删除发布不会删除已发布的对象从发布数据库或订阅数据库中的相应对象。 使用 DROP\<对象 > 手动删除这些对象，如有必要。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_droppublication**。  
  
## <a name="examples"></a>示例  
 [!code-sql[HowTo#sp_droppublication](../../relational-databases/replication/codesnippet/tsql/sp-droppublication-trans_1.sql)]  
  
## <a name="see-also"></a>请参阅  
 [删除发布](../../relational-databases/replication/publish/delete-a-publication.md)   
 [sp_addpublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_helppublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
