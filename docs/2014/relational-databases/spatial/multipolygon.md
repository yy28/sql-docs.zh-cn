---
title: MultiPolygon | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- dbe-spatial
ms.topic: conceptual
helpviewer_keywords:
- MultiPolygon geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 2c5db358-2a16-49d9-aac5-a74e86813932
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 35618fe95194a2c8fe256720bbfb3bb223390e57
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48076850"
---
# <a name="multipolygon"></a>MultiPolygon
  一个`MultiPolygon`实例是零个或多集合`Polygon`实例。  
  
## <a name="polygon-instances"></a>Polygon 实例  
 下图显示了示例的`MultiPolygon`实例。  
  
 ![几何 MultiPolygon 实例的示例](../../database-engine/media/multipolygon.gif "几何 MultiPolygon 实例的示例")  
  
 如图中所示：  
  
-   图 1 是`MultiPolygon`具有两个实例`Polygon`元素。 边界由两个外环和三个内环界定。  
  
-   图 2 是一个包含两个 `MultiPolygon` 元素的 `Polygon` 实例。 边界由两个外环和三个内环界定。 这两个 `Polygon` 元素在切点处相交。  
  
### <a name="accepted-instances"></a>已接受的实例  
 一个`MultiPolygon`实例接受的满足以下条件之一。  
  
-   它是一个空`MultiPolygon`实例。  
  
-   包含的所有实例`MultiPolygon`实例接受`Polygon`实例。 有关详细信息接受`Polygon`实例，请参阅[多边形](../spatial/polygon.md)。  
  
 以下示例显示接受`MultiPolygon`实例。  
  
```  
DECLARE @g1 geometry = 'MULTIPOLYGON EMPTY';  
DECLARE @g2 geometry = 'MULTIPOLYGON(((1 1, 1 -1, -1 -1, -1 1, 1 1)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
DECLARE @g3 geometry = 'MULTIPOLYGON(((2 2, 2 -2, -2 -2, -2 2, 2 2)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
```  
  
 下面的示例显示一个将引发 `System.FormatException`的 MultiPolygon 实例。  
  
```  
DECLARE @g geometry = 'MULTIPOLYGON(((1 1, 1 -1, -1 -1, -1 1, 1 1)),((1 1, 3 1, 3 3)))';  
```  
  
 MultiPolygon 中的第二个实例是 LineString 实例，而不是接受的 Polygon 实例。  
  
### <a name="valid-instances"></a>有效实例  
 如果 `MultiPolygon` 实例是空的 `MultiPolygon` 实例或者它满足以下条件，则前者有效。  
  
1.  组成 `MultiPolygon` 实例的所有实例是有效的 `Polygon` 实例。 有关有效`Polygon`实例，请参阅[多边形](../spatial/polygon.md)。  
  
2.  组成 `Polygon` 实例的所有 `MultiPolygon` 实例都不会重叠。  
  
 以下示例显示两个有效的 `MultiPolygon` 实例和一个无效的 `MultiPolygon` 实例。  
  
```  
DECLARE @g1 geometry = 'MULTIPOLYGON EMPTY';  
DECLARE @g2 geometry = 'MULTIPOLYGON(((1 1, 1 -1, -1 -1, -1 1, 1 1)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
DECLARE @g3 geometry = 'MULTIPOLYGON(((2 2, 2 -2, -2 -2, -2 2, 2 2)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
```  
  
 `@g2` 无效，因为这两个`Polygon`实例仅在切点接触。 `@g3` 不是有效因为的两个内部`Polygon`实例相互重叠。  
  
## <a name="examples"></a>示例  
 下面的示例演示如何创建 `geometry``MultiPolygon` 实例，并返回第二个组件的熟知文本 (WKT)。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTIPOLYGON(((0 0, 0 3, 3 3, 3 0, 0 0), (1 1, 1 2, 2 1, 1 1)), ((9 9, 9 10, 10 9, 9 9)))');  
SELECT @g.STGeometryN(2).STAsText();  
```  
  
 该示例实例化一个空的 `MultiPolygon` 实例。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTIPOLYGON EMPTY');  
```  
  
## <a name="see-also"></a>请参阅  
 [Polygon](../spatial/polygon.md)   
 [STArea（geometry 数据类型）](/sql/t-sql/spatial-geometry/starea-geometry-data-type)   
 [STCentroid（geometry 数据类型）](/sql/t-sql/spatial-geometry/stcentroid-geometry-data-type)   
 [STPointOnSurface（geometry 数据类型）](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)   
 [空间数据 (SQL Server)](../spatial/spatial-data-sql-server.md)  
  
  
