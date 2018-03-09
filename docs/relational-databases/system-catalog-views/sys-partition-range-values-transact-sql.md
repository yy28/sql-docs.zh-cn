---
title: "sys.partition_range_values (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.partition_range_values
- partition_range_values_TSQL
- partition_range_values
- sys.partition_range_values_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.partition_range_values catalog view
ms.assetid: 9aee483e-61f3-4613-bec6-f084161f45ac
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0f1fd5ab82c373dbc08edf7a901ccfee4d6eed34
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="syspartitionrangevalues-transact-sql"></a>sys.partition_range_values (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  类型为 R 的分区函数的每个范围边界值都在表中占一行。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**function_id**|**int**|该范围边界值的分区函数的 ID。|  
|**boundary_id**|**int**|边界值元组的 ID（从 1 开始的序号），最左边界以值为 1 的 ID 开始。|  
|**parameter_id**|**int**|该值所对应的函数参数的 ID。 此列中的值对应与**parameter_id**列**sys.partition_parameters**目录为任何特定的视图**function_id**。|  
|**值**|**sql_variant**|实际的边界值。|  
  
## <a name="permissions"></a>Permissions  
 要求 **公共** 角色具有成员身份。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [分区函数目录视图 &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.partition_functions &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [sys.partition_parameters &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md)  
  
  
