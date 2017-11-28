---
title: "sp_droppullsubscription (Transact SQL) |Microsoft 文档"
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
- sp_droppullsubscription
- sp_droppullsubscription_TSQL
helpviewer_keywords: sp_droppullsubscription
ms.assetid: 7352d94a-f8f2-42ea-aaf1-d08c3b5a0e76
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 13245c763bea2a34b6c7a95b13c046e43c3d4a31
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spdroppullsubscription-transact-sql"></a>sp_droppullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在订阅服务器的当前数据库中删除订阅。 此存储过程在订阅服务器上对请求订阅数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_droppullsubscription [ @publisher= ] 'publisher'  
        , [ @publisher_db= ] 'publisher_db'  
        , [ @publication= ] 'publication'  
    [ , [ @reserved= ] reserved ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@publisher=** ] *发布服务器*  
 远程服务器名。 *发布服务器*是**sysname**，无默认值。 如果**所有**，订阅根本删除发布服务器。  
  
 [  **@publisher_db=** ] *publisher_db*  
 发布服务器数据库的名称。 *publisher_db*是**sysname**，无默认值。 **所有**意味着所有发布服务器数据库。  
  
 [  **@publication=** ] *发布*  
 是该发布的名称。 *发布*是**sysname**，无默认值。 如果**所有**，对所有发布删除订阅。  
  
 [  **@reserved=** ]*保留*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_droppullsubscription**快照复制和事务复制中使用。  
  
 **sp_droppullsubscription**删除中的相应行[MSreplication_subscriptions &#40;Transact SQL &#41;](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md)表和订阅服务器上相应的分发服务器代理。 如果任何行都不会不保留在[MSreplication_subscriptions &#40;Transact SQL &#41;](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md)，它会删除表。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_droptranpullsubscription](../../relational-databases/replication/codesnippet/tsql/sp-droppullsubscription-_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或创建请求订阅的用户可以执行**sp_droppullsubscription**。 **Db_owner**固定的数据库角色是否只能执行**sp_droppullsubscription**如果创建请求订阅的用户属于此角色。  
  
## <a name="see-also"></a>另请参阅  
 [删除请求订阅](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [sp_addpullsubscription &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_change_subscription_properties &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [sp_helppullsubscription &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_dropsubscription &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)  
  
  
