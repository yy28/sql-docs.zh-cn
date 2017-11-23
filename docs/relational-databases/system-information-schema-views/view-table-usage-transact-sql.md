---
title: "VIEW_TABLE_USAGE (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-information-schema-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- VIEW_TABLE_USAGE_TSQL
- VIEW_TABLE_USAGE
dev_langs: TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.VIEW_TABLE_USAGE view
- VIEW_TABLE_USAGE view
ms.assetid: 0aeefb3f-02ef-457e-8c42-84ddb26f1c88
caps.latest.revision: "36"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f7e6852b3d8deeba7fb5d91d906f651cca5842d4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="viewtableusage-transact-sql"></a>VIEW_TABLE_USAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  为视图中使用的当前数据库的每个表返回一行。 该信息架构视图返回当前用户对其拥有权限的对象的相关信息。  
  
 若要从这些视图检索信息，指定完全限定的名称**INFORMATION_SCHEMA。***view_name*。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**VIEW_CATALOG**|**nvarchar (**128**)**|视图限定符。|  
|**VIEW_SCHEMA**|**nvarchar (**128**)**|包含该视图的架构名称。<br /><br /> **\*\*重要\* \*** 并使用 INFORMATION_SCHEMA 视图来确定对象的架构。 查找对象的架构的唯一可靠方法是查询 sys.objects 目录视图。|  
|**VIEW_NAME**|**sysname**|视图名。|  
|**TABLE_CATALOG**|**nvarchar (**128**)**|表限定符。|  
|**TABLE_SCHEMA**|**nvarchar (**128**)**|包含基表的架构的名称。<br /><br /> **\*\*重要\* \*** 并使用 INFORMATION_SCHEMA 视图来确定对象的架构。 查找对象的架构的唯一可靠方法是查询 sys.objects 目录视图。|  
|**TABLE_NAME**|**sysname**|用作视图基础的基表。|  
  
## <a name="see-also"></a>另请参阅  
 [系统视图 &#40;Transact SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [信息架构视图 &#40;Transact SQL &#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.sql_dependencies &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md)   
 [sys.objects &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.views (Transact-SQL)](../../relational-databases/system-catalog-views/sys-views-transact-sql.md)  
  
  
