---
title: STIntersection（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIntersection_TSQL
- STIntersection (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIntersection (geometry Data Type)
ms.assetid: 354843f5-cc14-478c-974a-04f363f9530f
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 63edfe76d39fe00c01134e79b34511b78fe5984a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762440"
---
# <a name="stintersection-geometry-data-type"></a>STIntersection（geometry 数据类型）
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

返回一个对象，它表示一个 **geometry** 实例与另一个 **geometry** 实例的交点。
  
## <a name="syntax"></a>语法  
  
```  
  
.STIntersection ( other_geometry )  
```  
  
## <a name="arguments"></a>参数  
 *other_geometry*  
 将与调用 `STIntersection()` 的实例进行比较的另一个 **geometry** 实例，进行比较的目的是确定这两个实例是否相交。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geometry   
  
 CLR 返回类型：SqlGeometry   
  
## <a name="remarks"></a>备注  
 如果 **geometry** 实例的空间引用 ID (SRID) 不匹配，则 `STIntersection()` 始终返回 null。 只有在输入实例包含它们时，结果才可能包含圆弧段。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-stintersection-on-polygon-instances"></a>A. 对 Polygon 实例使用 STIntersection()  
 下面的示例使用 `STIntersection()` 计算两个多边形的交点。  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 2 2, 2 0, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STIntersection(@h).ToString();  
```  
  
### <a name="b-using-stintersection-with-curvepolygon-instance"></a>B. 对 CurvePolygon 实例使用 STIntersection()  
 以下示例返回一个包含圆弧线段的实例。  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON (CIRCULARSTRING (0 -4, 4 0, 0 4, -4 0, 0 -4))';  
 DECLARE @h geometry = 'POLYGON ((1 -1, 5 -1, 5 3, 1 3, 1 -1))';  
 SELECT @h.STIntersection(@g).ToString();
 ```  
  
## <a name="see-also"></a>另请参阅  
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

