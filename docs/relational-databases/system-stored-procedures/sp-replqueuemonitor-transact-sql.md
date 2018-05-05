---
title: sp_replqueuemonitor (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
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
- sp_replqueuemonitor
- sp_replqueuemonitor_TSQL
helpviewer_keywords:
- sp_replqueuemonitor
ms.assetid: 6909a3f1-43a2-4df5-a6a5-9e6f347ac841
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 8c1d4737d5f1502d98a58f268b58c93cf71d71ab
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spreplqueuemonitor-transact-sql"></a>sp_replqueuemonitor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出中的队列消息[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]队列或[!INCLUDE[msCoName](../../includes/msconame-md.md)]消息队列为排队更新订阅到指定的发布。 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 队列，则将在订阅服务器上的订阅数据库上执行此存储过程。 如果使用消息队列，则将在分发服务器上的分发数据库上执行此存储过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_replqueuemonitor [ @publisher = ] 'publisher'  
    [ , [ @publisherdb = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @tranid = ] 'tranid' ]  
    [ , [ @queuetype = ] 'queuetype' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publisher** = ] **'***publisher***'**  
 发布服务器的名称。 *发布服务器*是**sysname**，默认值为 NULL。 必须将该服务器配置为用于发布。 NULL 表示所有发布服务器。  
  
 [ **@publisherdb** =] *****publisher_db***** ]  
 发布数据库的名称。 *publisher_db*是**sysname**，默认值为 NULL。 NULL 表示所有发布数据库。  
  
 [ **@publication** =] *****发布***** ]  
 发布的名称。 *发布*是**sysname**，默认值为 NULL。 NULL 表示所有发布。   
  
 [ **@tranid** =] *****tranid***** ]  
 为事务 id。 *tranid*是**sysname**，默认值为 NULL。 NULL 表示所有事务。  
  
 [**@queuetype=** ] *****queuetype***** ]  
 存储事务的队列类型。 *queuetype*是**tinyint**默认值为**0**，并且可以为这些值之一。  
  
|“值”|说明|  
|-----------|-----------------|  
|**0**|所有队列类型|  
|**1**|消息队列|  
|**2**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 队列|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_replqueuemonitor**在快照复制或带有排队更新订阅的事务复制中使用。 不显示不包含 SQL 命令的队列消息，也不显示作为跨越式 SQL 命令的一部分的队列消息。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_replqueuemonitor**。  
  
## <a name="see-also"></a>另请参阅  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
