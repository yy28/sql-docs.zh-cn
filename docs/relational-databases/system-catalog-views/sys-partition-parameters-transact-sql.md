---
title: sys.partition_parameters (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- partition_parameters_TSQL
- partition_parameters
- sys.partition_parameters_TSQL
- sys.partition_parameters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.partition_parameters catalog view
ms.assetid: 2012ed9d-3ea3-4c29-9b78-dfa54a392dce
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 32fe257f14c1e085a43b4150ee933888a83d5d14
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125343"
---
# <a name="syspartitionparameters-transact-sql"></a>sys.partition_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  每个分区函数的参数在表中对应一行。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**function_id**|**int**|此参数所属分区函数的 ID。|  
|**parameter_id**|**int**|参数的 ID。 在分区函数中是唯一的，从 1 开始。|  
|**system_type_id**|**tinyint**|参数的系统类型的 ID。 对应于**system_type_id**的列**sys.types**目录视图。|  
|**max_length**|**smallint**|参数的最大长度（字节）。|  
|**精度**|**tinyint**|如果参数是基于数值的，则表示参数的精度；否则为 0。|  
|**scale**|**tinyint**|如果参数是基于数值的，则表示参数的小数位数；否则为 0。|  
|**collation_name**|**sysname**|如果参数基于字符，则为参数的排序规则名称；否则为 NULL。|  
|**user_type_id**|**int**|类型的 ID。 在该数据库中是唯一的。 对于系统数据类型， **user_type_id** = **system_type_id**。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [分区函数目录视图&#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.partition_functions (Transact-SQL)](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [sys.partition_range_values &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)  
  
  
