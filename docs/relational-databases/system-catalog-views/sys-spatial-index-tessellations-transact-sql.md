---
title: "sys.spatial_index_tessellations (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fdac2e76ed1bc15a97981d91285569b4a18eb0a1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sysspatialindextessellations-transact-sql"></a>sys.spatial_index_tessellations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

 表示每个空间索引的分割方案和参数的相关信息。  
  
> [!NOTE]  
>  有关分割的信息，请参阅[空间索引概述](../../relational-databases/spatial/spatial-indexes-overview.md)。  
  

|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|定义了索引的对象的 ID。 每个 object_id (index_id） 对具有对应条目[sys.spatial_indexes](../../relational-databases/system-catalog-views/sys-spatial-indexes-transact-sql.md)。|  
|index_id|**int**|定义了索引列的空间索引的 ID。|  
|tessellation_scheme|**sysname**|分割方案，其中一个的名称： GEOMETRY_GRID、 GEOGRAPHY_GRID|  
|bounding_box_xmin|**float(53)**|边框的左下角的 X 坐标中，有一个： NULL = 不适用于给定的分割方案 （如 GEOGRAPHY_GRID)  *n*  = tessellation_scheme 是否 GEOMETRY_GRID、 最小 x 坐标值。                     **注意：**由边界框参数定义的坐标解释每个对象根据其[Spatial Reference Identifier (SRID)](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)。|  
|bounding_box_ymin|**float(53)**|边框的左下角的 Y 坐标中，有一个： NULL = 不适用于给定的分割方案 （如 GEOGRAPHY_GRID)  *n*  = tessellation_scheme 是否 GEOMETRY_GRID、 最小的 y 坐标值|  
|bounding_box_xmax|**float(53)**|边框的右上角的 X 坐标中，有一个： NULL = 不适用于给定的分割方案 （如 GEOGRAPHY_GRID)  *n*  = tessellation_scheme 是否 GEOMETRY_GRID，最大 x 坐标值|  
|bounding_box_ymax|**float(53)**|边框的右上角的 Y 坐标中，有一个： NULL = 不适用于给定的分割方案 （如 GEOGRAPHY_GRID)  *n*  = tessellation_scheme 是否 GEOMETRY_GRID，最大的 y 坐标值|  
|level_1_grid|**int**|顶级网格的网格密度。 如果 tessellation_scheme GEOMETRY_GRID 或 GEOGRAPHY_GRID、 之一： 由 16 网格 （高） 为 NULL 的 4 网格 （低） 64 = 8 由 8 网格 （中等规模） 256 = 16 16 = 4 = 不适用于给定的空间索引类型或分割方案。  在使用新的 SQL Server 11 分割时，将返回 NULL。|  
|level_1_grid_desc|**nvarchar(60)**|顶级网格，其中一个的网格密度： 低中等高 NULL = 不适用于给定的空间索引类型或分割方案。  在使用新的 SQL Server 11 分割时，将返回 NULL。|  
|level_2_grid|**int**|第二级网格的网格密度。 如果 tessellation_scheme GEOMETRY_GRID 或 GEOGRAPHY_GRID、 之一： 由 16 网格 （高） 为 NULL 的 4 网格 （低） 64 = 8 由 8 网格 （中等规模） 256 = 16 16 = 4 = 不适用于给定的空间索引类型或分割方案。  在使用新的 SQL Server 11 分割时，将返回 NULL。|  
|level_2_grid_desc|**nvarchar(60)**|第二个级别网格，其中一个的网格密度： 低中等高 NULL = 不适用于给定的空间索引类型或分割方案。  在使用新的 SQL Server 11 分割时，将返回 NULL。|  
|level_3_grid|**int**|第三级网格的网格密度。   如果 tessellation_scheme GEOMETRY_GRID 或 GEOGRAPHY_GRID、 之一： 由 16 网格 （高） 为 NULL 的 4 网格 （低） 64 = 8 由 8 网格 （中等规模） 256 = 16 16 = 4 = 不适用于给定的空间索引类型或分割方案。  在使用新的 SQL Server 11 分割时，将返回 NULL。|  
|level_3_grid_desc|**nvarchar(60)**|第三级网格，其中一个的网格密度： 低中等高 NULL = 不适用于给定的空间索引类型或分割方案。  在使用新的 SQL Server 11 分割时，将返回 NULL。|  
|level_4_grid|**int**|第四级网格的网格密度。 如果 tessellation_scheme GEOMETRY_GRID 或 GEOGRAPHY_GRID、 之一： 由 16 网格 （高） 为 NULL 的 4 网格 （低） 64 = 8 由 8 网格 （中等规模） 256 = 16 16 = 4 = 不适用于给定的空间索引类型或分割方案。  在使用新的 SQL Server 11 分割时，将返回 NULL。|  
|level_4_grid_desc|**nvarchar(60)**|第四级网格，其中一个的网格密度： < 低中等高 NULL = 不适用于给定的空间索引类型或分割方案。  在使用新的 SQL Server 11 分割时，将返回 NULL。|  
|cells_per_object|**int**|每个空间对象，其中一个单元数： tessellation_scheme 是否 GEOMETRY_GRID 或 GEOGRAPHY_GRID、  *n*  = 的每个对象为 NULL 的单元格数目 = 不适用于给定的空间索引类型或分割方案|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [对象目录视图 &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [空间索引概述](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [sys.objects &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.spatial_indexes &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-spatial-indexes-transact-sql.md)   
 [sys.indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
