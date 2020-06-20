---
title: GeometryCollection | Microsoft Docs
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- GeomCollection geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 4445c0d9-a66b-4d7c-88e4-a66fa6f7d9fd
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: b882aad6557eb812ee44eeeb46ecbbbda86061c3
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "84996324"
---
# <a name="geometrycollection"></a>GeometryCollection
  `GeometryCollection` 是零个或更多个 `geometry` 或 `geography` 实例的集合。 `GeometryCollection` 可以为空。  
  
## <a name="geometrycollection-instances"></a>GeometryCollection 实例  
  
### <a name="accepted-instances"></a>已接受的实例  
 要接受某个 `GeometryCollection` 实例，该实例必须为空的 `GeometryCollection` 实例或组成 `GeometryCollection` 实例的所有实例必须为接受的实例。 下面的示例显示接受的实例。  
  
```  
DECLARE @g1 geometry = 'GEOMETRYCOLLECTION EMPTY';  
DECLARE @g2 geometry = 'GEOMETRYCOLLECTION(LINESTRING EMPTY,POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g3 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
 下面的示例引发一个 `System.FormatException`，因为 `LinesString` 实例中的 `GeometryCollection` 实例不是接受的实例。  
  
```  
DECLARE @g geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1), POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
### <a name="valid-instances"></a>有效实例  
 当组成 `GeometryCollection` 实例的所有实例均有效时，`GeometryCollection` 实例有效。 以下示例显示三个有效的 `GeometryCollection` 实例和一个无效的实例。  
  
```  
DECLARE @g1 geometry = 'GEOMETRYCOLLECTION EMPTY';  
DECLARE @g2 geometry = 'GEOMETRYCOLLECTION(LINESTRING EMPTY,POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g3 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g4 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, 1 -5, -5 5, -5 -1, -1 -1)))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
 `@g4` 无效，因为 `Polygon` 实例中的 `GeometryCollection` 实例无效。  
  
 有关接受的和有效的实例的详细信息，请参阅 [Point](point.md)、 [MultiPoint](multipoint.md)、 [LineString](linestring.md)、 [MultiLineString](multilinestring.md)、 [Polygon](polygon.md)和 [MultiPolygon](multipolygon.md)。  
  
## <a name="examples"></a>示例  
 下面的示例实例化一个包含 `geometry``GeometryCollection` 实例和 `Point` 实例的 `Polygon` ，它具有 Z 值，且 SRID 为 1。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomCollFromText('GEOMETRYCOLLECTION(POINT(3 3 1), POLYGON((0 0 2, 1 10 3, 1 0 4, 0 0 2)))', 1);  
```  
  
## <a name="see-also"></a>另请参阅  
 [空间数据 (SQL Server)](spatial-data-sql-server.md)  
  
  
