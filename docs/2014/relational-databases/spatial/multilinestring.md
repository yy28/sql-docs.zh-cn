---
title: MultiLineString | Microsoft Docs
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
- MultiLineString geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 95deeefe-d6c5-4a11-b347-379e4486e7b7
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c340afc52dbd60f4accb1da7d3883e62d36974f6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37288523"
---
# <a name="multilinestring"></a>MultiLineString
  一个`MultiLineString`是零个或多集合`geometry`或**geographyLineString**实例。  
  
## <a name="multilinestring-instances"></a>MultiLineString 实例  
 下图显示了示例的`MultiLineString`实例。  
  
 ![几何 MultiLineString 实例的示例](../../database-engine/media/multilinestring.gif "几何 MultiLineString 实例的示例")  
  
 如图中所示：  
  
-   图 1 是一个简单`MultiLineString`实例，其边界是其两个四个端点`LineString`元素。  
  
-   图 2 显示的是一个简单的 `MultiLineString` 实例，因为只有 `LineString` 元素的端点相交。 边界是两个不重叠的端点。  
  
-   图 3 显示的是一个不简单的 `MultiLineString` 实例，因为它的其中一个 `LineString` 元素的内部出现了相交。 此边界`MultiLineString`实例是四个终结点。  
  
-   图 4 显示的是一个不简单、 非闭合的`MultiLineString`实例。  
  
-   图 5 显示的是一个简单、非闭合的 `MultiLineString`。 它没有闭合是因为其`LineStrings`元素没有闭合。 它是简单因为无任何内部`LineStrings`实例相交。  
  
-   图 6 是一个简单、 关闭`MultiLineString`实例。 它为闭合的是因为它的所有元素都是闭合的。 而其简单的原因在于，其所有元素都没有出现内部相交现象。  
  
### <a name="accepted-instances"></a>接受的实例  
 有关`MultiLineString`实例可接受它必须或者为空或组成仅`LineString`接受的实例。 有关详细信息接受`LineString`实例，请参阅[LineString](../spatial/linestring.md)。 下面的示例显示接受的 `MultiLineString` 实例。  
  
```  
DECLARE @g1 geometry = 'MULTILINESTRING EMPTY';  
DECLARE @g2 geometry = 'MULTILINESTRING((1 1, 3 5), (-5 3, -8 -2))';  
DECLARE @g3 geometry = 'MULTILINESTRING((1 1, 5 5), (1 3, 3 1))';  
DECLARE @g4 geometry = 'MULTILINESTRING((1 1, 3 3, 5 5),(3 3, 5 5, 7 7))';  
```  
  
 下面的示例将引发`System.FormatException`因为第二个`LineString`实例无效。  
  
```  
DECLARE @g geometry = 'MULTILINESTRING((1 1, 3 5),(-5 3))';  
```  
  
### <a name="valid-instances"></a>有效实例  
 有关`MultiLineString`实例才是有效它必须满足以下条件：  
  
1.  组成 `MultiLineString` 实例的所有实例必须是有效的 `LineString` 实例。  
  
2.  组成 `LineString` 实例的任何两个 `MultiLineString` 实例在某个间隔内都不会重叠。 `LineString` 实例只能与其自身或其他 `LineString` 实例在有限数量的点相交或接触。  
  
 以下示例显示三个有效的 `MultiLineString` 实例和一个无效的 `MultiLineString` 实例。  
  
```  
DECLARE @g1 geometry = 'MULTILINESTRING EMPTY';  
DECLARE @g2 geometry = 'MULTILINESTRING((1 1, 3 5), (-5 3, -8 -2))';  
DECLARE @g3 geometry = 'MULTILINESTRING((1 1, 5 5), (1 3, 3 1))';  
DECLARE @g4 geometry = 'MULTILINESTRING((1 1, 3 3, 5 5),(3 3, 5 5, 7 7))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
 `@g4` 不是有效因为第二个`LineString`与第一个实例重叠`LineString`实例在某个间隔。 它们在无限数量的点处接触。  
  
## <a name="examples"></a>示例  
 下面的示例创建了一个包含两个 `geometry``MultiLineString` 元素且 SRID 为 0 的简单 `LineString` 实例。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 2, 1 1), (1 0, 1 1))');  
```  
  
 若要使用不同的 SRID 实例化此实例，请使用 `STGeomFromText()` 或 `STMLineStringFromText()`。 也可以使用 `Parse()` ，然后修改 SRID，如下例所示。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 2, 1 1), (1 0, 1 1))');  
SET @g.STSrid = 13;  
```  
  
## <a name="see-also"></a>请参阅  
 [STLength（geometry 数据类型）](/sql/t-sql/spatial-geometry/stlength-geometry-data-type)   
 [STIsClosed（geometry 数据类型）](/sql/t-sql/spatial-geometry/stisclosed-geometry-data-type)   
 [LineString](../spatial/linestring.md)   
 [空间数据 (SQL Server)](../spatial/spatial-data-sql-server.md)  
  
  
