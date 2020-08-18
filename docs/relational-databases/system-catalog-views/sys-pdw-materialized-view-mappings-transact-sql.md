---
description: 'sys. pdw_materialized_view_mappings (Transact-sql) '
title: sys. pdw_materialized_view_mappings (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d62b0e25-3226-4f87-a10a-b3a0d9555e19
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 0ee83b26439397066806c50ba6e3056042f628a9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460590"
---
# <a name="syspdw_materialized_view_mappings-transact-sql"></a>sys. pdw_materialized_view_mappings (Transact-sql)   

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

通过 object_id 将具体化视图与内部对象名称进行绑定。

Physical_name 和 object_id 的列构成此目录视图的键。
  
|列名|数据类型|说明|  
|-----------------|---------------|-----------------|  
|physical_name |**nvarchar (36) **|具体化视图的物理名称。|  
|object_id  |**int**|具体化视图的对象 ID。 请参阅 [sys.databases (transact-sql) ](/sql/relational-databases/system-catalog-views/sys-objects-transact-sql?view=azure-sqldw-latest)。| 

## <a name="permissions"></a>权限

要求拥有 VIEW DATABASE STATE 权限。
  
## <a name="see-also"></a>另请参阅

[利用具体化视图进行性能优化](/azure/sql-data-warehouse/performance-tuning-materialized-views)   
[CREATE MATERIALIZED VIEW AS SELECT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-materialized-view-as-select-transact-sql?view=azure-sqldw-latest)   
[ALTER MATERIALIZED VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-materialized-view-transact-sql?view=azure-sqldw-latest)   
[说明 &#40;Transact-sql&#41;](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_column_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-column-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql?view=azure-sqldw-latest)   
[SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Azure SQL 数据仓库支持的系统视图](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Azure SQL 数据仓库支持的 T-SQL 语句](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements) 
