---
title: "STCurveN (geometry 数据类型) |Microsoft 文档"
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
- STCurveN method (geometry)
ms.assetid: 64adf1a1-3a41-41fb-b7d1-44390c3e4ea9
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dd5b459bfa271d98844d30455e4e1a9e03d0e2cd
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="stcurven-geometry-data-type"></a>STCurveN（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

返回从指定的曲线**几何图形**实例，它是**LineString**， **CircularString**， **CompoundCurve**，或**MultiLineString**。
  
## <a name="syntax"></a>语法  
  
```  
  
.STCurveN ( curve_index )  
```  
  
## <a name="arguments"></a>参数  
 *curve_index*  
 是**int**介于 1 和中的曲线数之间的表达式**几何图形**实例。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**几何图形**  
  
 CLR 返回类型： **SqlGeometry**  
  
## <a name="exceptions"></a>异常  
 如果*curve_index* < 1 则`ArgumentOutOfRangeException`引发。  
  
## <a name="remarks"></a>注释  
 **NULL**时返回发生以下任一情况：  
  
-   **几何图形**实例已声明，但未实例化  
  
-   **几何图形**实例为空  
  
-   *curve_index*超过中的曲线数目**几何图形**实例  
  
-   **几何图形**实例是**点**， **MultiPoint**，**多边形**， **CurvePolygon**，或**MultiPolygon**  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-stcurven-on-a-circularstring-instance"></a>A. 在 CircularString 实例上使用 STCurveN()  
 以下示例返回 `CircularString` 实例中的第二条曲线：  
  
 `DECLARE @g geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';`  
  
 `SELECT @g.STCurveN(2).ToString();`  
  
 本主题前面的示例返回：  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
### <a name="b-using-stcurven-on-a-compoundcurve-instance-with-one-circularstring-instance"></a>B. 在具有一个 CircularString 实例的 CompoundCurve 实例上使用 STCurveN()  
 以下示例返回 `CompoundCurve` 实例中的第二条曲线：  
  
 `DECLARE @g geometry = 'COMPOUNDCURVE(CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0))';`  
  
 `SELECT @g.STCurveN(2).ToString();`  
  
 本主题前面的示例返回：  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
### <a name="c-using-stcurven-on-a-compoundcurve-instance-with-three-circularstring-instances"></a>C. 在具有三个 CircularString 实例的 CompoundCurve 实例上使用 STCurveN()  
 以下示例使用 `CompoundCurve` 实例，该实例将三个单独的 `CircularString` 实例合并为与上一示例相同的曲线序列：  
  
 `DECLARE @g geometry = 'COMPOUNDCURVE (CIRCULARSTRING (0 0, 1 2.1082, 3 6.3246), CIRCULARSTRING(3 6.3246, 0 7, -3 6.3246), CIRCULARSTRING(-3 6.3246, -1 2.1082, 0 0))';`  
  
 `SELECT @g.STCurveN(2).ToString();`  
  
 本主题前面的示例返回：  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
 请注意，前面的三个示例的结果是相同的。 无论使用哪种 WKT（熟知文本）格式输入相同的曲线序列，在使用 `STCurveN()` 实例时，`CompoundCurve` 返回的结果都是相同的。  
  
### <a name="d-validating-the-parameter-before-calling-stcurven"></a>D. 在调用 STCurveN() 之前验证参数  
 下面的示例演示如何确保`@n`是否有效，然后才能调用`STCurveN()`方法：  
  
 `DECLARE @g geometry;`  
  
 `DECLARE @n int;`  
  
 `SET @n = 3;`  
  
 `SET @g = geometry::Parse('CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)');`  
  
 `IF @n >= 1 AND @n <= @g.STNumCurves()`  
  
 `BEGIN`  
  
 `SELECT @g.STCurveN(@n).ToString();`  
  
 `END`  
  
## <a name="see-also"></a>另请参阅  
 [STNumCurves &#40; geometry 数据类型 &#41;](../../t-sql/spatial-geometry/stnumcurves-geometry-data-type.md)   
 [在几何图形实例的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


