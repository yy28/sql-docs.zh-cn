---
title: LineString | Microsoft Docs
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- LineString geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: e50d0b86-8b31-4285-be71-ad05c7712cbd
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 543e248f19e76b0d2caca3ee595778fe430334ea
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58531879"
---
# <a name="linestring"></a>LineString
  `LineString` 是一个一维对象，表示一系列点和连接这些点的线段。  
  
## <a name="linestring-instances"></a>LineString 实例  
 下图显示了 `LineString` 实例的示例。  
  
 ![几何 LineString 实例的示例](../../database-engine/media/linestring.gif "几何 LineString 实例的示例")  
  
 如图中所示：  
  
-   图 1 显示的是一个简单、非闭合的 `LineString` 实例。  
  
-   图 2 显示的是一个不简单、非闭合的 `LineString` 实例。  
  
-   图 3 显示的是一个闭合、简单的 `LineString` 实例，因此是一个环。  
  
-   图 4 显示的是一个闭合、不简单的 `LineString` 实例，因此不是一个环。  
  
### <a name="accepted-instances"></a>已接受的实例  
 可以将已接受的 `LineString` 实例输入到一个几何图形变量中，但它们可能不是有效的 `LineString` 实例。 必须满足以下条件，`LineString` 实例才能被接受。 该实例必须由至少两个点组成，或者该实例必须为空。 下面是一些已接受的 LineString 实例。  
  
```  
DECLARE @g1 geometry = 'LINESTRING EMPTY';  
DECLARE @g2 geometry = 'LINESTRING(1 1,2 3,4 8, -6 3)';  
DECLARE @g3 geometry = 'LINESTRING(1 1, 1 1)';  
```  
  
 `@g3` 显示 `LineString` 实例可被接受，但无效。  
  
 下面的 `LineString` 实例不可接受。 它将引发 `System.FormatException`。  
  
```  
DECLARE @g geometry = 'LINESTRING(1 1)';  
```  
  
### <a name="valid-instances"></a>有效实例  
 必须满足以下条件，`LineString` 实例才是有效的。  
  
1.  `LineString` 实例必须是已接受的实例。  
  
2.  如果 `LineString` 实例不为空，则它必须包含至少两个非重复点。  
  
3.  在两个或更多连续点的间隔范围内，`LineString` 实例不能自身重叠。  
  
 以下是有效的 `LineString` 实例。  
  
```  
DECLARE @g1 geometry= 'LINESTRING EMPTY';  
DECLARE @g2 geometry= 'LINESTRING(1 1, 3 3)';  
DECLARE @g3 geometry= 'LINESTRING(1 1, 3 3, 2 4, 2 0)';  
DECLARE @g4 geometry= 'LINESTRING(1 1, 3 3, 2 4, 2 0, 1 1)';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
  
```  
  
 以下是无效的 `LineString` 实例。  
  
```  
DECLARE @g1 geometry = 'LINESTRING(1 4, 3 4, 2 4, 2 0)';  
DECLARE @g2 geometry = 'LINESTRING(1 1, 1 1)';  
SELECT @g1.STIsValid(), @g2.STIsValid();  
```  
  
> [!WARNING]  
>  `LineString` 重叠的检测基于不精确的浮点计算。  
  
## <a name="examples"></a>示例  
 下面的示例说明如何创建一个包含三个点且 SRID 为 0 的 `geometry``LineString` 实例：  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(1 1, 2 4, 3 9)', 0);  
```  
  
 此 `LineString` 实例中的每个点都可以包含 Z（仰角）和 M（度量）值。 下面这个示例向上例中创建的 `LineString` 实例添加了 M 值。 M 和 Z 可以为 Null 值。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(1 1 NULL 0, 2 4 NULL 12.3, 3 9 NULL 24.5)', 0);  
```  
  
 下面的示例说明如何创建一个包含两个相同点的 `geometry LineString` 实例。 对 `IsValid` 的调用指示 `LineString` 实例无效，并且对 `MakeValid` 的调用会将 `LineString` 实例转换为 `Point`。  
  
```sql  
DECLARE @g geometry  
SET @g = geometry::STGeomFromText('LINESTRING(1 3, 1 3)',0);  
IF @g.STIsValid() = 1  
  BEGIN  
     SELECT @g.ToString() + ' is a valid LineString.';    
  END  
ELSE  
  BEGIN  
     SELECT @g.ToString() + ' is not a valid LineString.';  
     SET @g = @g.MakeValid();  
     SELECT @g.ToString() + ' is a valid Point.';    
  END  
  
```  
  
 上面的代码段将返回以下结果：  
  
```  
LINESTRING(1 3, 1 3) is not a valid LineString  
POINT(1 3) is a valid Point.  
```  
  
## <a name="see-also"></a>请参阅  
 [STLength（geometry 数据类型）](/sql/t-sql/spatial-geometry/stlength-geometry-data-type)   
 [STStartPoint（geometry 数据类型）](/sql/t-sql/spatial-geometry/ststartpoint-geometry-data-type)   
 [STEndpoint（geometry 数据类型）](/sql/t-sql/spatial-geometry/stendpoint-geometry-data-type)   
 [STPointN（geometry 数据类型）](/sql/t-sql/spatial-geometry/stpointn-geometry-data-type)   
 [STNumPoints（geometry 数据类型）](/sql/t-sql/spatial-geometry/stnumpoints-geometry-data-type)   
 [STIsRing（geometry 数据类型）](/sql/t-sql/spatial-geometry/stisring-geometry-data-type)   
 [STIsClosed（geometry 数据类型）](/sql/t-sql/spatial-geometry/stisclosed-geometry-data-type)   
 [STPointOnSurface（geometry 数据类型）](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)   
 [空间数据 (SQL Server)](../spatial/spatial-data-sql-server.md)  
  
  
