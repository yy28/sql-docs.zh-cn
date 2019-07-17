---
title: sp_expired_subscription_cleanup (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_expired_subscription_cleanup
- SP_EXPIRED_SUBSCRIPTION_CLEANUP_TSQL
helpviewer_keywords:
- sp_expired_subscription_cleanup
ms.assetid: 6abc29fe-d77a-4673-9d99-ae31c688012c
author: stevestein
ms.author: sstein
ms.openlocfilehash: fb556a464077092cacd7107a8c2b4b124c6db707
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124432"
---
# <a name="spexpiredsubscriptioncleanup-transact-sql"></a>sp_expired_subscription_cleanup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  检查每个发布的所有订阅的状态并删除过期的订阅。 在发布服务器上任何数据库或分发服务器上，对于非分发数据库执行此存储的过程[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_expired_subscription_cleanup [ [ @publisher = ] 'publisher' ]   
```  
  
## <a name="arguments"></a>参数  
`[ @publisher = ] 'publisher'` 是的一个非名称[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 *发布*是**sysname**，默认值为 NULL。 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器，无需指定此参数。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_expired_subscription_cleanup**用于所有类型的复制。  
  
 **sp_expired_subscription_cleanup**执行者过期订阅清除作业，以检测并每隔 24 小时从发布数据库中删除过期的订阅。 如果有任何订阅过期，也就是说，在保持期内未与发布服务器保持同步，则声明发布已过期并在发布服务器上清除该订阅的跟踪。 有关详细信息，请参阅 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_expired_subscription_cleanup**。  
  
## <a name="see-also"></a>请参阅  
 [sp_mergesubscription_cleanup &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md)   
 [sp_subscription_cleanup &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
