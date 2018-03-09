---
title: "COLUMN_DOMAIN_USAGE (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-information-schema-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COLUMN_DOMAIN_USAGE_TSQL
- COLUMN_DOMAIN_USAGE
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.COLUMN_DOMAIN_USAGE view
- COLUMN_DOMAIN_USAGE view
ms.assetid: deb20037-6a51-47ae-9f49-7601698fafaf
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 39fe828fd62ba367c607c2e7b84c6b37bb87cc65
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="columndomainusage-transact-sql"></a>COLUMN_DOMAIN_USAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  针对当前数据库中每个带有别名数据类型的列返回一行。 该信息架构视图返回当前用户对其拥有权限的对象的相关信息。  
  
 若要从这些视图检索信息，指定完全限定的名称**INFORMATION_SCHEMA。***view_name*。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**DOMAIN_CATALOG**|**nvarchar (**128**)**|包含该别名数据类型的数据库。|  
|**DOMAIN_SCHEMA**|**nvarchar (**128**)**|包含该别名数据类型的架构的名称。<br /><br /> **\*\*重要\* \*** 并使用 INFORMATION_SCHEMA 视图来确定数据类型的架构。 查找类型的架构的唯一可靠方式是使用 TYPEPROPERTY 函数。|  
|**A I N _**|**sysname**|别名数据类型。|  
|**TABLE_CATALOG**|**nvarchar (**128**)**|表限定符。|  
|**TABLE_SCHEMA**|**nvarchar (**128**)**|表所有者。<br /><br /> **\*\*重要\* \*** 并使用 INFORMATION_SCHEMA 视图来确定对象的架构。 查找对象的架构的唯一可靠方法是查询 sys.objects 目录视图。|  
|**TABLE_NAME**|**sysname**|使用别名数据类型的表。|  
|**COLUMN_NAME**|**sysname**|使用别名数据类型的列。|  
  
## <a name="see-also"></a>另请参阅  
 [系统视图 &#40;Transact SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [信息架构视图 &#40;Transact SQL &#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.objects &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.types &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
  
