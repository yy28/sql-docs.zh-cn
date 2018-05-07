---
title: syspolicy_conditions (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- syspolicy_conditions
- syspolicy_conditions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_conditions view
ms.assetid: af97d26c-4bd5-4b08-be51-8419e3b2832c
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 09d52d9a4c4d5005a51057a40c29524301d3fdd4
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="syspolicyconditions-transact-sql"></a>syspolicy_conditions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中每个基于策略的管理条件在表中各占一行。 syspolicy_conditions 属于 msdb 数据库中的 dbo 架构。 下表介绍了 syspolicy_conditions 视图中的列。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|condition_id|**int**|此条件的标识符。 每个条件表示由一个或多个条件表达式组成的集合。|  
|name|**sysname**|条件名称。|  
|date_created|**datetime**|条件的创建日期和时间。|  
|description|**nvarchar(max)**|条件说明。 说明列是可选的，可以为 NULL。|  
|created_by|**sysname**|创建条件的登录名。|  
|modified_by|**sysname**|最近修改条件的登录名。 如果从未进行修改，则为 NULL。|  
|date_modified|**datetime**|条件的创建日期和时间。 如果从未进行修改，则为 NULL。|  
|is_name_condition|**int**|指定该条件是否为命名条件。<br /><br /> 0 = 条件表达式不包含 @Name 变量。<br /><br /> 1 = 条件表达式包含 @Name 变量。|  
|方面 (facet)|**nvarchar(max)**|条件所基于的方面的名称。|  
|表达式|**nvarchar(max)**|方面状态的表达式。|  
|obj_name|**sysname**|如果条件表达式包含 @Name，则为赋给此变量的对象名。|  
  
## <a name="remarks"></a>注释  
 在排除基于策略的管理的故障时，请查询 syspolicy_conditions 视图，以确定创建条件或上次更改条件的用户。  
  
## <a name="permissions"></a>权限  
 要求具有 msdb 数据库中 PolicyAdministratorRole 角色的成员身份。  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理来管理服务器](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [基于策略的管理视图 (Transact-SQL)](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
