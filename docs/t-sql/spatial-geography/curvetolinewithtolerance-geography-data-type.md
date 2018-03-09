---
title: "CurveToLineWithTolerance (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CurveToLineWithTolerance_TSQL
- CurveToLineWithTolerance
dev_langs:
- TSQL
helpviewer_keywords:
- CurveToLineWithTolerance method (geography)
ms.assetid: 74369c76-2cf6-42ae-b9cc-e7a051db2767
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 208878805dcf7c812caa1e6fb4f06120431ad803
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="curvetolinewithtolerance-geography-data-type"></a>CurveToLineWithTolerance（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  返回多边形的近似**geography**包含条圆弧线段实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
.CurveToLineWithTolerance( tolerance, relative )  
```  
  
## <a name="arguments"></a>参数  
 *tolerance*  
 是**double**定义原始条圆弧线段和其线性近似值之间的最大错误的表达式。  
  
 *relative*  
 是**bool** ，该值指示是否使用相对的最大偏差的表达式。 如果将 relative 设置为 false (0)，则为可能具有线性近似值的偏差设置绝对最大值。  如果将 relative 设置为 true (1)，则按 tolerance 参数与空间对象边界框直径的乘积来计算公差。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**地理位置**  
  
 CLR 返回类型： **SqlGeography**  
  
## <a name="exceptions"></a>异常  
 设置容差 < = 0 引发**ArgumentOutOfRange**异常。  
  
## <a name="remarks"></a>注释  
 此方法允许对要为所产生的指定错误容差量**LineString**。  
  
 **CurveToLineWithTolerance**方法将返回**LineString**实例**CircularString**或**CompoundCurve**实例和**多边形**实例**CurvePolygon**实例。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-different-tolerance-values-on-a-circularstring-instance"></a>A. 在 CircularString 实例上使用不同的公差值  
 下面的示例演示如何设置容差影响`LineString`从返回的实例`CircularString`实例：  
  
 ```
 DECLARE @g geography;  
 SET @g = geography::Parse('CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)');  
 SELECT @g.CurveToLineWithTolerance(0.1,0).STNumPoints(), @g.CurveToLineWithTolerance(0.01, 0).STNumPoints();
```  
  
### <a name="b-using-the-method-on-a-multilinestring-instance-containing-one-linestring"></a>B. 在包含一个 LineString 的 MultiLineString 实例上使用该方法  
 以下示例显示从仅包含一个 `MultiLineString` 实例的 `LineString` 实例中返回的内容：  
  
 ```
 DECLARE @g geography;  
 SET @g = geography::Parse('MULTILINESTRING((-122.358 47.653, -122.348 47.649))');  
 SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();
 ```  
  
### <a name="c-using-the-method-on-a-multilinestring-instance-containing-multiple-linestrings"></a>C. 在包含多个 LineString 的 MultiLineString 实例上使用该方法  
 以下示例显示从包含多个 `MultiLineString` 实例的 `LineString` 实例中返回的内容：  
  
 ```
 DECLARE @g geography;  
 SET @g = geography::Parse('MULTILINESTRING((-122.358 47.653, -122.348 47.649),(-123.358 47.653, -123.348 47.649))');  
 SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();
 ```  
  
### <a name="d-setting-relative-to-true-for-an-invoking-curvepolygon-instance"></a>D. 对于调用 CurvePolygon 实例，将 relative 设置为 true  
 下面的示例使用`CurvePolygon`实例来调用`CurveToLineWithTolerance()`与*相对*设置为 true:  
  
 ```
 DECLARE @g geography = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658), (-122.348 47.658, -122.358 47.658, -122.358 47.653)))';  
 SELECT @g.CurveToLineWithTolerance(.5,1).ToString();
 ```  
  
## <a name="see-also"></a>另请参阅  
 [地理实例上的扩展方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
