---
title: 列 (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- COLUMNS
- COLUMNS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- COLUMNS view
- INFORMATION_SCHEMA.COLUMNS view
ms.assetid: bbf7ac4a-7444-4351-a590-a9f71e0bc495
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f6a14751ea8a0b268c846935e5058c10d79b4d60
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54131777"
---
# <a name="columns-transact-sql"></a>COLUMNS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  为当前数据库中当前用户可访问的每一列返回一行。  
  
 若要从这些视图检索信息，请指定完全限定的名称**INFORMATION_SCHEMA**_.view_name_。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar(** 128 **)**|表限定符。|  
|**TABLE_SCHEMA**|**nvarchar(** 128 **)**|包含该表的架构的名称。<br /><br /> **&#42;&#42;重要&#42; &#42;** 请勿使用 INFORMATION_SCHEMA 视图来确定对象的架构。 查找对象架构的唯一可靠方法是查询 sys.objects 目录视图。|  
|**TABLE_NAME**|**nvarchar(** 128 **)**|表名。|  
|**COLUMN_NAME**|**nvarchar(** 128 **)**|列名称。|  
|**ORDINAL_POSITION**|**int**|列标识号。|  
|**COLUMN_DEFAULT**|**nvarchar (** 4000 **)**|列的默认值。|  
|**IS_NULLABLE**|**varchar (** 3 **)**|列的为空性。 如果列允许 NULL，则该列将返回 YES。 否则，返回 NO。|  
|**DATA_TYPE**|**nvarchar(** 128 **)**|系统提供的数据类型。|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|二进制数据、字符数据或文本和图像数据的最大长度（字符）。<br /><br /> -1，表示**xml**和大值类型数据。 否则，返回 NULL。 有关详细信息，请参阅[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)。|  
|**CHARACTER_OCTET_LENGTH**|**int**|二进制数据、字符数据或文本和图像数据的最大长度（字节）。<br /><br /> -1，表示**xml**和大值类型数据。 否则，返回 NULL。|  
|**NUMERIC_PRECISION**|**tinyint**|近似数字数据、精确数字数据、整数数据或货币数据的精度。 否则，返回 NULL。|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|近似数字数据、精确数字数据、整数数据或货币数据的精度基数。 否则，返回 NULL。|  
|**NUMERIC_SCALE**|**int**|近似数字数据、精确数字数据、整数数据或货币数据的小数位数。 否则，返回 NULL。|  
|**DATETIME_PRECISION**|**smallint**|子类型代码**datetime**和 ISO**间隔**数据类型。 对于其他数据类型，返回 NULL。|  
|**CHARACTER_SET_CATALOG**|**nvarchar(** 128 **)**|返回**主**。 如果列为字符数据，这指示字符集所在的数据库或**文本**数据类型。 否则，返回 NULL。|  
|**CHARACTER_SET_SCHEMA**|**nvarchar(** 128 **)**|始终返回 NULL。|  
|**CHARACTER_SET_NAME**|**nvarchar(** 128 **)**|返回将如果此列为字符数据的字符集的唯一名称或**文本**数据类型。 否则，返回 NULL。|  
|**COLLATION_CATALOG**|**nvarchar(** 128 **)**|始终返回 NULL。|  
|**COLLATION_SCHEMA**|**nvarchar(** 128 **)**|始终返回 NULL。|  
|**COLLATION_NAME**|**nvarchar(** 128 **)**|如果列为字符数据，则返回排序规则的唯一名称或**文本**数据类型。 否则，返回 NULL。|  
|**DOMAIN_CATALOG**|**nvarchar(** 128 **)**|如果此列是别名数据类型，则此列是在其中创建用户定义数据类型的数据库的名称。 否则，返回 NULL。|  
|**DOMAIN_SCHEMA**|**nvarchar(** 128 **)**|如果列是用户定义数据类型，则此列将返回该用户定义数据类型的架构名称。 否则，返回 NULL。<br /><br /> **&#42;&#42;重要&#42; &#42;** 请勿使用 INFORMATION_SCHEMA 视图来确定数据类型的架构。 查找类型的架构的唯一可靠方式是使用 TYPEPROPERTY 函数。|  
|**DOMAIN_NAME**|**nvarchar(** 128 **)**|如果列是用户定义数据类型，则此列是该用户定义数据类型的名称。 否则，返回 NULL。|  
  
## <a name="remarks"></a>备注  
 **ORDINAL_POSITION**列**INFORMATION_SCHEMA。列**视图不是与 COLUMNS_UPDATED 函数返回的列的位模式兼容。 若要获取与 COLUMNS_UPDATED 兼容的位模式，必须引用**ColumnID**属性的 COLUMNPROPERTY 系统函数查询时**INFORMATION_SCHEMA。列**视图。 例如：  
  
```  
USE AdventureWorks2012;  
GO  
SELECT TABLE_NAME, COLUMN_NAME, COLUMNPROPERTY(OBJECT_ID(TABLE_SCHEMA + '.' + TABLE_NAME), COLUMN_NAME, 'ColumnID') AS COLUMN_ID  
FROM AdventureWorks2012.INFORMATION_SCHEMA.COLUMNS  
WHERE TABLE_NAME = 'Person';  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [系统视图&#40;Transact SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [信息架构视图&#40;Transact SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.syscharsets &#40;Transact SQL&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)   
 [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.sql_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.configurations (Transact-SQL)](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [sys.objects (Transact-SQL)](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.types (Transact-SQL)](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)   
 [COLUMNS_UPDATED &#40;Transact SQL&#41;](../../t-sql/functions/columns-updated-transact-sql.md)  
  
  
