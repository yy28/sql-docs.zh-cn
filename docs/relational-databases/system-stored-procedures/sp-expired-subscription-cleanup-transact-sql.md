---
title: sp_expired_subscription_cleanup （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f739a51e57337628c666ac8e5ccee253785a1df6
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82820493"
---
# <a name="sp_expired_subscription_cleanup-transact-sql"></a>sp_expired_subscription_cleanup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  检查每个发布的所有订阅的状态并删除过期的订阅。 此存储过程在发布服务器上对任何数据库执行，或者在分发服务器的分发数据库上对非发布服务器执行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_expired_subscription_cleanup [ [ @publisher = ] 'publisher' ]   
```  
  
## <a name="arguments"></a>参数  
`[ @publisher = ] 'publisher'`非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器的名称。 *发布*为**sysname**，默认值为 NULL。 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器，无需指定此参数。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_expired_subscription_cleanup**在所有类型的复制中使用。  
  
 **sp_expired_subscription_cleanup**由 "过期的订阅清除" 作业执行，每24小时检测并删除发布数据库中的过期订阅。 如果有任何订阅过期，也就是说，在保持期内未与发布服务器保持同步，则声明发布已过期并在发布服务器上清除该订阅的跟踪。 有关详细信息，请参阅 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员或**db_owner**固定数据库角色的成员才能执行**sp_expired_subscription_cleanup**。  
  
## <a name="see-also"></a>另请参阅  
 [sp_mergesubscription_cleanup &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md)   
 [sp_subscription_cleanup &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
