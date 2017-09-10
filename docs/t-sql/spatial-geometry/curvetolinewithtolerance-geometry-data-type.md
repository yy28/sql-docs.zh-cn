---
title: "CurveToLineWithTolerance (geometry 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- CurveToLineWithTolerance method (geometry)
ms.assetid: 96871075-1998-4cd9-86b1-3fc55577aee4
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5120f9c27e6157fd2f19c598ad984e1a3543db94
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="curvetolinewithtolerance-geometry-data-type"></a>CurveToLineWithTolerance（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

返回多边形的近似**几何图形**包含条圆弧线段实例。
  
## <a name="syntax"></a>语法  
  
```  
  
.CurveToLineWithTolerance ( tolerance, relative )  
```  
  
## <a name="arguments"></a>参数  
 *容差*  
 是**double**定义原始条圆弧线段和其线性近似值之间的最大错误的表达式。  
  
 *相对*  
 是**bool**表达式，该值指示是否使用相对的最大偏差。 如果将 relative 设置为 false (0)，则为可能具有线性近似值的偏差设置绝对最大值。 如果将 relative 设置为 true (1)，则按 tolerance 参数与空间对象边界框直径的乘积来计算公差。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**几何图形**  
  
 CLR 返回类型： **SqlGeometry**  
  
## <a name="exceptions"></a>异常  
 设置 tolerance <= 0 将引发 `ArgumentOutOfRange` 异常。  
  
## <a name="remarks"></a>注释  
 此方法可指定所产生的错误容差金额**LineString**。  
  
 下表显示了 `CurveToLineWithTolerance()` 为各种类型返回的实例类型。  
  
|调用实例类型|返回的空间类型|  
|----------------------------|---------------------------|  
|空 geometry 实例|空**GeometryCollection**实例|  
|**点**和**MultiPoint**|**点**实例|  
|**MultiPoint**|**点**或**MultiPoint**实例|  
|**CircularString**， **CompoundCurve**，或**LineString**|**LineString**实例|  
|**MultiLineString**|**LineString**或**MultiLineString**实例|  
|**CurvePolygon**和**多边形**|**多边形**实例|  
|**MultiPolygon**|**多边形**或**MultiPolygon**实例|  
|**GeometryCollection**与不包含条圆弧线段的单个实例|中包含的实例**GeometryCollection**确定返回的实例的类型。|  
|**GeometryCollection**与一维条圆弧线段实例 (**CircularString**， **CompoundCurve**)|**LineString**实例|  
|**GeometryCollection**与二维条圆弧线段实例 (**CurvePolygon**)|**多边形**实例|  
|**GeometryCollection**使用多个一维实例|**MultiLineString**实例|  
|**GeometryCollection**与多个两维实例|**MultiPolygon**实例|  
|**GeometryCollection**不同维度的多个实例|**GeometryCollection**实例|  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-different-tolerance-values-on-a-circularstring-instance"></a>A. 在 CircularString 实例上使用不同的公差值  
 下面的示例演示如何设置容差影响`LineString`从返回的实例`CircularString`实例：  
  
 `DECLARE @g geometry;`  
  
 `SET @g = geometry::Parse('CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)');`  
  
 `SELECT @g.CurveToLineWithTolerance(0.1,0).STNumPoints(), @g.CurveToLineWithTolerance(0.01, 0).STNumPoints();`  
  
### <a name="b-using-the-method-on-a-multilinestring-instance-containing-one-linestring"></a>B. 在包含一个 LineString 的 MultiLineString 实例上使用该方法  
 以下示例显示从仅包含一个 `MultiLineString` 实例的 `LineString` 实例中返回的内容：  
  
 `DECLARE @g geometry;`  
  
 `SET @g = geometry::Parse('MULTILINESTRING((1 3, 4 8, 6 9))');`  
  
 `SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();`  
  
### <a name="c-using-the-method-on-a-multilinestring-instance-containing-multiple-linestrings"></a>C. 在包含多个 LineString 的 MultiLineString 实例上使用该方法  
 以下示例显示从包含多个 `MultiLineString` 实例的 `LineString` 实例中返回的内容：  
  
 `DECLARE @g geometry;`  
  
 `SET @g = geometry::Parse('MULTILINESTRING((1 3, 4 8, 6 9),(4 4, 9 18))');`  
  
 `SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();`  
  
### <a name="d-setting-relative-to-true-for-an-invoking-curvepolygon-instance"></a>D. 对于调用 CurvePolygon 实例，将 relative 设置为 true  
 下面的示例使用`CurvePolygon`实例来调用`CurveToLineWithTolerance()`与*相对*设置为 true:  
  
 `DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))';`  
  
 `SELECT @g.CurveToLineWithTolerance(.5,1).ToString();`  
  
### <a name="e-using-the-method-on-a-geometrycollection-instance"></a>E. 在 GeometryCollection 实例上使用该方法  
 以下示例在包含一个二维 `CurveToLineWithTolerance()` 实例和一个一维 `GeometryCollection` 实例的 `CurvePolygon` 上调用 `CircularString`。 `CurveToLineWithTolerance()` 将这两种圆弧线段类型转换为直线段类型，并以 `GeometryCollection` 类型返回它们。  
  
 `DECLARE @g geometry;`  
  
 `SET @g = geometry::Parse('GEOMETRYCOLLECTION(CURVEPOLYGON( COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), (4 2, 0 2))), CIRCULARSTRING(4 4, 8 6, 9 5))');`  
  
 `SELECT @g.CurveToLineWithTolerance(0.1,0).STNumPoints(), @g.CurveToLineWithTolerance(0.1, 0).ToString();`  
  
## <a name="see-also"></a>另请参阅  
 [CurveToLineWithTolerance &#40; geography 数据类型 &#41;](../../t-sql/spatial-geography/curvetolinewithtolerance-geography-data-type.md)   
 [STCurveToLine &#40; geometry 数据类型 &#41;](../../t-sql/spatial-geometry/stcurvetoline-geometry-data-type.md)  
  
  


