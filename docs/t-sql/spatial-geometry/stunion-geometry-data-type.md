---
title: STUnion（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STUnion (geometry Data Type)
- STUnion_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STUnion (geometry Data Type)
ms.assetid: 5b168118-137d-402f-9173-fee3f365a89c
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8ad0a956d1b23a61327159a0d103d8a5cbbec965
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36243069"
---
# <a name="stunion-geometry-data-type"></a>STUnion（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

返回一个对象，它表示一个 **geometry** 实例与另一个 **geometry** 实例的并集。
  
## <a name="syntax"></a>语法  
  
```  
  
.STUnion ( other_geometry )  
```  
  
## <a name="arguments"></a>参数  
 *other_geometry*  
 与调用 `STUnion()` 的实例形成并集的另一个 **geometry** 实例。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geometry  
  
 CLR 返回类型：SqlGeometry  
  
## <a name="remarks"></a>Remarks  
 如果 geometry 实例的空间引用 ID (SRID) 不匹配，则此方法始终返回 null。 只有在输入实例包含圆弧线段时，结果才会包含圆弧线段。  
  
## <a name="examples"></a>示例  
  
### <a name="a-computing-the-union-of-two-polygon-instances"></a>A. 计算两个 Polygon 实例的并集  
 以下示例使用 `STUnion()` 计算两个 `Polygon` 实例的并集。  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 2 2, 2 0, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STUnion(@h).ToString();  
```  
  
### <a name="b-computing-the-union-of-a-polygon-instance-with-a-curvepolygon-instance"></a>B. 计算 Polygon 实例与 CurvePolygon 实例的并集  
 以下示例返回一个包含圆弧段的 `GeometryCollection` 实例。  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(CIRCULARSTRING(0 -4, 4 0, 0 4, -4 0, 0 -4))';  
 DECLARE @h geometry = 'POLYGON((5 -1, 5 -3, 7 -3, 7 -1, 5 -1))';  
 SELECT @g.STUnion(@h).ToString();
 ```  
  
 由于调用 `STUnion()` 的实例包含圆弧段，因此 `STUnion()` 返回包含圆弧段的结果。  
  
## <a name="see-also"></a>另请参阅  
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

