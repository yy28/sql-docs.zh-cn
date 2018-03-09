---
title: "域 (Transact SQL) |Microsoft 文档"
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
- DOMAINS_TSQL
- DOMAINS
dev_langs:
- TSQL
helpviewer_keywords:
- DOMAINS view
- INFORMATION_SCHEMA.DOMAINS view
ms.assetid: f0b734d5-816f-4b10-a60c-615931b515c2
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2ab3416e33aa79bcb499451b5b4ffa7b50fe4efd
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="domains-transact-sql"></a>DOMAINS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  为当前数据库中可由当前用户访问的每个别名数据类型返回一行。  
  
 若要从这些视图检索信息，指定完全限定的名称**INFORMATION_SCHEMA。***view_name*。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**DOMAIN_CATALOG**|**nvarchar (**128**)**|包含该别名数据类型的数据库。|  
|**DOMAIN_SCHEMA**|**nvarchar (**128**)**|包含别名数据类型的架构名称。<br /><br /> **\*\*重要\* \*** 并使用 INFORMATION_SCHEMA 视图来确定数据类型的架构。 查找类型的架构的唯一可靠方式是使用 TYPEPROPERTY 函数。|  
|**A I N _**|**sysname**|别名数据类型。|  
|**DATA_TYPE**|**sysname**|系统提供的数据类型。|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|二进制数据、字符数据或文本和图像数据的最大长度（字符）。<br /><br /> -1 表示**xml**和大值类型数据。 否则，返回 NULL。 有关详细信息，请参阅[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)。|  
|**CHARACTER_OCTET_LENGTH**|**int**|二进制数据、字符数据或文本和图像数据的最大长度（字节）。<br /><br /> -1 表示**xml**和大值类型数据。 否则，返回 NULL。|  
|**COLLATION_CATALOG**|**varchar (**6**)**|始终返回 NULL。|  
|**COLLATION_SCHEMA**|**varchar (**3**)**|始终返回 NULL。|  
|**COLLATION_NAME**|**nvarchar (**128**)**|返回的排序顺序的唯一名称，如果列为字符数据或**文本**数据类型。 否则，返回 NULL。|  
|**CHARACTER_SET_CATALOG**|**varchar (**6**)**|返回**master**。 这表示的字符集所在的数据库，如果列为字符数据或**文本**数据类型。 否则，返回 NULL。|  
|**CHARACTER_SET_SCHEMA**|**varchar (**3**)**|始终返回 NULL。|  
|**CHARACTER_SET_NAME**|**nvarchar (**128**)**|返回将如果此列为字符数据的字符集的唯一名称或**文本**数据类型。 否则，返回 NULL。|  
|**NUMERIC_PRECISION**|**tinyint**|近似数字数据、精确数字数据、整数数据或货币数据的精度。 否则，返回 NULL。|  
|**NUMERIC_PRECISION_RADIX**|**int**|近似数字数据、精确数字数据、整数数据或货币数据的精度基数。 否则，返回 NULL。|  
|**NUMERIC_SCALE**|**tinyint**|近似数字数据、精确数字数据、整数数据或货币数据的小数位数。 否则，返回 NULL。|  
|**DATETIME_PRECISION**|**int**|子类型代码**datetime**和 ISO**间隔**数据类型。 对于其他数据类型，此列返回 NULL。|  
|**DOMAIN_DEFAULT**|**nvarchar (**4000**)**|定义的实际文本[!INCLUDE[tsql](../../includes/tsql-md.md)]语句。|  
  
## <a name="see-also"></a>另请参阅  
 [系统视图 &#40;Transact SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [信息架构视图 &#40;Transact SQL &#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.syscharsets &#40;Transact SQL &#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)   
 [sys.sql_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.configurations (Transact-SQL)](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [sys.types &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
  
