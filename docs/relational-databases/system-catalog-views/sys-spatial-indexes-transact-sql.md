---
title: sys.spatial_indexes (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.spatial_indexes_TSQL
- spatial_indexes
- spatial_indexes_TSQL
- sys.spatial_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.spatial_indexes catalog view
ms.assetid: 40e967d5-2e8d-45af-bf5e-5251493cf7cb
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 39b12f5bfd0a3227120a9f38950e5265e8b262dd
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sysspatialindexes-transact-sql"></a>sys.spatial_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  表示空间索引的主索引信息。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|\<继承列 >||继承中的列[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)。|  
|spatial_index_type|**tinyint**|空间索引的类型：<br /><br /> 1 = 几何空间索引<br /><br /> 2 = 地理空间索引|  
|spatial_index_type_desc|**nvarchar(60)**|空间索引的类型说明：<br /><br /> GEOMETRY = 几何空间索引<br /><br /> GEOGRAPHY = 地理空间索引|  
|tessellation_scheme|**sysname**|分割方案的名称：<br /><br /> GEOMETRY_GRID、GEOMETRY_AUTO_GRID、<br /><br /> GEOGRAPHY_GRID、GEOGRAPHY_AUTO_GRID<br /><br /> 注意： 有关分割方案的信息，请参阅[空间索引概述](../../relational-databases/spatial/spatial-indexes-overview.md)。|  
|\<继承列 >||继承中的列[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)。<br /><br /> 继承的列 has_filter 和 filter_definition 显示在特定于空间索引的列之后。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [sys.objects (Transact-SQL)](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.spatial_index_tessellations (Transact-SQL)](../../relational-databases/system-catalog-views/sys-spatial-index-tessellations-transact-sql.md)   
 [sys.indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [空间索引概述](../../relational-databases/spatial/spatial-indexes-overview.md)  
  
  
