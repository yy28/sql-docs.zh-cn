---
title: 架构 (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SCHEMATA_TSQL
- SCHEMATA
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.SCHEMATA view
- SCHEMATA view
ms.assetid: 69617642-0f54-4b25-b62f-5f39c8909601
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 16b2a23c696b4da405e4983689217abb15074f03
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078434"
---
# <a name="schemata-transact-sql"></a>SCHEMATA (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  为当前数据库中的每个架构返回一行。 若要从这些视图检索信息，请指定完全限定的名称**INFORMATION_SCHEMA。** _view_name_。 若要检索的实例中的所有数据库有关的信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，查询[sys.databases &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目录视图。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**CATALOG_NAME**|**sysname**|当前数据库的名称|  
|**SCHEMA_NAME**|**nvarchar(** 128 **)**|返回架构名称。|  
|**SCHEMA_OWNER**|**nvarchar(** 128 **)**|架构所有者名称。<br /><br /> **&#42;&#42;重要&#42; &#42;** 请勿使用 INFORMATION_SCHEMA 视图来确定对象的架构。 查找对象架构的唯一可靠的方式是查询 sys.objects 目录视图。|  
|**DEFAULT_CHARACTER_SET_CATALOG**|**varchar (** 6 **)**|始终返回 NULL。|  
|**DEFAULT_CHARACTER_SET_SCHEMA**|**varchar(** 3 **)**|始终返回 NULL。|  
|**DEFAULT_CHARACTER_SET_NAME**|**sysname**|返回默认字符集的名称。|  

**示例**  
以下示例中，在 master 数据库中返回的架构信息：  
```sql  
SELECT * FROM master.INFORMATION_SCHEMA.SCHEMATA;
```  

## <a name="see-also"></a>请参阅  
 [系统视图&#40;Transact SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [信息架构视图&#40;Transact SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.schemas (Transact-SQL)](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)   
 [sys.syscharsets &#40;Transact SQL&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)  
  
  
