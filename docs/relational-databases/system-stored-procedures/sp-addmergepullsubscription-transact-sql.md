---
title: "sp_addmergepullsubscription (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- sp_addmergepullsubscription_TSQL
- sp_addmergepullsubscription
helpviewer_keywords:
- sp_addmergepullsubscription
ms.assetid: d63909a0-8ea7-4734-9ce8-8204d936a3e4
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 64af301fda7ee871c30611698b1385fa8bd318f0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
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
 [  **@publication=**] *发布*  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@publisher=**] *发布服务器*  
 发布服务器的名称。 *发布服务器*是**sysname**，默认值为本地服务器名称。 发布服务器必须为有效服务器。  
  
 [  **@publisher_db =**] *publisher_db*  
 发布服务器数据库的名称。 *publisher_db*是**sysname**，默认值为 NULL。  
  
 [  **@subscriber_type=**] *subscriber_type*  
 订阅服务器的类型。 *subscriber_type*是**nvarchar(15)**，并且可以**全局**，**本地**或**匿名**。 在[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]和更高版本，本地订阅被称为客户端订阅和全局订阅统称为服务器订阅。  
  
 [  **@subscription_priority=**] *subscription_priority*  
 子订阅的优先级。 *subscription_priority*是**实际**，默认值为 NULL。 对于本地和匿名订阅，优先级是**0.0**。 在检测到冲突时，默认冲突解决程序将使用该优先级来选取入选方。 全局订阅服务器的订阅优先级必须低于 100，因为 100 是发布服务器的优先级。  
  
 [  **@sync_type=**] *sync_type*  
 订阅同步类型。 *sync_type*是**nvarchar(15)**，默认值为**自动**。 可以是**自动**或**无**。 如果**自动**，架构和已发布表的初始数据传输到订阅服务器第一次。 如果**无**，假定您在订阅服务器已拥有的架构和初始数据已发布表。 始终会传输系统表和数据。  
  
> [!NOTE]  
>  我们不建议指定的值**无**。  
  
 [  **@description=**] *说明*  
 对该发布订阅的简短说明。 *说明*是**nvarchar （255)**，默认值为 NULL。 此值显示在复制监视器**友好名称**列，可用于对监视发布的订阅进行排序。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_addmergepullsubscription**用于合并复制。  
  
 如果使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理以同步订阅， [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)必须在订阅服务器上创建代理和作业与发布同步，运行存储的过程。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_0_1.sql)]  
  
 [!code-sql[HowTo#sp_addmergepullsub_websync_anon](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_0_2.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_addmergepullsubscription**。  
  
## <a name="see-also"></a>另请参阅  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [订阅发布](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergepullsubscription_agent &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)   
 [sp_changemergepullsubscription &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [用 sp_dropmergepullsubscription &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
