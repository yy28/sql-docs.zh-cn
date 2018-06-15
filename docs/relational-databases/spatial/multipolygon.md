---
title: MultiPolygon | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: spatial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MultiPolygon geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 2c5db358-2a16-49d9-aac5-a74e86813932
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 33f162687d14fe8b9fba65077a1da275d05c5c52
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32969968"
---
# <a name="multipolygon"></a>MultiPolygon
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **MultiPolygon** 实例是零个或更多个 **Polygon** 实例的集合。  
  
## <a name="polygon-instances"></a>Polygon 实例  
 下图显示了 **MultiPolygon** 实例的示例。  
  
 ![几何 MultiPolygon 实例的示例](../../relational-databases/spatial/media/multipolygon.gif "几何 MultiPolygon 实例的示例")  
  
 如图中所示：  
  
-   图 1 是一个包含两个 **Polygon** 元素的 **MultiPolygon** 实例。 边界由两个外环和三个内环界定。  
  
-   图 2 是一个包含两个 **MultiPolygon** 元素的 **Polygon** 实例。 边界由两个外环和三个内环界定。 这两个 **Polygon** 元素在切点处相交。  
  
### <a name="accepted-instances"></a>已接受的实例  
 当满足以下条件之一时，接受 **MultiPolygon** 实例。  
  
-   它是空的 **MultiPolygon** 实例。  
  
-   组成 **MultiPolygon** 实例的所有实例是接受的 **Polygon** 实例。 有关接受的 **Polygon** 实例的详细信息，请参阅 [Polygon](../../relational-databases/spatial/polygon.md)。  
  
 下面的示例显示接受的 **MultiPolygon** 实例。  
  
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
 如果 **MultiPolygon** 实例是空的 **MultiPolygon** 实例或者它满足以下条件，则前者有效。  
  
1.  组成 **MultiPolygon** 实例的所有实例是有效的 **Polygon** 实例。 对于有效的 **Polygon** 实例，请参阅 [Polygon](../../relational-databases/spatial/polygon.md)。  
  
2.  组成 **Polygon** 实例的所有 **MultiPolygon** 实例都不会重叠。  
  
 以下示例显示两个有效的 **MultiPolygon** 实例和一个无效的 **MultiPolygon** 实例。  
  
```  
DECLARE @g1 geometry = 'MULTIPOLYGON EMPTY';  
DECLARE @g2 geometry = 'MULTIPOLYGON(((1 1, 1 -1, -1 -1, -1 1, 1 1)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
DECLARE @g3 geometry = 'MULTIPOLYGON(((2 2, 2 -2, -2 -2, -2 2, 2 2)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
```  
  
 `@g2` 之所以有效，原因在于两个 **Polygon** 实例仅在切点接触。 `@g3` 之所以无效，原因在于这两个 **Polygon** 实例的内部相互重叠。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [Polygon](../../relational-databases/spatial/polygon.md)   
 [STArea（geometry 数据类型）](../../t-sql/spatial-geometry/starea-geometry-data-type.md)   
 [STCentroid（geometry 数据类型）](../../t-sql/spatial-geometry/stcentroid-geometry-data-type.md)   
 [STPointOnSurface（geometry 数据类型）](../../t-sql/spatial-geometry/stpointonsurface-geometry-data-type.md)   
 [空间数据 (SQL Server)](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
