---
title: "架构 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/08/2017
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
- SCHEMATA_TSQL
- SCHEMATA
dev_langs: TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.SCHEMATA view
- SCHEMATA view
ms.assetid: 69617642-0f54-4b25-b62f-5f39c8909601
caps.latest.revision: "41"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ac71e5f401f0eb411f7356d8bc4c15fa0a57c901
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="schemata-transact-sql"></a>SCHEMATA (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  为当前数据库中的每个架构返回一行。 若要从这些视图检索信息，指定完全限定的名称**INFORMATION_SCHEMA。***view_name*。 若要检索的实例中的所有数据库有关的信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，查询[sys.databases &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目录视图。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**CATALOG_NAME**|**sysname**|当前数据库的名称|  
|**SCHEMA_NAME**|**nvarchar (**128**)**|返回架构名称。|  
|**SCHEMA_OWNER**|**nvarchar (**128**)**|架构所有者名称。<br /><br /> **\*\*重要\* \*** 并使用 INFORMATION_SCHEMA 视图来确定对象的架构。 查找对象架构的唯一可靠的方式是查询 sys.objects 目录视图。|  
|**DEFAULT_CHARACTER_SET_CATALOG**|**varchar (**6**)**|始终返回 NULL。|  
|**DEFAULT_CHARACTER_SET_SCHEMA**|**varchar (**3**)**|始终返回 NULL。|  
|**DEFAULT_CHARACTER_SET_NAME**|**sysname**|返回默认字符集的名称。|  

**示例**  
以下示例中，在 master 数据库中返回有关架构的信息：  
```sql  
SELECT * FROM master.INFORMATION_SCHEMA.SCHEMATA;
```  

## <a name="see-also"></a>另请参阅  
 [系统视图 &#40;Transact SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [信息架构视图 &#40;Transact SQL &#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.schemas &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)   
 [sys.syscharsets &#40;Transact SQL &#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)  
  
  
