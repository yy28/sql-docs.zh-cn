---
title: 参数 (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-information-schema-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PARAMETERS_TSQL
- PARAMETERS
dev_langs:
- TSQL
helpviewer_keywords:
- PARAMETERS view
- INFORMATION_SCHEMA.PARAMETERS view
ms.assetid: 06ded0ca-7d21-4400-864a-b801e855b257
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 71aaf16dd45c0bc5efb6a2741f554b346abf4905
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="parameters-transact-sql"></a>PARAMETERS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  对于当前用户在当前数据库中可以访问的用户定义函数或存储过程的每个参数，相应地返回一行。 对于函数，该视图还会返回一行返回值信息。  
  
 若要从这些视图检索信息，指定完全限定的名称 **INFORMATION_SCHEMA。 * * * view_name*。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**SPECIFIC_CATALOG**|**nvarchar(** 128 **)**|以此为参数的例程的目录名称。|  
|**SPECIFIC_SCHEMA**|**nvarchar(** 128 **)**|以此为参数的例程的架构名称。<br /><br /> **\*\* 重要\* \*** 并使用 INFORMATION_SCHEMA 视图来确定对象的架构。 查找对象的架构的唯一可靠方法是查询 sys.objects 目录视图。|  
|**SPECIFIC_NAME**|**nvarchar(** 128 **)**|以此为参数的例程的名称。|  
|**ORDINAL_POSITION**|**int**|参数的序号位置从 1 开始。 对于函数的返回值，则为 0。|  
|**PARAMETER_MODE**|**nvarchar (** 10 **)**|如果是输入参数，则返回 IN；如果是输出参数，则返回 OUT；如果是输入/输出参数，则返回 INOUT。|  
|**IS_RESULT**|**nvarchar (** 10 **)**|如果指示作为函数的例程的结果，则返回 YES。 否则，返回 no。|  
|**AS_LOCATOR**|**nvarchar (** 10 **)**|如果声明为定位器，则返回 YES。 否则，返回 no。|  
|**PARAMETER_NAME**|**nvarchar(** 128 **)**|参数的名称。 如果该名称对应于函数的返回值，则为 NULL。|  
|**DATA_TYPE**|**nvarchar(** 128 **)**|系统提供的数据类型。|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|二进制或字符数据类型的最大长度（字符）。<br /><br /> -1 表示**xml**和大值类型数据。 否则，返回 NULL。|  
|**CHARACTER_OCTET_LENGTH**|**int**|二进制或字符数据类型的最大长度（字节）。<br /><br /> -1 表示**xml**和大值类型数据。 否则，返回 NULL。|  
|**COLLATION_CATALOG**|**nvarchar(** 128 **)**|始终返回 NULL。|  
|**COLLATION_SCHEMA**|**nvarchar(** 128 **)**|始终返回 NULL。|  
|**COLLATION_NAME**|**nvarchar(** 128 **)**|参数排序规则的名称。 如果不是一种字符类型，则返回 NULL。|  
|**CHARACTER_SET_CATALOG**|**nvarchar(** 128 **)**|编录的参数的字符集的名称。 如果不是一种字符类型，则返回 NULL。|  
|**CHARACTER_SET_SCHEMA**|**nvarchar(** 128 **)**|始终返回 NULL。|  
|**CHARACTER_SET_NAME**|**nvarchar(** 128 **)**|参数字符集的名称。 如果不是一种字符类型，则返回 NULL。|  
|**NUMERIC_PRECISION**|**tinyint**|近似数字数据、精确数字数据、整数数据或货币数据的精度。 否则，返回 NULL。|  
|**NUMERIC_PRECISION_RADIX**|**int**|近似数字数据、精确数字数据、整数数据或货币数据的精度基数。 否则，返回 NULL。|  
|**NUMERIC_SCALE**|**tinyint**|近似数字数据、精确数字数据、整数数据或货币数据的小数位数。 否则，返回 NULL。|  
|**DATETIME_PRECISION**|**int**|参数类型是否为小数秒数精度**datetime**或**smalldatetime**。 否则，返回 NULL。|  
|**INTERVAL_TYPE**|**nvarchar (** 30 **)**|NULL。 保留供将来使用。|  
|**INTERVAL_PRECISION**|**int**|NULL。 保留供将来使用。|  
|**USER_DEFINED_TYPE_CATALOG**|**nvarchar(** 128 **)**|NULL。 保留供将来使用。|  
|**USER_DEFINED_TYPE_SCHEMA**|**nvarchar(** 128 **)**|NULL。 保留供将来使用。|  
|**USER_DEFINED_TYPE_NAME**|**nvarchar(** 128 **)**|NULL。 保留供将来使用。|  
|**SCOPE_CATALOG**|**nvarchar(** 128 **)**|NULL。 保留供将来使用。|  
|**SCOPE_SCHEMA**|**nvarchar(** 128 **)**|NULL。 保留供将来使用。|  
|**SCOPE_NAME**|**nvarchar(** 128 **)**|NULL。 保留供将来使用。|  
  
## <a name="see-also"></a>另请参阅  
 [系统视图&#40;Transact SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [信息架构视图&#40;Transact SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects (Transact-SQL)](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.parameters & #40;Transact SQL & #41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)  
  
  
