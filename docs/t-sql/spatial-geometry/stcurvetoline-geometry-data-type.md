---
title: "STCurveToLine (geometry 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords: STCurveToLine method (geometry)
ms.assetid: abc80b32-4152-4e10-b816-798b901e0ac5
caps.latest.revision: "19"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 59e40c95212420ed5f2dd46c46cf11eca623fd29
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="stcurvetoline-geometry-data-type"></a>STCurveToLine（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

返回多边形的近似**几何图形**包含条圆弧线段实例。
  
## <a name="syntax"></a>语法  
  
```  
  
.STCurveToLine ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**几何图形**  
  
 CLR 返回类型： **SqlGeometry**  
  
## <a name="remarks"></a>注释  
 返回一个空**GeometryCollection**空实例**几何图形**实例变量和返回**NULL**为未初始化的**几何图形**变量。  
  
 取决于该方法返回的多边形近似**几何图形**用于调用方法的实例：  
  
-   返回**LineString**实例**CircularString**或**CompoundCurve**实例。  
  
-   返回**多边形**实例**CurvePolygon**实例。  
  
-   返回一份**几何图形**实例如果该实例不是**CircularString**， **CompoundCurve**，或**CurvePolygon**实例. 例如，`STCurveToLine`方法返回**点**实例**几何图形**实例，它是**点**实例。  
  
 与 SQL/MM 规范中，不同`STCurveToLine`方法不使用 z 坐标值来计算的多边形的近似值。 该方法将忽略任何调用中存在的 z 坐标值**几何图形**实例。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-an-uninitialized-geometry-variable-and-empty-instance"></a>A. 使用未初始化的 Geometry 变量和空实例  
 在下面的示例中，第一个**选择**语句使用未初始化**几何图形**实例来调用`STCurveToLine`方法和第二个**选择**语句使用一个空**几何图形**实例。 因此，该方法返回**NULL**的第一个语句和**GeometryCollection**到第二个语句的集合。  
  
```
 DECLARE @g geometry; 
 SET @g = @g.STCurveToLine(); 
 SELECT @g.STGeometryType(); 
 SET @g = geometry::Parse('LINESTRING EMPTY'); 
 SELECT @g.STGeometryType();
 ```  
  
### <a name="b-using-a-linestring-instance"></a>B. 使用 LineString 实例  
 **选择**语句在下面的示例使用**LineString**实例调用 STCurveToLine 方法。 因此，该方法返回**LineString**实例。  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('LINESTRING(1 3, 5 5, 4 3, 1 3)'); 
 SET @g = @g.STCurveToLine(); 
 SELECT @g.STGeometryType();
 ```  
  
### <a name="c-using-a-circularstring-instance"></a>C. 使用 CircularString 实例  
 第一个**选择**语句在下面的示例使用**CircularString**实例调用 STCurveToLine 方法。 因此，该方法返回**LineString**实例。 这**选择**语句也将进行比较的两个实例都大约是相同的长度。  最后，第二个**选择**语句返回的每个实例的点数。  它返回的仅 5 点**CircularString**实例，但 65 点**LineString**实例。  
  
```
 DECLARE @g1 geometry, @g2 geometry; 
 SET @g1 = geometry::Parse('CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0)'); 
 SET @g2 = @g1.STCurveToLine(); 
 SELECT @g1.STGeometryType() AS [G1 Type], @g2.STGeometryType() AS [G2 Type], @g1.STLength() AS [G1 Perimeter], @g2.STLength() AS [G2 Perimeter], @g2.ToString() AS [G2 Def]; 
 SELECT @g1.STNumPoints(), @g2.STNumPoints();
 ```  
  
### <a name="d-using-a-curvepolygon-instance"></a>D. 使用 CurvePolygon 实例  
 **选择**语句在下面的示例使用**CurvePolygon**实例调用 STCurveToLine 方法。 因此，该方法返回**多边形**实例。  
  
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
  
  

