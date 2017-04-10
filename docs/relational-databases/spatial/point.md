---
title: "点 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-spatial"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Point 几何图形子类型 [SQL Server]"
  - "geometry 数据类型 [SQL Server], 空间数据"
ms.assetid: 2a596ec4-8b2f-4962-bcb4-e5c8f77edad5
caps.latest.revision: 19
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 19
---
# 点
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 空间数据中，**Point** 是表示单个位置的零维对象，可能包含 Z（仰角）和 M（度量）值。  
  
## Geography 数据类型  
 Geography 数据类型的 Point 类型表示单个位置，其中 *Lat* 表示纬度， *Long* 表示经度。 维度和经度值以度数进行衡量。 纬度值始终处于间隔 [-90, 90] 内，如果输入的值超出此范围，将引发异常。 经度值始终处于间隔 (-180, 180] 内，如果输入的值超出此范围，将对值进行回绕以便适合此范围。 例如，如果为经度值输入 190，则该值将被回绕到值 -170。 *SRID* 表示您希望返回的 **geography** 实例的空间引用 ID。  
  
## Geometry 数据类型  
 Geometry 数据类型的 Point 类型表示单个位置，其中 *X* 表示要生成的点的 X 坐标，*Y* 表示要生成的点的 Y 坐标。 *SRID* 表示您希望返回的 **geometry** 实例的空间引用 ID。  
  
## 示例  
 下面的示例创建一个表示点 (3, 4) 的 `geometry Point` 实例，该实例的 SRID 为 0。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT (3 4)', 0);  
```  
  
 下一个示例创建一个表示点 (3, 4) 的 `geometry``Point` 实例，该实例的 Z（仰角）值为 7，M（度量）值为 2.5，默认 SRID 为 0。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('POINT(3 4 7 2.5)');  
```  
  
 最后一个示例返回 `geometry``Point` 实例的 X、Y、Z 和 M 值。  
  
```  
SELECT @g.STX;  
SELECT @g.STY;  
SELECT @g.Z;  
SELECT @g.M;  
```  
  
 Z 和 M 值可以显式指定为 NULL，如下例所示。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('POINT(3 4 NULL NULL)');  
```  
  
## 另请参阅  
 [MultiPoint](../../relational-databases/spatial/multipoint.md)   
 [STX（geometry 数据类型）](../../t-sql/spatial-geometry/stx-geometry-data-type.md)   
 [STY（geometry 数据类型）](../../t-sql/spatial-geometry/sty-geometry-data-type.md)   
 [空间数据 (SQL Server)](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  