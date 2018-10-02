---
title: STSymDifference（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STSymDifference_TSQL
- STSymDifference (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STSymDifference (geometry Data Type)
ms.assetid: 1d4cf35a-ca89-4aa4-ae30-e61a0ff18b53
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6625ea3cbd43996eda702832774220c35646f1ec
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47621105"
---
# <a name="stsymdifference-geometry-data-type"></a>STSymDifference（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  返回一个对象，它表示位于一个 **geometry** 实例或另一个 **geometry** 实例中的所有点，但不包含同时位于这两个实例中的点。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STSymDifference ( other_geometry )  
```  
  
## <a name="arguments"></a>参数  
 *other_geometry*  
 调用 `STSymDistance()` 的实例以外的另一个 **geometry** 实例。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geometry  
  
 CLR 返回类型：SqlGeometry  
  
## <a name="remarks"></a>Remarks  
 如果 geometry 实例的空间引用 ID (SRID) 不匹配，则此方法始终返回 null。 只有在输入实例包含圆弧线段时，结果才会包含圆弧线段。  
  
## <a name="examples"></a>示例  
  
### <a name="a-computing-the-symmetric-difference-of-two-polygon-instances"></a>A. 计算两个 Polygon 实例的余集  
 以下示例使用 `STSymDifference()` 计算两个 `Polygon` 实例的余集。  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 2 2, 2 0, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STSymDifference(@h).ToString();  
```  
  
### <a name="b-computing-the-symmetric-difference-between-a-curvepolygon-and-a-polygon-instance"></a>B. 计算 CurvePolygon 和 Polygon 实例之间的余集  
 下面的示例返回一个表示 `GeometryCollection` 和 `CurvePolygon` 之间余集的 `Polygon`。  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON (CIRCULARSTRING (0 -4, 4 0, 0 4, -4 0, 0 -4))';  
 DECLARE @h geometry = 'POLYGON ((1 -1, 5 -1, 5 3, 1 3, 1 -1))';  
 SELECT @h.STSymDifference(@g).ToString();
 ```  
  
## <a name="c-using-stsymdifference-on-curvepolygon-instance-with-an-inscribed-polygon-instance"></a>C. 对 CurvePolygon 实例和内切的 Polygon 实例使用 STSymDifference()  
 下面的示例返回一个具有内部 `CurvePolygon` 环的 `Polygon` 实例，该实例表示比较的两个实例的余集。  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON (CIRCULARSTRING (0 -4, 4 0, 0 4, -4 0, 0 -4))';  
 DECLARE @h geometry = 'POLYGON ((1 -1, 2 -1, 2 1, 1 1, 1 -1))';  
 SELECT @h.STSymDifference(@g).ToString();
 ```  
  
## <a name="see-also"></a>另请参阅  
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
