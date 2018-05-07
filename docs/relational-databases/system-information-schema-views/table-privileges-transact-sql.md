---
title: TABLE_PRIVILEGES (Transact SQL) |Microsoft 文档
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
- TABLE_PRIVILEGES_TSQL
- TABLE_PRIVILEGES
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.TABLE_PRIVILEGES view
- TABLE_PRIVILEGES view
ms.assetid: 70269d26-b085-4a98-8a9f-b4742c2848bd
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 10f005190b8f1348353a09eb7cf607c13211cbe7
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="tableprivileges-transact-sql"></a>TABLE_PRIVILEGES (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  为当前数据库中每个授予当前用户的表特权或由当前用户授予的表特权返回一行。  
  
 若要从这些视图检索信息，指定完全限定的名称 **INFORMATION_SCHEMA。 * * * view_name*。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**授权者**|**nvarchar(** 128 **)**|授权者。|  
|**被授权者**|**nvarchar(** 128 **)**|被授权者。|  
|**TABLE_CATALOG**|**nvarchar(** 128 **)**|表限定符。|  
|**TABLE_SCHEMA**|**nvarchar(** 128 **)**|包含该表的架构的名称。<br /><br /> **\*\* 重要\* \*** 并使用 INFORMATION_SCHEMA 视图来确定对象的架构。 查找对象的架构的唯一可靠方法是查询 sys.objects 目录视图。|  
|**TABLE_NAME**|**sysname**|表名。|  
|**PRIVILEGE_TYPE**|**varchar (** 10 **)**|特权的类型。|  
|**IS_GRANTABLE**|**varchar (** 3 **)**|指定被授权者是否可以向其他人授予权限。|  
  
## <a name="see-also"></a>另请参阅  
 [系统视图&#40;Transact SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [信息架构视图&#40;Transact SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.objects (Transact-SQL)](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.database_permissions (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [sys.server_permissions &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)  
  
  
