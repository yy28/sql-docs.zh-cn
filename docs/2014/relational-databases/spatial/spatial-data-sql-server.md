---
title: 空间数据 (SQL Server) | Microsoft Docs
ms.date: 06/14/2017
ms.prod: sql-server-2014
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
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 7bd529f67f9184f86d4a9ec704e9cf7af972f3f3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66014058"
---
# <a name="spatial-data-sql-server"></a>空间数据 (SQL Server)
  空间数据表示有关物理位置和几何对象形状的信息。 这些对象可能是点位置或更复杂的对象，例如国家/地区、道路或湖泊。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支持两种空间数据类型： `geometry`数据类型和`geography`数据类型。  
  
-   `geometry`类型表示欧氏（平面）坐标系中的数据。  
  
-   
  `geography` 类型表示圆形地球坐标系中的数据。  
  
 这两种数据类型在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中都是作为 .NET 公共语言运行时 (CLR) 数据类型实现的。  
  
> [!IMPORTANT]  
>  有关 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]中引入的空间功能的详细说明和示例，请下载白皮书 [SQL Server 2012 中的新空间功能](https://go.microsoft.com/fwlink/?LinkId=226407)。  
  
##  <a name="reltasks"></a> 相关任务  
 [创建、构造和查询几何图形实例](create-construct-and-query-geometry-instances.md)  
 介绍可用于 geometry 数据类型实例的方法。  
  
 [创建、构造和查询地理实例](create-construct-and-query-geography-instances.md)  
 介绍可用于 geography 数据类型实例的方法。  
  
 [为 Nearest Neighbor 查询空间数据](query-spatial-data-for-nearest-neighbor.md)  
 介绍用于查找与特定的空间对象最接近的空间对象的常见查询模式。  
  
 [创建、修改和删除空间索引](create-modify-and-drop-spatial-indexes.md)  
 提供有关创建、更改和删除空间索引的信息。  
  
## <a name="related-content"></a>相关内容  
 [空间数据类型概述](spatial-data-types-overview.md)  
 介绍空间数据类型。  
  
-   [Point](point.md)  
  
-   [LineString](linestring.md)  
  
-   [CircularString](circularstring.md)  
  
-   [CompoundCurve](compoundcurve.md)  
  
-   [Polygon](polygon.md)  
  
-   [CurvePolygon](curvepolygon.md)  
  
-   [MultiPoint](multipoint.md)  
  
-   [MultiLineString](multilinestring.md)  
  
-   [MultiPolygon](multipolygon.md)  
  
-   [GeometryCollection](geometrycollection.md)  
  
 [空间索引概述](spatial-indexes-overview.md)  
 介绍空间索引并描述分割和分割方案。  
  
  
