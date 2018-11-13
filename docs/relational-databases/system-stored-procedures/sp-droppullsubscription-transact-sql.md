---
title: sp_droppullsubscription (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_droppullsubscription
- sp_droppullsubscription_TSQL
helpviewer_keywords:
- sp_droppullsubscription
ms.assetid: 7352d94a-f8f2-42ea-aaf1-d08c3b5a0e76
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 35b050798f9be9255b9ee35fdc0a8d378f03ecf5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47733759"
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
 [ **@publisher=** ] **'***发布服务器*****  
 远程服务器名。 *发布服务器*是**sysname**，无默认值。 如果**所有**，删除的订阅是在所有服务器的发布服务器。  
  
 [ **@publisher_db=** ] **'***publisher_db*****  
 发布服务器数据库的名称。 *publisher_db*是**sysname**，无默认值。 **所有**表示所有发布服务器数据库。  
  
 [  **@publication=** ] **'***发布*****  
 为发布名称。 *发布*是**sysname**，无默认值。 如果**所有**，针对所有发布删除的订阅。  
  
 [  **@reserved=** ]*保留*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_droppullsubscription**快照复制和事务复制中使用。  
  
 **sp_droppullsubscription**删除中的相应行[MSreplication_subscriptions &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md)表和订阅服务器上相应的分发服务器代理。 如果没有行也会保留在[MSreplication_subscriptions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md)，则将删除该表。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_droptranpullsubscription](../../relational-databases/replication/codesnippet/tsql/sp-droppullsubscription-_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或创建请求订阅的用户才能执行**sp_droppullsubscription**。 **Db_owner**固定的数据库角色才可以执行**sp_droppullsubscription**如果创建请求订阅的用户属于此角色。  
  
## <a name="see-also"></a>请参阅  
 [删除请求订阅](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [sp_addpullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_change_subscription_properties &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [sp_helppullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)  
  
  
