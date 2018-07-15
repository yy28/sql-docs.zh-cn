---
title: GeometryCollection | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- GeomCollection geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 4445c0d9-a66b-4d7c-88e4-a66fa6f7d9fd
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3a0f4ad36d9664d6627d02edfc401af9ed3d8b55
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37307517"
---
# <a name="geometrycollection"></a>GeometryCollection
  一个`GeometryCollection`是零个或多集合`geometry`或`geography`实例。 一个`GeometryCollection`能为空。  
  
## <a name="geometrycollection-instances"></a>GeometryCollection 实例  
  
### <a name="accepted-instances"></a>已接受的实例  
 要接受某个 `GeometryCollection` 实例，该实例必须为空的 `GeometryCollection` 实例或组成 `GeometryCollection` 实例的所有实例必须为接受的实例。 下面的示例显示接受的实例。  
  
```  
DECLARE @g1 geometry = 'GEOMETRYCOLLECTION EMPTY';  
DECLARE @g2 geometry = 'GEOMETRYCOLLECTION(LINESTRING EMPTY,POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g3 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
 下面的示例将引发`System.FormatException`因为`LinesString`实例中`GeometryCollection`实例不可接受。  
  
```  
DECLARE @g geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1), POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
### <a name="valid-instances"></a>有效实例  
 当组成 `GeometryCollection` 实例的所有实例均有效时，`GeometryCollection` 实例有效。 以下示例显示三个有效`GeometryCollection`实例和一个不是有效的实例。  
  
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
  
## <a name="see-also"></a>请参阅  
 [空间数据 (SQL Server)](spatial-data-sql-server.md)  
  
  
