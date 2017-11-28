---
title: "syspolicy_policy_category_subscriptions (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- syspolicy_policy_category_subscriptions_TSQL
- syspolicy_policy_category_subscriptions
dev_langs: TSQL
helpviewer_keywords: syspolicy_policy_group_subscriptions view
ms.assetid: b3b3a7d7-0b78-46c0-9755-045f7a5692b9
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a5e9ffa5b4e2c005a85966ea4ee989b1f8938d1c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="syspolicypolicycategorysubscriptions-transact-sql"></a>syspolicy_policy_category_subscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中每个基于策略的管理订阅在表中各占一行。 每个行所说明的目标和策略类别对。 下表介绍了 syspolicy_policy_group_subscriptions 视图中的列。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|policy_category_subscription_id|**int**|此记录的标识符。|  
|target_type|**sysname**|作为此订阅目标的数据库对象的类型。|  
|target_object|**sysname**|目标对象的名称。|  
|policy_category_id|**int**|应用于目标的策略类别的 ID。|  
  
## <a name="remarks"></a>注释  
 此视图显示订阅了策略类别的目标。  
  
## <a name="permissions"></a>Permissions  
 要求具有 msdb 数据库中 PolicyAdministratorRole 角色的成员身份。  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理来管理服务器](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [基于策略的管理视图 (Transact-SQL)](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
