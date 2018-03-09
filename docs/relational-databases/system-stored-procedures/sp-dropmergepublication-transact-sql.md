---
title: "sp_dropmergepublication (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_dropmergepublication
- sp_dropmergepublication_TSQL
helpviewer_keywords:
- sp_dropmergepublication
ms.assetid: 9e1cb96e-5889-4f97-88cd-f60cf313ce68
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5ec45802cc2784b46022ab061cc48f5985b7eaee
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spdropmergepublication-transact-sql"></a>sp_dropmergepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除合并发布及其关联的快照代理。 删除合并发布之前必须删除全部的订阅。 发布中的项目将自动删除。 在发布服务器的发布数据库上执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_dropmergepublication [ @publication= ] 'publication'   
    [ , [ @ignore_distributor = ] ignore_distributor ]   
    [ , [ @reserved = ] reserved ]  
    [ , [ @ignore_merge_metadata = ] ignore_merge_metadata ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@publication=**] *发布*  
 是要删除的名称。 *发布*是**sysname**，无默认值。 如果**所有**，所有现有合并发布删除以及与之关联的快照代理作业。 如果指定一个特定的值*发布*，仅该发布和其关联的快照代理作业被删除。  
  
 [  **@ignore_distributor =**] *ignore_distributor*  
 用于删除发布但不清除分发服务器上的任务。 *ignore_distributor*是**位**，默认值为**0**。 重新安装分发服务器时也将使用此参数。  
  
 [  **@reserved=**]*保留*  
 供将来使用的保留参数。 *保留*是**位**，默认值为**0**。  
  
 [  **@ignore_merge_metadata=** ] *ignore_merge_metadata*  
 仅限内部使用。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_dropmergepublication**合并复制中使用。  
  
 **sp_dropmergepublication**以递归方式将放置与发布相关联的所有项目，然后将都放置发布本身。 如果发布包含一个或更多对它的订阅，则不能删除。 有关如何删除订阅的信息，请参阅[Delete a Push Subscription](../../relational-databases/replication/delete-a-push-subscription.md)和[Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md)。  
  
 执行**sp_dropmergepublication**中删除发布不会删除已发布的对象从发布数据库或订阅数据库中的相应对象。 使用下拉\<对象 > 若要手动删除这些对象，如有必要。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_dropmergepublication](../../relational-databases/replication/codesnippet/tsql/sp-dropmergepublication-_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_dropmergepublication**。  
  
## <a name="see-also"></a>另请参阅  
 [删除发布](../../relational-databases/replication/publish/delete-a-publication.md)   
 [sp_addmergepublication &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_changemergepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_helpmergepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
