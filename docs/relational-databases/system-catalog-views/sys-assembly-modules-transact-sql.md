---
title: sys.assembly_modules (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.assembly_modules
- sys.assembly_modules_TSQL
- assembly_modules
- assembly_modules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.assembly_modules catalog view
ms.assetid: 5f9e644e-8065-49a2-b53d-db7df98f70d8
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d457f00cdab5d8b7e6584c895c9a9070a1d9e395
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38062022"
---
# <a name="sysassemblymodules-transact-sql"></a>sys.assembly_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  为公共语言运行时 (CLR) 程序集所定义的每个函数、过程或触发器返回一行。 此目录视图将 CLR 存储过程、CLR 触发器或 CLR 函数映射到其基础实现。 类型为 TA、AF、PC、FS 和 FT 的对象具有相关联的程序集模块。 若要查找对象和程序集之间的关联，可以将此目录视图联接到其他目录视图。 例如，在创建 CLR 存储过程时，它表示通过中的一行**sys.objects**、 利用某个中的一行**sys.procedures** (派生自**sys.objects**)，和中的一行**sys.assembly_modules**。 中的元数据表示存储的过程本身**sys.objects**并**sys.procedures**。 对过程的基础 CLR 实现的引用中找到**sys.assembly_modules**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|SQL 对象的对象标识号。 是在数据库中唯一。|  
|**assembly_id**|**int**|创建此模块所基于的程序集的 ID。|  
|**assembly_class**|**sysname**|定义此模块的程序集中的类名。|  
|**assembly_method**|**sysname**|中的方法的名称**assembly_class**定义此模块。<br /><br /> 对于聚合函数 (AF)，该参数的值为 NULL。|  
|**null_on_null_input**|**bit**|将模块声明为针对任意 NULL 输入生成 NULL 输出。|  
|**execute_as_principal_id**|**int**|在其中执行上下文的数据库主体的 ID，该 ID 由 CLR 函数、存储过程或触发器的 EXECUTE AS 子句指定。<br /><br /> NULL = EXECUTE AS CALLER。 这是默认设置。<br /><br /> 指定的数据库主体 ID = EXECUTE AS SELF、 EXECUTE AS *user_name*，或 EXECUTE AS *login_name*。<br /><br /> -2 = EXECUTE AS OWNER。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
