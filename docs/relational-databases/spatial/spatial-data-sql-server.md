---
title: 空间数据 (SQL Server) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- geography data type [SQL Server], spatial storage design
- planar spatial data [SQL Server], designing
- spatial data types [SQL Server]
- geodetic spatial data [SQL Server]
- geometry data type [SQL Server], spatial storage design
- spatial storage [SQL Server]
- geodetic spatial data [SQL Server], designing
ms.assetid: 41a132a1-09e2-4426-b9df-225270cb8e15
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f6c3dcb4a6c1c23513a9dd8ea74f1eac5c6e3d65
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51663076"
---
# <a name="spatial-data-sql-server"></a>空间数据 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  空间数据表示有关几何对象的物理位置和形状的信息。 这些对象可以是点位置或更复杂的对象，例如国家/地区、公路或湖泊。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持两种空间数据类型： **geometry** 数据类型和 **geography** 数据类型。  
  
-   **Geometry** 类型表示欧几里得（平面）坐标系中的数据。  
  
-   **Geography** 类型表示圆形地球坐标系中的数据。  
  
 这两种数据类型在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中都是作为 .NET 公共语言运行时 (CLR) 数据类型实现的。  
  
> [!IMPORTANT]  
>  有关 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]中引入的空间功能的详细说明和示例，请下载白皮书 [SQL Server 2012 中的新空间功能](https://go.microsoft.com/fwlink/?LinkId=226407)。  
  
##  <a name="reltasks"></a> 相关任务  
 [创建、构造和查询几何图形实例](../../relational-databases/spatial/create-construct-and-query-geometry-instances.md)  
 介绍可用于 geometry 数据类型实例的方法。  
  
 [创建、构造和查询地理实例](../../relational-databases/spatial/create-construct-and-query-geography-instances.md)  
 介绍可用于 geography 数据类型实例的方法。  
  
 [为 Nearest Neighbor 查询空间数据](../../relational-databases/spatial/query-spatial-data-for-nearest-neighbor.md)  
 介绍用于查找与特定的空间对象最接近的空间对象的常见查询模式。  
  
 [创建、修改和删除空间索引](../../relational-databases/spatial/create-modify-and-drop-spatial-indexes.md)  
 提供有关创建、更改和删除空间索引的信息。  
  
## <a name="related-content"></a>相关内容  
 [空间数据类型概述](../../relational-databases/spatial/spatial-data-types-overview.md)  
 介绍空间数据类型。  
  
-   [点](../../relational-databases/spatial/point.md)  
  
-   [LineString](../../relational-databases/spatial/linestring.md)  
  
-   [CircularString](../../relational-databases/spatial/circularstring.md)  
  
-   [CompoundCurve](../../relational-databases/spatial/compoundcurve.md)  
  
-   [多边形](../../relational-databases/spatial/polygon.md)  
  
-   [CurvePolygon](../../relational-databases/spatial/curvepolygon.md)  
  
-   [MultiPoint](../../relational-databases/spatial/multipoint.md)  
  
-   [MultiLineString](../../relational-databases/spatial/multilinestring.md)  
  
-   [MultiPolygon](../../relational-databases/spatial/multipolygon.md)  
  
-   [GeometryCollection](../../relational-databases/spatial/geometrycollection.md)  
  
 [空间索引概述](../../relational-databases/spatial/spatial-indexes-overview.md)  
 介绍空间索引并描述分割和分割方案。  
  
  
