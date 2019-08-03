---
title: sp_dropsubscriber (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropsubscriber_TSQL
- sp_dropsubscriber
helpviewer_keywords:
- sp_dropsubscriber
ms.assetid: 8c6eb282-81b5-4ec4-b691-aa061d9267dc
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9bef68803beedbfdb0d6034b2a92665f033d9641
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768287"
---
# <a name="spdropsubscriber-transact-sql"></a>sp_dropsubscriber (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  从注册的服务器中删除订阅服务器名称。 此存储过程在发布服务器上对发布数据库执行。  
  
> [!IMPORTANT]  
>  已不推荐使用此存储过程。 你不再需要在发布服务器上显式注册订阅服务器。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_dropsubscriber [ @subscriber= ] 'subscriber'   
    [ , [ @reserved= ] 'reserved' ]   
    [ , [ @ignore_distributor = ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>参数  
`[ @subscriber = ] 'subscriber'`要删除的订阅服务器的名称。 *订阅服务器*的**sysname**, 无默认值。  
  
`[ @reserved = ] 'reserved'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @ignore_distributor = ] ignore_distributor` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>返回代码值  
 **0** (成功) 或**1** (失败)  
  
## <a name="remarks"></a>备注  
 **sp_dropsubscriber**用于所有类型的复制。  
  
 此存储过程将删除服务器**子项**选项, 并删除系统管理员到**repl_subscriber**的远程登录映射。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员才能执行**sp_dropsubscriber**。  
  
## <a name="see-also"></a>请参阅  
 [删除推送订阅](../../relational-databases/replication/delete-a-push-subscription.md)   
 [删除请求订阅](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [sp_addsubscriber &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [sp_changesubscriber &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_helpdistributor (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helpsubscriberinfo (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
