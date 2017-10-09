---
title: "BufferWithCurves (geometry 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
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
- BufferWithCurves method (geometry)
ms.assetid: 8ffaba3f-d2dd-4e57-9f41-3ced9f14b600
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a88ea4010ec1cfd48661b34e990634fe371141f3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="bufferwithcurves-geometry-data-type"></a>BufferWithCurves（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  返回**几何图形**表示的所有组的实例中调用的点的距离**几何图形**实例小于或等于*距离*参数。  
  
## <a name="syntax"></a>语法  
  
```  
  
.BufferWithCurves ( distance )  
```  
  
## <a name="arguments"></a>参数  
 *距离*  
 是**float** ，表示点构成缓冲区的最大距离可以来自**几何图形**实例。  
  
## <a name="return-types"></a>返回类型  
SQL Server 返回类型：**几何图形**  
  
 CLR 返回类型： **SqlGeometry**  
  
## <a name="exceptions"></a>异常  
 以下条件将引发**ArgumentException**。  
  
-   无参数传递给方法如`@g.BufferWithCurves()`  
  
-   非数字参数被传递给方法如`@g.BufferWithCurves('a')`  
  
-   **NULL**传递给方法，如`@g.BufferWithCurves(NULL)`  
  
## <a name="remarks"></a>注释  
 下图显示此方法返回的示例 geometry 实例。  
  
 ![BufferedCurve](../../t-sql/spatial-geometry/media/bufferedcurve.gif)
  
 下表显示为不同距离值返回的结果。  
  
|距离值|类型维度|返回的空间类型|  
|--------------------|---------------------|---------------------------|  
|距离 < 0|0 或 1|空**GeometryCollection**实例|  
|距离 < 0|2 或更大|A **CurvePolygon**或**GeometryCollection**与负缓冲区的实例。 **注意：**负缓冲区可能创建一个空**GeometryCollection**|  
|距离 = 0|所有维度|调用的复制**几何图形**实例|  
|距离 > 0|所有维度|**CurvePolygon**或**GeometryCollection**实例|  
  
> [!NOTE]  
>  由于*距离*是**float**，可以相当非常小的值为零的计算中。 在这种情况然后一份调用**几何图形**返回实例。 请参阅[float 和 real &#40;Transact SQL &#41;](../../t-sql/data-types/float-and-real-transact-sql.md).  
  
 负缓冲区删除距几何图形边界给定距离内的所有点。 下图以圆的明暗交错区域显示负缓冲区。 虚线是原始多边形的边界，实线是结果多边形的边界。  
  
 如果**字符串**参数传递给方法，则它将转换为**float**或它会引发`ArgumentException`。  
  
## <a name="examples"></a>示例  
  
### <a name="a-calling-bufferwithcurves-with-a-parameter-value--0-on-one-dimensional-geometry-instance"></a>A. 使用 < 0 的参数值对一维 geometry 实例调用 BufferWithCurves()  
 以下示例返回一个空 `GeometryCollection` 实例：  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves(-1).ToString(); 
 ```
  
### <a name="b-calling-bufferwithcurves-with-a-parameter-value--0-on-a-two-dimensional-geometry-instance"></a>B. 使用 < 0 的参数值对二维 geometry 实例调用 BufferWithCurves()  
 以下示例返回一个具有负缓冲区的 `CurvePolygon` 实例：  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.BufferWithCurves(-1).ToString()
 ```  
  
### <a name="c-calling-bufferwithcurves-with-a-parameter-value--0-that-returns-an-empty-geometrycollection"></a>C. 使用 < 0 的参数值调用 BufferWithCurves()，它返回一个空 GeometryCollection  
 下面的示例演示所发生的情况时*距离*参数等于-2:  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.BufferWithCurves(-2).ToString();
 ```  
  
 这**选择**语句返回`GEOMETRYCOLLECTION EMPTY`  
  
### <a name="d-calling-bufferwithcurves-with-a-parameter-value--0"></a>D. 使用 = 0 的参数值调用 BufferWithCurves()  
 下面的示例返回一份调用**几何图形**实例：  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves(0).ToString();
 ```  
  
### <a name="e-calling-bufferwithcurves-with-a-non-zero-parameter-value-that-is-extremely-small"></a>E. 使用极小的非零参数值调用 BufferWithCurves()  
 下面的示例也会返回一份调用**几何图形**实例：  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 DECLARE @distance float = 1e-20; 
 SELECT @g.BufferWithCurves(@distance).ToString();
 ```  
  
### <a name="f-calling-bufferwithcurves-with-a-parameter-value--0"></a>F. 使用 > 0 的参数值调用 BufferWithCurves()  
 以下示例返回 `CurvePolygon` 实例：  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves(2).ToString();
 ```  
  
### <a name="g-passing-a-valid-string-parameter"></a>G. 传递有效的字符串参数  
 以下示例返回与前面相同的 `CurvePolygon` 实例，但为方法传递一个字符串参数：  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves('2').ToString();
 ```  
  
### <a name="h-passing-an-invalid-string-parameter"></a>H. 传递无效的字符串参数  
 以下示例将引发错误：  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)' 
 SELECT @g.BufferWithCurves('a').ToString();
 ```  
  
 请注意，前面的两个示例为 `BufferWithCurves()` 方法传递字符串文字。 第一个示例有效，因为可以将字符串文字转换为数值。 但第二个示例引发 `ArgumentException`。  
  
### <a name="i-calling-bufferwithcurves-on-multipoint-instance"></a>I. 对 MultiPoint 实例调用 BufferWithCurves()  
 以下示例返回两个 `GeometryCollection` 实例和一个 `CurvePolygon` 实例。  
  
```
 DECLARE @g geometry = 'MULTIPOINT((1 1),(1 4))'; 
 SELECT @g.BufferWithCurves(1).ToString(); 
 SELECT @g.BufferWithCurves(1.5).ToString(); 
 SELECT @g.BufferWithCurves(1.6).ToString();
 ```  
  
 前两个**选择**语句返回`GeometryCollection`实例，因为参数*距离*小于或等于 1/2 到这两者之间的距离点 (1 1) 和 (1 4)。 第三个**选择**语句返回`CurvePolygon`实例，因为这两个缓冲的实例点 (1 1) 和 (1 4) 重叠。  
  
## <a name="see-also"></a>另请参阅  
 [在几何图形实例的扩展的方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
 

