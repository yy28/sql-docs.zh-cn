---
title: sys.security_policies (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
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
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b93943109267db79b1c8475eb3e1875950f9970a
ms.sourcegitcommit: 11ab8a241a6d884b113b3cf475b2b9ed61ff00e3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2019
ms.locfileid: "58161784"
---
# <a name="syssecuritypolicies-transact-sql"></a>sys.security_policies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  返回数据库中的每个安全策略的行。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|NAME|**sysname**|安全策略的名称，在数据库中是唯一的。|  
|object_id|**int**|安全策略的 ID。|  
|principal_id|**int**|注册到数据库的安全策略所有者的 ID。 如果通过架构确定所有者，则为 NULL。|  
|schema_id|**int**|对象所在架构的 ID。|  
|parent_object_id|**int**|策略所属对象的 ID。 必须为 0。|  
|type|**vachar(2)**|必须是**SP**。|  
|type_desc|**nvarchar(60)**|**SECURITY_POLICY**。|  
|create_date|**datetime**|所创建的安全策略的 UTC 日期。|  
|modify_date|**datetime**|最近一次修改的安全策略的 UTC 日期。|  
|is_ms_shipped|**bit**|始终为 false。|  
|is_enabled|**bit**|安全策略规范状态：<br /><br /> 0 = 已禁用<br /><br /> 1 = 已启用|  
|is_not_for_replication|**bit**|策略是使用 NOT FOR REPLICATION 选项创建的。|  
|uses_database_collation|**bit**|使用与数据库相同的排序规则。|  
|is_schemabinding_enabled|**bit**|架构绑定的安全策略的状态：<br /><br /> 0 或 NULL = 已启用<br /><br /> 1 = 已禁用|  
  
## <a name="permissions"></a>权限  
 具有主体**ALTER ANY SECURITY POLICY**权限有权访问此目录视图以及与任何人中的所有对象**VIEW DEFINITION**对象上。  
  
## <a name="see-also"></a>请参阅  
 [行级安全性](../../relational-databases/security/row-level-security.md)   
 [sys.security_predicates (Transact-SQL)](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)   
 [CREATE SECURITY POLICY (Transact-SQL)](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [安全性目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
