---
title: STCurveToLine（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveToLine method (geometry)
ms.assetid: abc80b32-4152-4e10-b816-798b901e0ac5
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d2b8e54971337520c8d96caa7560436f34a692a8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33063964"
---
# <a name="stcurvetoline-geometry-data-type"></a>STCurveToLine（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

返回包含圆弧线段的 geometry 实例的多边形近似值。
  
## <a name="syntax"></a>语法  
  
```  
  
.STCurveToLine ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geometry  
  
 CLR 返回类型：SqlGeometry  
  
## <a name="remarks"></a>Remarks  
 为空的 geometry 实例变量返回空的 GeometryCollection 实例，为未初始化的 geometry 变量返回 NULL。  
  
 该方法返回的多边形近似值取决于用于调用该方法的 **geometry** 实例：  
  
-   为 CircularString 或 CompoundCurve 实例返回 LineString 实例。  
  
-   为 CurvePolygon 实例返回 Polygon 实例。  
  
-   如果 geometry 实例不是 CircularString、CompoundCurve 或 CurvePolygon 实例，则返回该实例的副本。 例如，`STCurveToLine` 方法为属于 **Point** 实例的 **geometry** 实例返回 **Point** 实例。  
  
 与 SQL/MM 规范不同，`STCurveToLine` 方法不使用 Z 坐标值来计算多边形近似值。 该方法忽略执行调用的 **geometry** 实例中存在的任何 Z 坐标值。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-an-uninitialized-geometry-variable-and-empty-instance"></a>A. 使用未初始化的 Geometry 变量和空实例  
 在以下示例中，第一个 **SELECT** 语句使用未初始化的 **geometry** 实例调用 `STCurveToLine` 方法，第二个 **SELECT** 语句使用空的 **geometry** 实例。 因此，该方法为第一个语句返回 **NULL**，为第二个语句返回 **GeometryCollection** 集合。  
  
```
 DECLARE @g geometry; 
 SET @g = @g.STCurveToLine(); 
 SELECT @g.STGeometryType(); 
 SET @g = geometry::Parse('LINESTRING EMPTY'); 
 SELECT @g.STGeometryType();
 ```  
  
### <a name="b-using-a-linestring-instance"></a>B. 使用 LineString 实例  
 以下示例中的 **SELECT** 语句使用 **LineString** 实例调用 STCurveToLine 方法。 因此，该方法返回 **LineString** 实例。  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('LINESTRING(1 3, 5 5, 4 3, 1 3)'); 
 SET @g = @g.STCurveToLine(); 
 SELECT @g.STGeometryType();
 ```  
  
### <a name="c-using-a-circularstring-instance"></a>C. 使用 CircularString 实例  
 以下示例中的第一个 **SELECT** 语句使用 **CircularString** 实例调用 STCurveToLine 方法。 因此，该方法返回 **LineString** 实例。 该 **SELECT** 语句还比较两个实例的长度，它们大致相同。  最后，第二个 **SELECT** 语句返回每个实例的点数。  它仅为 **CircularString** 实例返回 5 个点，而为 **LineString** 实例返回 65 个点。  
  
```
 DECLARE @g1 geometry, @g2 geometry; 
 SET @g1 = geometry::Parse('CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0)'); 
 SET @g2 = @g1.STCurveToLine(); 
 SELECT @g1.STGeometryType() AS [G1 Type], @g2.STGeometryType() AS [G2 Type], @g1.STLength() AS [G1 Perimeter], @g2.STLength() AS [G2 Perimeter], @g2.ToString() AS [G2 Def]; 
 SELECT @g1.STNumPoints(), @g2.STNumPoints();
 ```  
  
### <a name="d-using-a-curvepolygon-instance"></a>D. 使用 CurvePolygon 实例  
 以下示例中的 **SELECT** 语句使用 **CurvePolygon** 实例调用 STCurveToLine 方法。 因此，该方法返回 **Polygon** 实例。  
  
```
 DECLARE @g1 geometry, @g2 geometry; 
 SET @g1 = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0))'); 
 SET @g2 = @g1.STCurveToLine(); 
 SELECT @g1.STGeometryType() AS [G1 Type], @g2.STGeometryType() AS [G2 Type];
 ```  
  
## <a name="see-also"></a>另请参阅  
 [空间数据类型概述](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [STLength（geometry 数据类型）](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)   
 [STNumPoints（geometry 数据类型）](../../t-sql/spatial-geometry/stnumpoints-geometry-data-type.md)   
 [STGeometryType（geometry 数据类型）](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)  
  
  

