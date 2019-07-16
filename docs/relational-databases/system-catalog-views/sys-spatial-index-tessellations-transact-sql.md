---
title: sys.spatial_index_tessellations (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- spatial_index_tessellations
- sys.spatial_index_tessellations_TSQL
- spatial_index_tessellations_TSQL
- sys.spatial_index_tessellations
dev_langs:
- TSQL
helpviewer_keywords:
- sys.spatial_index_tessellations catalog view
ms.assetid: 8b17a9a4-b57f-4220-8138-fc73581b1670
author: stevestein
ms.author: sstein
ms.openlocfilehash: c4f2f4b8ea0184d063a6423f27fdf2cf9c450a05
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078652"
---
# <a name="sysspatialindextessellations-transact-sql"></a>sys.spatial_index_tessellations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

 表示每个空间索引的分割方案和参数的相关信息。  
  
> [!NOTE]  
>  有关分割的信息，请参阅[空间索引概述](../../relational-databases/spatial/spatial-indexes-overview.md)。  
  

|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|object_id|**int**|定义了索引的对象的 ID。 每个 （object_id，index_id） 对具有一个对应的条目[sys.spatial_indexes](../../relational-databases/system-catalog-views/sys-spatial-indexes-transact-sql.md)。|  
|index_id|**int**|定义了索引列的空间索引的 ID。|  
|tessellation_scheme|**sysname**|分割方案，其中一个的名称：GEOMETRY_GRID GEOGRAPHY_GRID|  
|bounding_box_xmin|**float(53)**|之一的边界框左下角的 X 坐标：NULL = 不适用于给定的分割方案 （如 GEOGRAPHY_GRID) *n* = 如果 tessellation_scheme 为 GEOMETRY_GRID，最小 x 坐标值。                     **注意：** 由边界框参数定义的坐标解释为每个对象根据其[空间引用标识符 (SRID)](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)。|  
|bounding_box_ymin|**float(53)**|之一的边界框左下角的 Y 坐标：NULL = 不适用于给定的分割方案 （如 GEOGRAPHY_GRID) *n* = 如果 tessellation_scheme 为 GEOMETRY_GRID，最小 y 坐标值|  
|bounding_box_xmax|**float(53)**|之一的边界框右上角的 X 坐标：NULL = 不适用于给定的分割方案 （如 GEOGRAPHY_GRID) *n* = 如果 tessellation_scheme 为 GEOMETRY_GRID，最大 x 坐标值|  
|bounding_box_ymax|**float(53)**|之一的边界框右上角的 Y 坐标：NULL = 不适用于给定的分割方案 （如 GEOGRAPHY_GRID) *n* = 如果 tessellation_scheme 为 GEOMETRY_GRID，最大 y 坐标值|  
|level_1_grid|**smallint**|顶级网格的网格密度。 如果 tessellation_scheme 为 GEOMETRY_GRID 或 GEOGRAPHY_GRID，之一：        16 = 4 乘 4 网格 (LOW) 64 = 8 乘 8 网格 (MEDIUM) 256 = 16 乘 16 网格 （高） 为 NULL = 不适用于给定的空间索引类型或分割方案。  在使用新的 SQL Server 11 分割时，将返回 NULL。|  
|level_1_grid_desc|**nvarchar(60)**|其中一个的顶级网格的网格密度：低中型高 NULL = 不适用于给定的空间索引类型或分割方案。  在使用新的 SQL Server 11 分割时，将返回 NULL。|  
|level_2_grid|**smallint**|第二级网格的网格密度。 如果 tessellation_scheme 为 GEOMETRY_GRID 或 GEOGRAPHY_GRID，之一：16 = 4 乘 4 网格 (LOW) 64 = 8 乘 8 网格 (MEDIUM) 256 = 16 乘 16 网格 （高） 为 NULL = 不适用于给定的空间索引类型或分割方案。  在使用新的 SQL Server 11 分割时，将返回 NULL。|  
|level_2_grid_desc|**nvarchar(60)**|第二级网格，其中一个的网格密度：低中型高 NULL = 不适用于给定的空间索引类型或分割方案。  在使用新的 SQL Server 11 分割时，将返回 NULL。|  
|level_3_grid|**smallint**|第三级网格的网格密度。   如果 tessellation_scheme 为 GEOMETRY_GRID 或 GEOGRAPHY_GRID，之一：16 = 4 乘 4 网格 (LOW) 64 = 8 乘 8 网格 (MEDIUM) 256 = 16 乘 16 网格 （高） 为 NULL = 不适用于给定的空间索引类型或分割方案。  在使用新的 SQL Server 11 分割时，将返回 NULL。|  
|level_3_grid_desc|**nvarchar(60)**|第三级网格，其中一个的网格密度： 低中型高 NULL = 不适用于给定的空间索引类型或分割方案。  在使用新的 SQL Server 11 分割时，将返回 NULL。|  
|level_4_grid|**smallint**|第四级网格的网格密度。 如果 tessellation_scheme 为 GEOMETRY_GRID 或 GEOGRAPHY_GRID，之一：16 = 4 乘 4 网格 (LOW) 64 = 8 乘 8 网格 (MEDIUM) 256 = 16 乘 16 网格 （高） 为 NULL = 不适用于给定的空间索引类型或分割方案。  在使用新的 SQL Server 11 分割时，将返回 NULL。|  
|level_4_grid_desc|**nvarchar(60)**|第四级网格，其中一个的网格密度： < 低中型高 NULL = 不适用于给定的空间索引类型或分割方案。  在使用新的 SQL Server 11 分割时，将返回 NULL。|  
|cells_per_object|**int**|每个空间对象，其中一个单元格的数目：如果 tessellation_scheme 为 GEOMETRY_GRID 或 GEOGRAPHY_GRID， *n* = 的单元格数，每个对象为 NULL = 不适用于给定的空间索引类型或分割方案|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [空间索引概述](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [sys.objects (Transact-SQL)](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.spatial_indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-spatial-indexes-transact-sql.md)   
 [sys.indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
