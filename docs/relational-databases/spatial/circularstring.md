---
title: "CircularString | Microsoft Docs"
ms.custom: ""
ms.date: "06/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-spatial"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9fe06b03-d98c-4337-9f89-54da98f49f9f
caps.latest.revision: 27
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 27
---
# CircularString
  **CircularString** 是零个或多个连续圆弧线段的集合。 圆弧线段是二维平面中由三个点定义的曲线段；第一个点不能与第三个点相同。 如果圆弧线段的所有三个点共线，则将该圆弧线段视为一条直线段。  
  
> [!IMPORTANT]  
>  有关 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中引入的新空间功能的详细说明和示例（包括 **CircularString** 子类型），请下载白皮书 [SQL Server 2012 中的新空间功能](http://go.microsoft.com/fwlink/?LinkId=226407)。  
  
## CircularString 实例  
 下面的图形显示了有效的 **CircularString** 实例：  
  
 ![5ff17e34-b578-4873-9d33-79500940d0bc](../../relational-databases/spatial/media/5ff17e34-b578-4873-9d33-79500940d0bc.gif)
  
### 接受的实例  
 如果 **CircularString** 实例为空或包含奇数个点 n，其中 n > 1，则该实例将被接受。 下面的 **CircularString** 实例均为已接受实例。  
  
```  
DECLARE @g1 geometry = 'CIRCULARSTRING EMPTY';  
DECLARE @g2 geometry = 'CIRCULARSTRING(1 1, 2 0, -1 1)';  
DECLARE @g3 geometry = 'CIRCULARSTRING(1 1, 2 0, 2 0, 2 0, 1 1)';  
```  
  
 `@g3` 显示 **CircularString** 实例可能被接受，但无效。 下面的 CircularString 实例声明未被接受。 此声明引发 `System.FormatException`。  
  
```  
DECLARE @g geometry = 'CIRCULARSTRING(1 1, 2 0, 2 0, 1 1)';  
```  
  
### 有效实例  
 有效 **CircularString** 实例必须为空或具有以下属性：  
  
-   必须至少包含一条圆弧线段（也就是至少有三个点）。  
  
-   序列中的每条圆弧线段（最后一条线段除外）的最后一个端点必须是序列中后一条线段的第一个端点。  
  
-   必须有奇数个点。  
  
-   不能有一段与自身重合。  
  
-   虽然 **CircularString** 实例可能包含直线段，但这些直线段必须由三个共线点定义。  
  
 下面的示例显示有效的 **CircularString** 实例。  
  
```  
DECLARE @g1 geometry = 'CIRCULARSTRING EMPTY';  
DECLARE @g2 geometry = 'CIRCULARSTRING(1 1, 2 0, -1 1)';  
DECLARE @g3 geometry = 'CIRCULARSTRING(1 1, 2 0, 2 0, 1 1, 0 1)';  
DECLARE @g4 geometry = 'CIRCULARSTRING(1 1, 2 2, 2 2)';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(),@g4.STIsValid();  
```  
  
 **CircularString** 实例必须至少包含两条圆弧线段以定义完整的圆。 **CircularString** 实例不能使用一条圆弧线段（例如（1 1、3 1、1 1））定义一个完整的圆。 使用（1 1、2 2、3 1、2 0、1 1）定义圆。  
  
 下面的示例显示无效的 CircularString 实例。  
  
```  
DECLARE @g1 geometry = 'CIRCULARSTRING(1 1, 2 0, 1 1)';  
DECLARE @g2 geometry = 'CIRCULARSTRING(0 0, 0 0, 0 0)';  
SELECT @g1.STIsValid(), @g2.STIsValid();  
```  
  
### 具有共线点的实例  
 在下列情况下，圆弧线段将被视为直线段：  
  
-   当所有三个点共线时，例如（1 3、4 4、7 5）。  
  
-   当第一个点和中间的点相同但第三个点不同时，例如（1 3、1 3、7 5）。  
  
-   当中间的点和最后一个点相同但第一个点不同时，例如（1 3、4 4、4 4）。  
  
## 示例  
  
### A. 使用空的 CircularString 实例化一个几何图形实例  
 该示例说明如何创建一个空的 **CircularString** 实例：  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CIRCULARSTRING EMPTY');  
```  
  
### B. 使用具有一条圆弧线段的 CircularString 实例化一个几何图形实例  
 下面的示例演示如何创建一个具有一条圆弧线段（半圆）的 **CircularString** 实例：  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry:: STGeomFromText('CIRCULARSTRING(2 0, 1 1, 0 0)', 0);  
SELECT @g.ToString();  
```  
  
### C. 使用具有多条圆弧线段的 CircularString 实例化一个几何图形实例  
 下面的示例演示如何创建一个具有多个圆弧线段（整圆）的 **CircularString** 实例：  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CIRCULARSTRING(2 1, 1 2, 0 1, 1 0, 2 1)');  
SELECT 'Circumference = ' + CAST(@g.STLength() AS NVARCHAR(10));    
```  
  
 此示例将产生以下输出：  
  
```  
Circumference = 6.28319  
```  
  
 在使用 **LineString** 而不使用 **CircularString**时，比较输出结果：  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(2 1, 1 2, 0 1, 1 0, 2 1)', 0);  
SELECT 'Perimeter = ' + CAST(@g.STLength() AS NVARCHAR(10));  
```  
  
 此示例将产生以下输出：  
  
```  
Perimeter = 5.65685  
```  
  
 请注意， **CircularString** 示例的值接近 2∏，这是圆的实际周长。  
  
### D. 在同一语句中使用 CircularString 声明和实例化一个几何图形实例  
 此代码段说明了如何在同一语句中使用 **geometry** 声明和实例化 **CircularString** 实例：  
  
```tsql  
DECLARE @g geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
```  
  
### E. 使用 CircularString 实例化一个地域实例  
 下面的示例演示如何使用 **geography** 声明和实例化 **CircularString**实例：  
  
```tsql  
DECLARE @g geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
```  
  
### F. 使用直线 CircularString 实例化一个几何图形实例  
 下面的示例演示如何创建一个直线 **CircularString** 实例：  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('CIRCULARSTRING(0 0, 1 2, 2 4)', 0);  
```  
  
## 另请参阅  
 [空间数据类型概述](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [CompoundCurve](../../relational-databases/spatial/compoundcurve.md)   
 [MakeValid（geography 数据类型）](../../t-sql/spatial-geography/makevalid-geography-data-type.md)   
 [MakeValid（geometry 数据类型）](../../t-sql/spatial-geometry/makevalid-geometry-data-type.md)   
 [STIsValid（geometry 数据类型）](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)   
 [STIsValid（geography 数据类型）](../../t-sql/spatial-geography/stisvalid-geography-data-type.md)   
 [STLength（geometry 数据类型）](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)   
 [STStartPoint（geometry 数据类型）](../../t-sql/spatial-geometry/ststartpoint-geometry-data-type.md)   
 [STEndpoint（geometry 数据类型）](../../t-sql/spatial-geometry/stendpoint-geometry-data-type.md)   
 [STPointN（geometry 数据类型）](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md)   
 [STNumPoints（geometry 数据类型）](../../t-sql/spatial-geometry/stnumpoints-geometry-data-type.md)   
 [STIsRing（geometry 数据类型）](../../t-sql/spatial-geometry/stisring-geometry-data-type.md)   
 [STIsClosed（geometry 数据类型）](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)   
 [STPointOnSurface（geometry 数据类型）](../../t-sql/spatial-geometry/stpointonsurface-geometry-data-type.md)   
 [LineString](../../relational-databases/spatial/linestring.md)  
  
  