---
title: sp_replqueuemonitor (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_replqueuemonitor
- sp_replqueuemonitor_TSQL
helpviewer_keywords:
- sp_replqueuemonitor
ms.assetid: 6909a3f1-43a2-4df5-a6a5-9e6f347ac841
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 438e00700e62306e28cc25fbdcb1ae62c490a2cd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47751405"
---
# <a name="spreplqueuemonitor-transact-sql"></a>sp_replqueuemonitor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出了从队列消息[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]队列或[!INCLUDE[msCoName](../../includes/msconame-md.md)]消息队列对指定发布的排队更新订阅。 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 队列，则将在订阅服务器上的订阅数据库上执行此存储过程。 如果使用消息队列，则将在分发服务器上的分发数据库上执行此存储过程。  
  
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
  
 [ **@publisherdb** =] **'***publisher_db***’** ]  
 发布数据库的名称。 *publisher_db*是**sysname**，默认值为 NULL。 NULL 表示所有发布数据库。  
  
 [ **@publication** =] **'***发布***’** ]  
 发布的名称。 *发布*是**sysname**，默认值为 NULL。 NULL 表示所有发布。   
  
 [ **@tranid** =] **'***tranid***’** ]  
 事务 id。 *tranid*是**sysname**，默认值为 NULL。 NULL 表示所有事务。  
  
 [**@queuetype=** ] **'***queuetype***’** ]  
 存储事务的队列类型。 *queuetype*是**tinyint**默认值为**0**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**0**|所有队列类型|  
|**1**|消息队列|  
|**2**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 队列|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_replqueuemonitor**快照复制或具有排队更新订阅的事务复制中使用。 不显示不包含 SQL 命令的队列消息，也不显示作为跨越式 SQL 命令的一部分的队列消息。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_replqueuemonitor**。  
  
## <a name="see-also"></a>请参阅  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
