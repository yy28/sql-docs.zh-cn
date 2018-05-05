---
title: sp_replmonitorsubscriptionpendingcmds (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
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
- sp_replmonitorsubscriptionpendingcmds_TSQL
- sp_replmonitorsubscriptionpendingcmds
helpviewer_keywords:
- sp_replmonitorsubscriptionpendingcmds
ms.assetid: df5b955a-feb0-4863-9b3b-7f71e9653b3d
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: c94d01031094e03ddde2fc9bcdf234729ecd11c9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spreplmonitorsubscriptionpendingcmds-transact-sql"></a>sp_replmonitorsubscriptionpendingcmds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关对事务发布的订阅的等待命令数以及处理这些命令的粗略估计时间的信息。 此存储过程针对每个返回的订阅返回一行。 在分发服务器的分发数据库上执行此存储过程，用于监视复制。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_replmonitorsubscriptionpendingcmds [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @subscriber = ] 'subscriber'  
        , [ @subscriber_db = ] 'subscriber_db'   
        , [ @subscription_type = ] subscription_type  
```  
  
## <a name="arguments"></a>参数  
 [ **@publisher** = ] **'***publisher***'**  
 发布服务器的名称。 *发布服务器*是**sysname**，无默认值。  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 已发布数据库的名称。 *publisher_db*是**sysname**，无默认值。  
  
 [ **@publication** = ] **'***publication***'**  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
 [ **@subscriber** = ] **'***subscriber***'**  
 订阅服务器的名称。 *订阅服务器*是**sysname**，无默认值。  
  
 [ **@subscriber_db** = ] **'***subscriber_db***'**  
 是订阅数据库的名称。 *subscriber_db*是**sysname**，无默认值。  
  
 [ **@subscription_type** =] *subscription_type*  
 订阅的类型。 *publication_type*是**int**，无默认值并且可为这些值之一。  
  
|“值”|说明|  
|-----------|-----------------|  
|**0**|推送订阅|  
|**1**|请求订阅|  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**pendingcmdcount**|**int**|等待订阅的命令数。|  
|**estimatedprocesstime**|**int**|将所有等待的命令传递到订阅服务器所需的估计秒数。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_replmonitorsubscriptionpendingcmds**与事务复制一起使用。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色在分发服务器或成员的**db_owner**分发数据库中的固定的数据库角色可以执行**sp_replmonitorsubscriptionpendingcmds**。 使用分发数据库的发布可以执行的发布访问的成员列出**sp_replmonitorsubscriptionpendingcmds**返回挂起命令为该发布。  
  
## <a name="see-also"></a>另请参阅  
 [以编程方式监视复制](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
