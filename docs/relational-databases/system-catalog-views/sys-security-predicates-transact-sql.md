---
title: sys.security_predicates (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server 2016 Preview
f1_keywords:
- SYS.SECURITY_PREDICATES
- SECURITY_PREDICATES
- SECURITY_PREDICATES_TSQL
- SYS.SECURITY_PREDICATES_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.security_predicates catalog view
- security_predicates catalog view
ms.assetid: c7a2f28c-98da-463d-8b8a-8e5619e2c6a6
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 539ca48e5c55485a5a4b3fdecb3044c1feae6826
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="syssecuritypredicates-transact-sql"></a>sys.security_predicates (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  返回数据库中的每个安全谓词的行。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|包含此谓词的安全策略的 ID。|  
|security_predicate_id|**int**|此安全策略内的谓词 ID。|  
|target_object_id|**int**|安全性谓词所绑定的对象的 ID。|  
|predicate_definition|**nvarchar(max)**|将用作安全性谓词的函数的完全限定名称，包括参数。 请注意，`schema.function`名称可能规范化 （即转义） 以及一致性的文本中的任何其他元素。 例如：<br /><br /> `[dbo].[fn_securitypredicate]([wing], [startTime], [endTime])`|  
|predicate_type|**int**|谓词由安全策略的类型：<br /><br /> 0 = 筛选器谓词<br /><br /> 1 = 阻止谓词|  
|predicate_type_desc|**nvarchar(60)**|谓词由安全策略的类型：<br /><br /> FILTER<br /><br /> 块|  
|操作|**int**|为谓词指定的操作的类型：<br /><br /> NULL = 所有适用的操作<br /><br /> 1 = 后插入<br /><br /> 2 = 更新后<br /><br /> 3 = 更新前<br /><br /> 4 = 之前删除|  
|operation_desc|**nvarchar(60)**|为谓词指定的操作的类型：<br /><br /> NULL<br /><br /> 后插入<br /><br /> AFTER UPDATE<br /><br /> 更新之前<br /><br /> 在删除之前|  
  
## <a name="permissions"></a>权限  
 具有主体**ALTER ANY SECURITY POLICY**权限有权访问此目录视图，以及具有任何人都中的所有对象**VIEW DEFINITION**对象上。  
  
## <a name="see-also"></a>另请参阅  
 [行级安全性](../../relational-databases/security/row-level-security.md)   
 [sys.security_policies (Transact-SQL)](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
 [CREATE SECURITY POLICY (Transact-SQL)](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [安全性目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
