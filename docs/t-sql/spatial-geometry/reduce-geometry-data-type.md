---
title: "减少 (geometry 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Reduce_TSQL
- Reduce
dev_langs:
- TSQL
helpviewer_keywords:
- Reduce method
ms.assetid: 132184bf-c4d2-4a27-900d-8373445dce2a
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6e74a2a16806741dda7171ec0327b709fb697cb9
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="reduce-geometry-data-type"></a>Reduce（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回可大概了解给定**几何图形**实例生成的具有给定容差的实例上运行道格拉斯 • Peucker 算法的扩展。
  
## <a name="syntax"></a>语法  
  
```  
  
.Reduce ( tolerance )  
```  
  
## <a name="arguments"></a>参数  
 *容差*  
 是类型的值**float**。 *容差*是近似算法输入容差。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**几何图形**  
  
 CLR 返回类型： **SqlGeometry**  
  
## <a name="remarks"></a>注释  
 有关集合类型，此算法对独立每**几何图形**实例中包含。  
  
 此算法不会修改**点**实例。  
  
 上**LineString**， **CircularString**，和**CompoundCurve**情况下，近似算法保留原始的开始和结束点的实例，并以迭代方式添加回点从大多数偏离直到没有点结果超过给定容差偏离的原始实例。  
  
 `Reduce()`返回**LineString**， **CircularString**，或**CompoundCurve**实例**CircularString**实例。  `Reduce()`返回**CompoundCurve**或**LineString**实例**CompoundCurve**实例。  
  
 上**多边形**情况下，近似算法独立应用于每个环。 则此方法将生成`FormatException`如果返回**多边形**实例不是有效的; 例如，无效**MultiPolygon**如果创建实例`Reduce()`用于简化每环中实例，并生成环重叠。  上**CurvePolygon**实例外环和任何内部环，`Reduce()`返回**CurvePolygon**， **LineString**，或**点**实例。  如果**CurvePolygon**具有内部环则**CurvePolygon**或**MultiPoint**返回实例。  
  
 遇到圆弧段时，近似算法会检查是否可以通过在给定公差一半之内的弦来近似弧。  如果弦满足此条件，计算中会用该弦来替换圆弧。 如果弦不满足此条件，则保留圆弧，并将近似算法应用于其余的段。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-reduce-to-simplify-a-linestring"></a>A. 使用 Reduce() 简化 LineString  
 以下示例创建一个 `LineString` 实例，并使用 `Reduce()` 简化该实例。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 0 1, 1 0, 2 1, 3 0, 4 1)', 0);  
SELECT @g.Reduce(.75).ToString();  
```  
  
### <a name="b-using-reduce-with-varying-tolerance-levels-on-a-circularstring"></a>B. 对 CircularString 使用具有不同公差级别的 Reduce()  
 下面的示例使用`Reduce()`具有三个容差级别上**CircularString**实例：  
  
```
 DECLARE @g geometry = 'CIRCULARSTRING(0 0, 8 8, 16 0, 20 -4, 24 0)'; 
 SELECT @g.Reduce(5).ToString(); 
 SELECT @g.Reduce(15).ToString(); 
 SELECT @g.Reduce(16).ToString();
 ```  
  
 此示例生成以下输出：  
  
 ```
 CIRCULARSTRING (0 0, 8 8, 16 0, 20 -4, 24 0) 
 COMPOUNDCURVE (CIRCULARSTRING (0 0, 8 8, 16 0), (16 0, 24 0)) 
 LINESTRING (0 0, 24 0)
 ```  
  
 返回的每个实例都包含端点 (0 0) 和 (24 0)。  
  
### <a name="c-using-reduce-with-varying-tolerance-levels-on-a-compoundcurve"></a>C. 对 CompoundCurve 使用具有不同公差级别的 Reduce()  
 下面的示例使用`Reduce()`具有两个容差级别上**CompoundCurve**实例：  
  
```
 DECLARE @g geometry = 'COMPOUNDCURVE(CIRCULARSTRING(0 0, 8 8, 16 0, 20 -4, 24 0),(24 0, 20 4, 16 0))';  
 SELECT @g.Reduce(15).ToString();  
 SELECT @g.Reduce(16).ToString();
 ```  
  
 在此示例中请注意，第二个**选择**语句返回**LineString**实例： `LineString(0 0, 16 0)`。  
  
### <a name="showing-an-example-where-the-original-start-and-end-points-are-lost"></a>显示原始起点和终点丢失的示例  
 下面的示例演示生成的实例为何无法保留原始的起点和终点。 这是因为保留原始的开始和结束点将导致无效**LineString**实例。  
  
```  
DECLARE @g geometry = 'LINESTRING(0 0, 4 0, 2 .01, 1 0)';  
DECLARE @h geometry = @g.Reduce(1);  
SELECT @g.STIsValid() AS Valid  
SELECT @g.ToString() AS Original, @h.ToString() AS Reduced;  
```  
  
## <a name="see-also"></a>另请参阅  
 [扩展静态几何图形方法](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  


