---
title: "sys.security_policies (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server 2016 Preview
f1_keywords:
- SYS.SECURITY_POLICIES_TSQL
- SECURITY_POLICIES_TSQL
- SYS.SECURITY_POLICIES
- SECURITY_POLICIES
dev_langs:
- TSQL
helpviewer_keywords:
- sys.security_policies catalog view
- security_policies catalog view
ms.assetid: 35362f5b-e601-4049-9e1d-c5307e823831
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9e30a903e31ce8ba7951f9756a8fd258375fb8e2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="syssecuritypolicies-transact-sql"></a>sys.security_policies (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  返回数据库中的每个安全策略的行。  
  
|列名|数据类型|说明|  
|-----------------|---------------|-----------------|  
|name|**sysname**|安全策略的名称，在数据库中是唯一的。|  
|object_id|**int**|安全策略的 ID。|  
|principal_id|**int**|注册到数据库的安全策略所有者的 ID。 如果通过架构确定所有者，则为 NULL。|  
|schema_id|**int**|对象所在架构的 ID。|  
|parent_object_id|**int**|策略所属对象的 ID。 必须为 0。|  
|类型|**vachar(2)**|必须是**SP**。|  
|type_desc|**nvarchar(60)**|**SECURITY_POLICY**。|  
|create_date|**datetime**|所创建的安全策略的 UTC 日期。|  
|modify_date|**datetime**|最近一次修改的安全策略的 UTC 日期。|  
|is_ms_shipped|**bit**|始终为 false。|  
|is_enabled|**bit**|安全策略规范状态：<br /><br /> 0 = 已禁用<br /><br /> 1 = 已启用|  
|is_not_for_replication|**bit**|策略是使用 NOT FOR REPLICATION 选项创建的。|  
|uses_database_collation|**bit**|使用与数据库相同的排序规则。|  
|is_schemabinding_enabled|**bit**|安全策略的 Schemabinding 状态：<br /><br /> 0 或 NULL = 已启用<br /><br /> 1 = 已禁用|  
  
## <a name="permissions"></a>Permissions  
 具有主体**ALTER ANY SECURITY POLICY**权限有权访问此目录视图，以及具有任何人都中的所有对象**VIEW DEFINITION**对象上。  
  
## <a name="see-also"></a>另请参阅  
 [行级安全性](../../relational-databases/security/row-level-security.md)   
 [sys.security_predicates (Transact-SQL)](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)   
 [CREATE SECURITY POLICY (Transact-SQL)](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [安全性目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
