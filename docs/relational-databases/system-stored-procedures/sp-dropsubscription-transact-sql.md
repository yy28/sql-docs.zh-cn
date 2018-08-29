---
title: sp_dropsubscription (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_dropsubscription
- sp_dropsubscription_TSQL
helpviewer_keywords:
- sp_dropsubscription
ms.assetid: 7551f345-5510-4684-ab53-f9057249d13a
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0dc8bba63c8b1ffef6e1c24810c9457e1e9b5242
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43029109"
---
# <a name="spdropsubscription-transact-sql"></a>sp_dropsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除对发布服务器上的特殊项目、发布或订阅集的订阅。 在发布服务器上对发布数据库执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_dropsubscription [ [ @publication= ] 'publication' ]  
    [ , [ @article= ] 'article' ]  
        , [ @subscriber= ] 'subscriber'  
    [ , [ @destination_db= ] 'destination_db' ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @reserved= ] 'reserved' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@publication=** ] **'***发布*****  
 关联的发布的名称。 *发布*是**sysname**，默认值为 NULL。 如果**所有**，则取消对指定订阅服务器的所有发布的所有订阅。 *发布*是一个必需的参数。  
  
 [  **@article=** ] **'***文章*****  
 项目的名称。 *文章*是**sysname**，默认值为 NULL。 如果**所有**，每个订阅的所有项目指定删除发布和订阅服务器。 使用**所有**的发布允许立即更新。  
  
 [  **@subscriber=** ] **' * **订阅*r*** *  
 要删除其订阅的订阅服务器名。 *订阅服务器上*是**sysname**，无默认值。 如果**所有**，所有订阅服务器的所有订阅将被都删除。  
  
 [  **@destination_db=** ] **'***destination_db*****  
 目标数据库的名称。 *destination_db*是**sysname**，默认值为 NULL。 如果为 NULL，则删除该订阅服务器中的所有订阅。  
  
 [  **@ignore_distributor =** ] *ignore_distributor*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@reserved=** ] **'***保留*****  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>Remarks  
 **sp_dropsubscription**快照和事务复制中使用。  
  
 如果删除即时同步发布中的一个项目上的订阅，则不能再对其进行重新添加，除非是删除发布中所有项目上的订阅并同时对它们进行重新添加。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_droptransubscription](../../relational-databases/replication/codesnippet/tsql/sp-dropsubscription-tran_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定服务器角色**db_owner**固定的数据库角色或创建订阅的用户才能执行**sp_dropsubscription**。  
  
## <a name="see-also"></a>请参阅  
 [删除推送订阅](../../relational-databases/replication/delete-a-push-subscription.md)   
 [sp_addsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_changesubstatus &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubstatus-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
