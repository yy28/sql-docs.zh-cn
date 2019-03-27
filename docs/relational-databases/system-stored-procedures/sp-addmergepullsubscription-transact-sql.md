---
title: sp_addmergepullsubscription (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepullsubscription_TSQL
- sp_addmergepullsubscription
helpviewer_keywords:
- sp_addmergepullsubscription
ms.assetid: d63909a0-8ea7-4734-9ce8-8204d936a3e4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 59e639c1dd319d7db074d692d3776105abe89f0f
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58493739"
---
# <a name="spaddmergepullsubscription-transact-sql"></a>sp_addmergepullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  添加对合并发布的请求订阅。 此存储过程在订阅服务器的订阅数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addmergepullsubscription [ @publication= ] 'publication'   
    [ , [ @publisher= ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @subscriber_type= ] 'subscriber_type' ]   
    [ , [ @subscription_priority= ] subscription_priority ]   
    [ , [ @sync_type= ] 'sync_type' ]   
    [ , [ @description= ] 'description' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @publication = ] 'publication'` 是发布的名称。 *发布*是**sysname**，无默认值。  
  
`[ @publisher = ] 'publisher'` 是发布服务器的名称。 *发布服务器*是**sysname**，默认值为本地服务器名称。 发布服务器必须为有效服务器。  
  
`[ @publisher_db = ] 'publisher_db'` 是发布服务器数据库的名称。 *publisher_db*是**sysname**，默认值为 NULL。  
  
`[ @subscriber_type = ] 'subscriber_type'` 是订阅服务器的类型。 *subscriber_type*是**nvarchar(15)**，并且可以**全局**，**本地**或**匿名**。 在[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]和更高版本，本地订阅称为客户端订阅和全局订阅称为服务器订阅。  
  
`[ @subscription_priority = ] subscription_priority` 为订阅优先级。 *subscription_priority*是**实际**，默认值为 NULL。 对于本地和匿名订阅，优先级很**0.0**。 在检测到冲突时，默认冲突解决程序将使用该优先级来选取入选方。 全局订阅服务器的订阅优先级必须低于 100，因为 100 是发布服务器的优先级。  
  
`[ @sync_type = ] 'sync_type'` 是订阅同步类型。 *sync_type* 是 **nvarchar(15)** ，默认值为 **自动**。 可以是**自动**或**none**。 如果**自动**，架构和已发布表的初始数据首先传输到订阅服务器上。 如果**none**，假定订阅服务器已包含架构和初始数据已发布的表。 始终会传输系统表和数据。  
  
> [!NOTE]  
>  我们不建议将值指定为**none**。  
  
`[ @description = ] 'description'` 为此请求订阅的简短说明。 *描述*是**nvarchar(255)**，默认值为 NULL。 此值显示在复制监视器**友好名称**列，该列可用于对受监视发布的订阅进行排序。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_addmergepullsubscription**用于合并复制。  
  
 如果使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理以同步订阅， [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)必须在订阅服务器上创建一个代理，并与发布保持同步作业运行存储的过程。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_0_1.sql)]  
  
 [!code-sql[HowTo#sp_addmergepullsub_websync_anon](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_0_2.sql)]  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_addmergepullsubscription**。  
  
## <a name="see-also"></a>请参阅  
 [创建请求订阅](../../relational-databases/replication/create-a-pull-subscription.md)   
 [订阅发布](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)   
 [sp_changemergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
