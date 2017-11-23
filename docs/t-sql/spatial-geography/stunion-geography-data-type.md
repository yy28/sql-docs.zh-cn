---
title: "STUnion (geography 数据类型) |Microsoft 文档"
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
- STUnion (geography Data Type)
- STUnion_TSQL
dev_langs: TSQL
helpviewer_keywords: STUnion method
ms.assetid: 9bf87691-efd8-4c53-bd2f-eefe0acd19ca
caps.latest.revision: "23"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: de8c86b99b040c23347ccc8618d8a8bef999d747
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="stunion-geography-data-type"></a>STUnion（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回一个对象，表示同时兼具**geography**与另一个实例**geography**实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STUnion ( other_geography )  
```  
  
## <a name="arguments"></a>参数  
 *other_geography*  
 是另一种**geography**实例以形成具有对其调用则的实例的联合。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**地理位置**  
  
 CLR 返回类型： **SqlGeography**  
  
## <a name="exceptions"></a>异常  
 此方法将引发**ArgumentException**如果实例包含对跖边缘。  
  
## <a name="remarks"></a>注释  
 如果此方法将始终返回 null 的空间引用标识符 (Srid) **geography**实例不匹配。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持大于半球的空间实例。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，可能返回的结果集在服务器上已扩展到**FullGlobe**实例。  
  
 只有在输入实例包含圆弧线段时，结果才会包含圆弧线段。  
  
 此方法不精确。  
  
## <a name="examples"></a>示例  
  
### <a name="a-computing-the-union-of-two-polygons"></a>A. 计算两个多边形的并集  
 以下示例使用 `STUnion()` 计算两个 `Polygon` 实例的并集。  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SET @h = geography::STGeomFromText('POLYGON((-122.351 47.656, -122.341 47.656, -122.341 47.661, -122.351 47.661, -122.351 47.656))', 4326);  
SELECT @g.STUnion(@h).ToString();  
```  
  
### <a name="b-producing-a-fullglobe-result"></a>B. 生成 FullGlobe 结果  
 以下示例在 `FullGlobe` 合并两个 `STUnion()` 实例时生成 `Polygon`。  
  
```
 DECLARE @g geography = 'POLYGON ((-122.358 47.653, -122.358 47.658,-122.348 47.658, -122.348 47.649, -122.358 47.653))';  
 DECLARE @h geography = 'POLYGON ((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STUnion(@h).ToString();
 ```  
  
### <a name="c-producing-a-triagonal-hole-from-a-union-of-a-curvepolygon-and-a-traigonal-hole"></a>C. 通过 CurvePolygon 和 Polygon 的并集生成一个三角形孔。  
 以下示例通过 `CurvePolygon` 和 `Polygon` 实例的并集生成一个三角形孔。  
  
```
 DECLARE @g geography = 'POLYGON ((-0.5 0, 0 1, 0.5 0.5, -0.5 0))';  
 DECLARE @h geography = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 0, 0.7 0.7, 0 1), (0 1, 0 0)))';  
 SELECT @g.STUnion(@h).ToString();
 ```  
  
## <a name="see-also"></a>另请参阅  
 [地理实例上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
