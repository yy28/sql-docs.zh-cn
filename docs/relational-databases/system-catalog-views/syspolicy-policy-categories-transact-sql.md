---
title: syspolicy_policy_categories (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syspolicy_policy_categories
- syspolicy_policy_categories_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policy_groups view
ms.assetid: 65f080c7-771f-4cf6-a7a0-88882c637f8d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: af9086ba9de7d9c61bcedecd4331e7e0e77d6489
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121124"
---
# <a name="syspolicypolicycategories-transact-sql"></a>syspolicy_policy_categories (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中每个基于策略的管理策略类别在表中各占一行。 策略类别可帮助您组织策略时有很多策略。 下表介绍了 syspolicy_policy_groups 视图中的列。  
 
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|policy_category_id|**int**|策略类别的标识符。|  
|name|**sysname**|策略类别的名称。|  
|mandate_database_subscriptions|**bit**|指示是在不使用显式订阅的情况下，将策略类别应用到实例中的所有数据库 (1)；还是必须使用显式订阅，将策略类别应用到某个数据库 (0)。|  
  
## <a name="remarks"></a>备注  
 显示基于策略的管理策略组的列表。  
  
## <a name="permissions"></a>权限  
 要求具有 msdb 数据库中 PolicyAdministratorRole 角色的成员身份。  
  
## <a name="see-also"></a>请参阅  
 [使用基于策略的管理来管理服务器](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [基于策略的管理视图 (Transact-SQL)](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
