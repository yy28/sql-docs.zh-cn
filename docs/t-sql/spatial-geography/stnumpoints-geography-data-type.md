---
title: "STNumPoints (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STNumPoints (geography Data Type)
- STNumPoints_TSQL
dev_langs: TSQL
helpviewer_keywords: STNumPoints method
ms.assetid: 25ff7ad1-ba5f-4cfb-816a-59255ac1591d
caps.latest.revision: "21"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5195cac2dd616a7ae83515d3f3ae4e7ef832ebf6
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="stnumpoints-geography-data-type"></a>STNumPoints（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  每个中的图表中返回的点总数**geography**实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STNumPoints ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型： **int**  
  
 CLR 返回类型： **SqlInt32**  
  
## <a name="remarks"></a>注释  
 此方法计算中的说明的点**geography**实例。 重复的点被计算在内；但是，段之间的连接点只计算一次。 如果此实例为集合，则此方法将返回该集合内的总点数。  
  
## <a name="examples"></a>示例  
  
### <a name="a-retrieving-the-total-number-of-points-in-a-linestring"></a>A. 检索 LineString 中的总点数  
 下面的示例创建一个 `LineString` 实例，并使用 `STNumPoints()` 确定该实例说明中使用的点数。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STNumPoints();  
```  
  
### <a name="b-retrieving-the-total-number-of-points-in-a-geometrycollection"></a>B. 检索 GeometryCollection 中的总点数  
 以下示例返回 `GeometryCollection` 中的所有元素的点数之和。  
  
```  
DECLARE @g geography = 'GEOMETRYCOLLECTION(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)  
    ,CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)))';  
SELECT @g.STNumPoints();  
```  
  
### <a name="c-returning-the-number-of-points-in-a-compoundcurve"></a>C. 返回 CompoundCurve 中的点数  
 以下示例返回 CompoundCurve 实例中的点数。 由于 STNumPoints() 只对线段之间的连接点计数一次，因此查询将返回 5，而不是 6。  
  
```
 DECLARE @g geography = 'COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658),( -122.348 47.658, -121.56 48.12, -122.358 47.653))'  
 SELECT @g.STNumPoints();
 ```  
  
## <a name="see-also"></a>另请参阅  
 [地理实例上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
