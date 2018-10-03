---
title: syspolicy_policy_category_subscriptions (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syspolicy_policy_category_subscriptions_TSQL
- syspolicy_policy_category_subscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policy_group_subscriptions view
ms.assetid: b3b3a7d7-0b78-46c0-9755-045f7a5692b9
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 845b665c108c2d91ef5876667e71a5c883ec8e80
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47735001"
---
# <a name="syspolicypolicycategorysubscriptions-transact-sql"></a>syspolicy_policy_category_subscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中每个基于策略的管理订阅在表中各占一行。 每行描述目标和策略的类别对。 下表介绍了 syspolicy_policy_group_subscriptions 视图中的列。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|policy_category_subscription_id|**int**|此记录的标识符。|  
|target_type|**sysname**|作为此订阅目标的数据库对象的类型。|  
|target_object|**sysname**|目标对象的名称。|  
|policy_category_id|**int**|应用于目标的策略类别的 ID。|  
  
## <a name="remarks"></a>备注  
 此视图显示订阅了策略类别的目标。  
  
## <a name="permissions"></a>Permissions  
 要求具有 msdb 数据库中 PolicyAdministratorRole 角色的成员身份。  
  
## <a name="see-also"></a>请参阅  
 [使用基于策略的管理来管理服务器](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [基于策略的管理视图 (Transact-SQL)](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
