---
title: sp_droppullsubscription （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_droppullsubscription
- sp_droppullsubscription_TSQL
helpviewer_keywords:
- sp_droppullsubscription
ms.assetid: 7352d94a-f8f2-42ea-aaf1-d08c3b5a0e76
author: stevestein
ms.author: sstein
ms.openlocfilehash: f4ad522c13987f7617def29d5ff112a5a26db8b9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68771452"
---
# <a name="sp_droppullsubscription-transact-sql"></a>sp_droppullsubscription (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  在订阅服务器的当前数据库中删除订阅。 此存储过程在订阅服务器上对请求订阅数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_droppullsubscription [ @publisher= ] 'publisher'  
        , [ @publisher_db= ] 'publisher_db'  
        , [ @publication= ] 'publication'  
    [ , [ @reserved= ] reserved ]  
```  
  
## <a name="arguments"></a>参数  
`[ @publisher = ] 'publisher'`远程服务器名称。 *发布服务器*的**sysname**，无默认值。 如果为**all**，则删除所有发布服务器上的订阅。  
  
`[ @publisher_db = ] 'publisher_db'`发布服务器数据库的名称。 *publisher_db* **sysname**，无默认值。 **all**表示所有发布服务器数据库。  
  
`[ @publication = ] 'publication'`发布名称。 *发布*为**sysname**，无默认值。 如果为**all**，则将订阅删除到所有发布。  
  
`[ @reserved = ] reserved` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_droppullsubscription**用于快照复制和事务复制。  
  
 **sp_droppullsubscription**将[MSreplication_subscriptions &#40;transact-sql&#41;](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md)表中删除相应的行，并在订阅服务器上删除相应的分发服务器代理。 如果[MSreplication_subscriptions &#40;transact-sql&#41;](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md)中没有剩余的行，则将删除该表。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_droptranpullsubscription](../../relational-databases/replication/codesnippet/tsql/sp-droppullsubscription-_1.sql)]  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员或创建请求订阅的用户才能**sp_droppullsubscription**执行。 只有创建请求订阅的用户属于此角色时， **db_owner**固定数据库角色才能执行**sp_droppullsubscription** 。  
  
## <a name="see-also"></a>另请参阅  
 [删除请求订阅](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [sp_addpullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_change_subscription_properties &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [sp_helppullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)  
  
  
