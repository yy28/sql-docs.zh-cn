---
title: sp_dropmergesubscription (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
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
- sp_dropmergesubscription_TSQL
- sp_dropmergesubscription
helpviewer_keywords:
- sp_dropmergesubscription
ms.assetid: 34244ae6-bd98-4a6a-bbd3-85f50edfcdc0
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d639b189f1b271f6563c32090992c376113ccfa2
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43027210"
---
# <a name="spdropmergesubscription-transact-sql"></a>sp_dropmergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除对合并发布的订阅及其关联的合并代理。 在发布服务器上对发布数据库执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_dropmergesubscription [ [ @publication= ] 'publication' ]   
    [ , [ @subscriber= ] 'subscriber'    
    [ , [ @subscriber_db= ] 'subscriber_db' ]   
    [ , [ @subscription_type= ] 'subscription_type' ]   
    [ , [ @ignore_distributor = ] ignore_distributor ]   
    [ , [ @reserved = ] reserved ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@publication=** ] **'***发布*****  
 为发布名称。 *发布*是**sysname**，默认值为 NULL。 该发布必须已经存在，并符合标识符的相关规则。  
  
 [  **@subscriber=**] **'***订阅服务器*****  
 订阅服务器的名称。 *订阅服务器上*是**sysname**，默认值为 NULL。  
  
 [  **@subscriber_db=** ] **'***subscriber_db*****  
 是订阅数据库的名称。 *subscription_database*是**sysname**，默认值为 NULL。  
  
 [  **@subscription_type=** ] **'***subscription_type*****  
 是订阅的类型。 *subscription_type*是**nvarchar(15)**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**所有**|推送订阅、请求订阅和匿名订阅|  
|**匿名**|匿名订阅。|  
|**推送**|推送订阅。|  
|**请求**|请求订阅。|  
|**同时**（默认值）|推送订阅和请求订阅。|  
  
 [  **@ignore_distributor =** ] *ignore_distributor*  
 指示是否在未连接到分发服务器的情况下执行此存储过程。 *ignore_distributor*是**位**，默认值为**0**。 该参数可用于删除订阅，但不清除分发服务器上的任务。 在必须重新安装分发服务器的情况下，该参数也很有用。  
  
 [  **@reserved=** ]*保留*  
 供将来使用的保留参数。 *保留*是**位**，默认值为**0**。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>Remarks  
 **sp_dropmergesubscription**合并复制中使用。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_dropmergesubscription](../../relational-databases/replication/codesnippet/tsql/sp-dropmergesubscription_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_dropmergesubscription**。  
  
## <a name="see-also"></a>请参阅  
 [删除推送订阅](../../relational-databases/replication/delete-a-push-subscription.md)   
 [删除请求订阅](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [sp_addmergesubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [sp_changemergesubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [sp_helpmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)  
  
  
