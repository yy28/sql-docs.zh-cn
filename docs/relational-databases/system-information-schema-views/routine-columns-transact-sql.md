---
title: "ROUTINE_COLUMNS (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-information-schema-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ROUTINE_COLUMNS_TSQL
- ROUTINE_COLUMNS
dev_langs: TSQL
helpviewer_keywords:
- ROUTINE_COLUMNS view
- INFORMATION_SCHEMA.ROUTINE_COLUMNS view
ms.assetid: 91dbc61b-e4c0-4826-976c-b2fce88b7793
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3815c6db044ec66bae8eddd7bceb6ad69f29db61
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="routinecolumns-transact-sql"></a>ROUTINE_COLUMNS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  为当前数据库中当前用户可访问的表值函数所返回的每一列返回一行。  
  
 若要从该视图中检索信息，请指定完全限定的名称**INFORMATION_SCHEMA。***view_name*。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar (**128**)**|表值函数的目录或数据库名称。|  
|**TABLE_SCHEMA**|**nvarchar (**128**)**|包含表值函数的架构的名称。<br /><br /> **\*\*重要\* \*** 并使用 INFORMATION_SCHEMA 视图来确定对象的架构。 查找对象的架构的唯一可靠方法是查询 sys.objects 目录视图。|  
|**TABLE_NAME**|**nvarchar (**128**)**|表值函数的名称。|  
|**COLUMN_NAME**|**nvarchar (**128**)**|列名称。|  
|**ORDINAL_POSITION**|**int**|列标识号。|  
|**COLUMN_DEFAULT**|**nvarchar (**4000**)**|列的默认值。|  
|**IS_NULLABLE**|**varchar (**3**)**|如果此列允许 NULL，则返回 YES。 否则，返回 no。|  
|**DATA_TYPE**|**nvarchar (**128**)**|系统提供的数据类型。|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|二进制数据、字符数据或文本和图像数据的最大长度（字符）。<br /><br /> -1 表示**xml**和大值类型数据。 否则，返回 NULL。 有关详细信息，请参阅[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)。|  
|**CHARACTER_OCTET_LENGTH**|**int**|二进制数据、字符数据或文本和图像数据的最大长度（字节）。<br /><br /> -1 表示**xml**和大值类型数据。 否则，返回 NULL。|  
|**NUMERIC_PRECISION**|**tinyint**|近似数字数据、精确数字数据、整数数据或货币数据的精度。 否则，返回 NULL。|  
|**NUMERIC_PRECISION_RADIX**|**int**|近似数字数据、精确数字数据、整数数据或货币数据的精度基数。 否则，返回 NULL。|  
|**NUMERIC_SCALE**|**tinyint**|近似数字数据、精确数字数据、整数数据或货币数据的小数位数。 否则，返回 NULL。|  
|**DATETIME_PRECISION**|**int**|子类型代码**datetime**和 ISO**整数**数据类型。 对于其他数据类型，则返回 NULL。|  
|**CHARACTER_SET_CATALOG**|**varchar (**6**)**|返回**master**。 这表示的字符集所在如果列为字符数据的数据库或**文本**数据类型。 否则，返回 NULL。|  
|**CHARACTER_SET_SCHEMA**|**varchar (**3**)**|始终返回 NULL。|  
|**CHARACTER_SET_NAME**|**nvarchar (**128**)**|返回将如果此列为字符数据的字符集的唯一名称或**文本**数据类型。 否则，返回 NULL。|  
|**COLLATION_CATALOG**|**varchar (**6**)**|始终返回 NULL。|  
|**COLLATION_SCHEMA**|**varchar (**3**)**|始终返回 NULL。|  
|**COLLATION_NAME**|**nvarchar (**128**)**|返回的排序顺序的唯一名称，如果列为字符数据或**文本**数据类型。 否则，返回 NULL。|  
|**DOMAIN_CATALOG**|**nvarchar (**128**)**|如果此列是别名数据类型，则此列是在其中创建用户定义数据类型的数据库的名称。 否则，返回 NULL。|  
|**DOMAIN_SCHEMA**|**nvarchar (**128**)**|如果列是架构的用户定义数据类型，此列是架构的包含用户定义数据类型的名称。 否则，返回 NULL。<br /><br /> **\*\*重要\* \*** 并使用 INFORMATION_SCHEMA 视图来确定对象的架构。 查找对象的架构的唯一可靠方法是查询 sys.objects 目录视图。|  
|**A I N _**|**nvarchar (**128**)**|如果列是用户定义数据类型，则此列是该用户定义数据类型的名称。 否则，返回 NULL。|  
  
## <a name="see-also"></a>另请参阅  
 [系统视图 &#40;Transact SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [信息架构视图 &#40;Transact SQL &#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  
