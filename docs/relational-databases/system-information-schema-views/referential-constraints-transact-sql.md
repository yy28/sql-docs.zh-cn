---
title: REFERENTIAL_CONSTRAINTS (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- REFERENTIAL_CONSTRAINTS
- REFERENTIAL_CONSTRAINTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.REFERENTIAL_CONSTRAINTS view
- REFERENTIAL_CONSTRAINTS view
ms.assetid: 5d358f18-0a85-4b55-af4b-98d5f4cd1020
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4eca39fc2fab5193b9dee9875a754fd224f2c1ce
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="referentialconstraints-transact-sql"></a>REFERENTIAL_CONSTRAINTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  为当前数据库中的每个 FOREIGN KEY 约束返回一行。 该信息架构视图返回当前用户对其拥有权限的对象的相关信息。  
  
 若要从这些视图检索信息，指定完全限定的名称 **INFORMATION_SCHEMA。 * * * view_name*。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**nvarchar(** 128 **)**|约束限定符。|  
|**CONSTRAINT_SCHEMA**|**nvarchar(** 128 **)**|包含该约束的架构的名称。<br /><br /> **\*\* 重要\* \*** 并使用 INFORMATION_SCHEMA 视图来确定对象的架构。 查找对象的架构的唯一可靠方法是查询 sys.objects 目录视图。|  
|**CONSTRAINT_NAME**|**sysname**|约束名称。|  
|**UNIQUE_CONSTRAINT_CATALOG**|**nvarchar(** 128 **)**|UNIQUE 约束限定符。|  
|**UNIQUE_CONSTRAINT_SCHEMA**|**nvarchar(** 128 **)**|包含 UNIQUE 约束的架构的名称。<br /><br /> **\*\* 重要\* \*** 并使用 INFORMATION_SCHEMA 视图来确定对象的架构。 查找对象的架构的唯一可靠方法是查询 sys.objects 目录视图。|  
|**UNIQUE_CONSTRAINT_NAME**|**sysname**|UNIQUE 约束。|  
|**MATCH_OPTION**|**varchar (** 7 **)**|引用约束匹配条件。 始终返回 SIMPLE。 这表示没有定义匹配。 当下列情况之一为真时，条件被视为匹配：<br /><br /> 外键列中至少有一个值为 NULL。<br /><br /> 外键列中的所有值都不是 NULL，并且主键表中有一行含有相同的键。|  
|**UPDATE_RULE**|**varchar (** 11 **)**|当 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句违反该约束所定义的引用完整性时执行的操作。 返回下列项之一： <br />NO ACTION<br />CASCADE<br />SET NULL<br />SET DEFAULT<br /><br /> 如果为该约束在 ON UPDATE 上指定了 NO ACTION，则对该约束中被引用主键的更新不会传播到外键。 如果因为至少有一个外键包含相同的值，而导致主键的更新违反了引用完整性，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将不会对父表和引用表执行任何更改。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 还将引发错误。<br /><br /> 如果为该约束在 ON UPDATE 上指定了 CASCADE，则对主键值所做的任何更改都将自动地传播到外键值。|  
|**DELETE_RULE**|**varchar (** 11 **)**|当 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句违反了该约束所定义的引用完整性时执行的操作。 返回下列项之一： <br />NO ACTION<br />CASCADE<br />SET NULL<br />SET DEFAULT<br /><br /> 如果为该约束在 ON DELETE 上定义了 NO ACTION，则对该约束中被引用主键所做的删除将不会传播到外键。 如果因为至少有一个外键包含相同的值而导致主键的删除违反了引用完整性，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将不会对父表和引用表执行任何更改。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 还将引发错误。<br /><br /> 如果为该约束在 ON DELETE 上指定了 CASCADE，则对主键值所做的任何更改都将自动传播到外键值。|  
  
## <a name="see-also"></a>另请参阅  
 [系统视图&#40;Transact SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [信息架构视图&#40;Transact SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.objects (Transact-SQL)](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.foreign_keys &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md)  
  
  
