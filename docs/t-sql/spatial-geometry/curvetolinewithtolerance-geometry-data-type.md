---
title: CurveToLineWithTolerance（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- CurveToLineWithTolerance method (geometry)
ms.assetid: 96871075-1998-4cd9-86b1-3fc55577aee4
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 30264ebeef5a398d677abbb2bc380a68c69893d4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65938127"
---
# <a name="curvetolinewithtolerance-geometry-data-type"></a>CurveToLineWithTolerance（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

返回包含圆弧线段的 geometry 实例的多边形近似值  。
  
## <a name="syntax"></a>语法  
  
```  
  
.CurveToLineWithTolerance ( tolerance, relative )  
```  
  
## <a name="arguments"></a>参数  
 tolerance   
 一个 double 表达式，它定义原始圆弧线段与其线性近似值之间的最大误差  。  
  
 *relative*  
 一个 bool 表达式，它指示是否使用偏差的相对最大值  。 如果将 relative 设置为 false (0)，则为可能具有线性近似值的偏差设置绝对最大值。 如果将 relative 设置为 true (1)，则按 tolerance 参数与空间对象边界框直径的乘积来计算公差。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geometry   
  
 CLR 返回类型：**SqlGeometry**  
  
## <a name="exceptions"></a>异常  
 设置 tolerance <= 0 将引发 `ArgumentOutOfRange` 异常。  
  
## <a name="remarks"></a>Remarks  
 此方法可以指定结果 LineString 的容错大小  。  
  
 下表显示了 `CurveToLineWithTolerance()` 为各种类型返回的实例类型。  
  
|调用实例类型|返回的空间类型|  
|----------------------------|---------------------------|  
|空 geometry 实例|空的 GeometryCollection 实例 |  
|Point 和 MultiPoint  |Point 实例 |  
|**MultiPoint**|Point 或 MultiPoint 实例  |  
|CircularString、CompoundCurve 或 LineString   |LineString 实例 |  
|**MultiLineString**|LineString 或 MultiLineString 实例  |  
|CurvePolygon 和 Polygon  |Polygon 实例 |  
|**MultiPolygon**|Polygon 或 MultiPolygon 实例  |  
|具有一个不包含圆弧线段的实例的 GeometryCollection |GeometryCollection 中包含的实例决定了返回的实例类型  。|  
|具有一个一维圆弧线段实例（CircularString、CompoundCurve）的 GeometryCollection   |LineString 实例 |  
|具有一个二维圆弧线段实例 (CurvePolygon) 的 GeometryCollection  |Polygon 实例 |  
|具有多个一维实例的 GeometryCollection |MultiLineString 实例 |  
|具有多个二维实例的 GeometryCollection |MultiPolygon 实例 |  
|具有多个不同维度的实例的 GeometryCollection |GeometryCollection 实例 |  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-different-tolerance-values-on-a-circularstring-instance"></a>A. 在 CircularString 实例上使用不同的公差值  
 以下示例说明设置容差如何影响从 `CircularString` 实例返回的 `LineString` 实例：  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)'); 
 SELECT @g.CurveToLineWithTolerance(0.1,0).STNumPoints(), @g.CurveToLineWithTolerance(0.01, 0).STNumPoints();
 ```  
  
### <a name="b-using-the-method-on-a-multilinestring-instance-containing-one-linestring"></a>B. 在包含一个 LineString 的 MultiLineString 实例上使用该方法  
 以下示例显示从仅包含一个 `MultiLineString` 实例的 `LineString` 实例中返回的内容：  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('MULTILINESTRING((1 3, 4 8, 6 9))'); 
 SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();
 ```  
  
### <a name="c-using-the-method-on-a-multilinestring-instance-containing-multiple-linestrings"></a>C. 在包含多个 LineString 的 MultiLineString 实例上使用该方法  
 以下示例显示从包含多个 `MultiLineString` 实例的 `LineString` 实例中返回的内容：  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('MULTILINESTRING((1 3, 4 8, 6 9),(4 4, 9 18))'); 
 SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();
 ```  
  
### <a name="d-setting-relative-to-true-for-an-invoking-curvepolygon-instance"></a>D. 对于调用 CurvePolygon 实例，将 relative 设置为 true  
 以下示例使用 `CurvePolygon` 实例调用 `CurveToLineWithTolerance()` 并将 relative 设置为 true  ：  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.CurveToLineWithTolerance(.5,1).ToString();
 ```  
  
### <a name="e-using-the-method-on-a-geometrycollection-instance"></a>E. 在 GeometryCollection 实例上使用该方法  
 以下示例在包含一个二维 `CurveToLineWithTolerance()` 实例和一个一维 `GeometryCollection` 实例的 `CurvePolygon` 上调用 `CircularString`。 `CurveToLineWithTolerance()` 将这两种圆弧线段类型转换为直线段类型，并以 `GeometryCollection` 类型返回它们。  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('GEOMETRYCOLLECTION(CURVEPOLYGON( COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), (4 2, 0 2))), CIRCULARSTRING(4 4, 8 6, 9 5))'); 
 SELECT @g.CurveToLineWithTolerance(0.1,0).STNumPoints(), @g.CurveToLineWithTolerance(0.1, 0).ToString();
 ```  
  
## <a name="see-also"></a>另请参阅  
 [CurveToLineWithTolerance（geography 数据类型）](../../t-sql/spatial-geography/curvetolinewithtolerance-geography-data-type.md)   
 [STCurveToLine（geometry 数据类型）](../../t-sql/spatial-geometry/stcurvetoline-geometry-data-type.md)  
  
  

