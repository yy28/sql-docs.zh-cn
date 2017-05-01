---
title: GeometryCollection | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- GeomCollection geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 4445c0d9-a66b-4d7c-88e4-a66fa6f7d9fd
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ad3b942675c879183f8be2fe8bc8b82effee8bf2
ms.lasthandoff: 04/11/2017

---
# <a name="geometrycollection"></a>GeometryCollection
  **GeometryCollection** 是零个或更多个 **geometry** 或 **geography** 实例的集合。 **GeometryCollection** 可以为空。  
  
## <a name="geometrycollection-instances"></a>GeometryCollection 实例  
  
### <a name="accepted-instances"></a>已接受的实例  
 要接受某个 **GeometryCollection** 实例，该实例必须为空的 **GeometryCollection** 实例或组成 **GeometryCollection** 实例的所有实例必须为接受的实例。 下面的示例显示接受的实例。  
  
```  
DECLARE @g1 geometry = 'GEOMETRYCOLLECTION EMPTY';  
DECLARE @g2 geometry = 'GEOMETRYCOLLECTION(LINESTRING EMPTY,POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g3 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
 下面的示例引发一个 `System.FormatException` ，因为 **GeometryCollection** 实例中的 **LinesString** 实例不是接受的实例。  
  
```  
DECLARE @g geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1), POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
### <a name="valid-instances"></a>有效实例  
 当组成 **GeometryCollection** 实例的所有实例均有效时， **GeometryCollection** 实例有效。 以下示例显示三个有效的 **GeometryCollection** 实例和一个无效的实例。  
  
```  
DECLARE @g1 geometry = 'GEOMETRYCOLLECTION EMPTY';  
DECLARE @g2 geometry = 'GEOMETRYCOLLECTION(LINESTRING EMPTY,POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g3 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g4 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, 1 -5, -5 5, -5 -1, -1 -1)))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
 `@g4` 无效，因为 **GeometryCollection** 实例中的 **Polygon** 实例无效。  
  
 有关接受的和有效的实例的详细信息，请参阅 [Point](../../relational-databases/spatial/point.md)、 [MultiPoint](../../relational-databases/spatial/multipoint.md)、 [LineString](../../relational-databases/spatial/linestring.md)、 [MultiLineString](../../relational-databases/spatial/multilinestring.md)、 [Polygon](../../relational-databases/spatial/polygon.md)和 [MultiPolygon](../../relational-databases/spatial/multipolygon.md)。  
  
## <a name="examples"></a>示例  
 下面的示例实例化一个包含 `geometry``GeometryCollection` 实例和 `Point` 实例的 `Polygon` ，它具有 Z 值，且 SRID 为 1。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomCollFromText('GEOMETRYCOLLECTION(POINT(3 3 1), POLYGON((0 0 2, 1 10 3, 1 0 4, 0 0 2)))', 1);  
```  
  
## <a name="see-also"></a>另请参阅  
 [空间数据 (SQL Server)](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
