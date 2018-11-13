---
title: sp_setreplfailovermode (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_setreplfailovermode
- sp_setreplfailovermode_TSQL
helpviewer_keywords:
- sp_setreplfailovermode
ms.assetid: ca98a4c3-bea4-4130-88d7-79e0fd1e85f6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 97254571aaa19acb71928424a20ec9ffb741ee02
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47772935"
---
# <a name="spsetreplfailovermode-transact-sql"></a>sp_setreplfailovermode (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  允许为启用了以排队更新为故障转移的立即更新的订阅设置故障转移操作模式。 此存储过程在订阅服务器的订阅数据库中执行。 有关故障转移模式的详细信息，请参阅[事务复制的可更新订阅](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_setreplfailovermode [ @publisher= ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db' ]  
    [ , [ @publication= ] 'publication' ]  
    [ , [ @failover_mode= ] 'failover_mode' ]  
    [ , [ @override = ] override ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publisher=**] **'***publisher***'**  
 发布的名称。 *发布*是**sysname**，无默认值。 该发布必须已存在。  
  
 [  **@publisher_db =**] **'***publisher_db***’**  
 发布数据库的名称。 *publisher_db*是**sysname**，无默认值。  
  
 [ **@publication=**] **'***publication***'**  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
 [**@failover_mode=**] **'***failover_mode***’**  
 订阅的故障转移模式。 *failover_mode*是**nvarchar(10)** 可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**立即**或**同步**|订阅服务器上的数据修改将被大容量复制到发布服务器。|  
|**排入队列**|数据修改存储在[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]队列。|  
  
> [!NOTE]  
>  不再推荐使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 消息队列，也不再为其提供支持。  
  
 [ **@override**=]*重写*  
 仅限内部使用。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_setreplfailovermode**用于快照复制或事务复制的订阅已启用，要么排队更新，且故障转移到立即更新，或使用故障转移的立即更新排队正在更新。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_setreplfailovermode**。  
  
## <a name="see-also"></a>请参阅  
 [切换可更新事务性订阅的更新模式](../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
