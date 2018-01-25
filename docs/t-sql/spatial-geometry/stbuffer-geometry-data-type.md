---
title: "STBuffer (geometry 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 08/03/2017
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
- STBuffer (geometry Data Type)
- STBuffer_TSQL
dev_langs: TSQL
helpviewer_keywords: STBuffer (geometry Data Type)
ms.assetid: ca6bf2dc-1d38-4503-b87e-f2ea033d36ba
caps.latest.revision: "29"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ff65df2a1216a29b15a0458e9e4537c748140714
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="stbuffer-geometry-data-type"></a>STBuffer（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回表示的所有联合的几何对象点从其距离**几何图形**实例小于或等于指定的值。
  
## <a name="syntax"></a>语法  
  
```  
  
.STBuffer ( distance )  
```  
  
## <a name="arguments"></a>参数  
 *distance*  
 是类型的值**float** (**double** .NET Framework 中) 指定围绕其计算的缓冲区的几何图形实例之间的距离。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**几何图形**  
  
 CLR 返回类型： **SqlGeometry**  
  
## <a name="remarks"></a>注释  
 `STBuffer()`计算类似的缓冲区[BufferWithTolerance](../../t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type.md)，并指定*容差*= 距离\*.001 和*相对* =  **false**。  
  
 当*距离*> 0，则请**多边形**或**MultiPolygon**返回实例。  
  
> [!NOTE]  
>  由于距离是**float**，可以相当非常小的值为零的计算中。  在这种情况，调用一份**几何图形**返回实例。  请参阅[float 和 real &#40;Transact SQL &#41;](../../t-sql/data-types/float-and-real-transact-sql.md)  
  
 当*距离*= 0，则调用一份**几何图形**返回实例。  
  
 当*距离*< 0，然后  
  
-   一个空**GeometryCollection**时实例的维度是 0 或 1，则返回实例。  
  
-   2 个或多个实例的维度时，则返回负缓冲区。  
  
    > [!NOTE]  
    >  负缓冲区还可以创建一个空**GeometryCollection**实例。  
  
 负缓冲区删除距几何图形边界给定距离的所有点。  
  
 Theorectical 和计算的缓冲区之间的错误是最大 (容差，范围 * 1.E 7)，容差 = 距离\*.001。 有关扩展盘区的详细信息，请参阅[geometry 数据类型方法引用](http://msdn.microsoft.com/library/d88e632b-6b2f-4466-a15f-9fbef1a347a7)。  
  
## <a name="examples"></a>示例  
  
### <a name="a-calling-stbuffer-with-parametervalue--0-on-one-dimensional-geometry-instance"></a>A. 使用 < 0 的参数值在一维 geometry 实例上调用 STBuffer()  
 以下示例返回一个空 `GeometryCollection` 实例：  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer(-1).ToString();
 ```  
  
### <a name="b-calling-stbuffer-with-parametervalue--0-on-a-polygon-instance"></a>B. 使用 < 0 的参数值在 Polygon 实例上调用 STBuffer()  
 以下示例返回一个具有负缓冲区的 `Polygon` 实例：  
  
```
 DECLARE @g geometry = 'POLYGON((1 1, 1 5, 5 5, 5 1, 1 1))'; 
 SELECT @g.STBuffer(-1).ToString();
 ```  
  
### <a name="c-calling-stbuffer-with-parametervalue--0-on-a-curvepolygon-instance"></a>C. 使用 < 0 的参数值在 CurvePolygon 实例上调用 STBuffer()  
 以下示例从 `Polygon` 实例中返回一个具有负缓冲区的 `CurvePolygon` 实例：  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.STBuffer(-1).ToString();
 ```  
  
> [!NOTE]  
>  将返回 `Polygon` 实例，而非 `CurvePolygon` 实例。  若要返回`CurvePolygon`实例，请参阅[BufferWithCurves &#40; geometry 数据类型 &#41;](../../t-sql/spatial-geometry/bufferwithcurves-geometry-data-type.md)  
  
### <a name="d-calling-stbuffer-with-a-negative-parameter-value-that-returns-an-empty-instance"></a>D. 使用返回一个空实例的负参数值调用 STBuffer()  
 下面的示例演示所发生的情况时*距离*参数等于-2 前面的示例。  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.STBuffer(-2).ToString();
 ```  
  
 这**选择**语句返回`GEOMETRYCOLLECTION EMPTY.`  
  
### <a name="e-calling-stbuffer-with-parametervalue--0"></a>E. 当参数值 = 0 时调用 STBuffer()  
 以下示例返回调用 `geometry` 实例的副本：  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer(0).ToString();
 ```  
  
### <a name="f-calling-stbuffer-with-a-non-zero-parameter-value-that-is-extremely-small"></a>F. 使用极小的非零参数值调用 STBuffer()  
 以下示例还返回调用 `geometry` 实例的副本：  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)';  
 DECLARE @distance float = 1e-20;  
 SELECT @g.STBuffer(@distance).ToString();
 ```  
  
### <a name="g-calling-stbuffer-with-parametervalue--0"></a>G. 使用 > 0 的参数值调用 STBuffer()  
 以下示例返回 `Polygon` 实例：  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer(2).ToString();
 ```  
  
### <a name="h-calling-stbuffer-with-a-string-parameter-value"></a>H. 使用字符串参数值调用 STBuffer()  
 以下示例返回与前面相同的 `Polygon` 实例，但为方法传递一个字符串参数：  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer('2').ToString();
 ```  
  
 以下示例将引发错误：  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer('a').ToString();
 ```  
  
> [!NOTE]  
>  前面的两个示例为 `STBuffer()` 方法传递字符串文字。  第一个示例有效，因为可以将字符串文字转换为数值。 但第二个示例引发 `ArgumentException`。  
  
### <a name="i-calling-stbuffer-on-a-multipoint-instance"></a>I. 对 MultiPoint 实例调用 STBuffer()  
 以下示例返回两个 `MultiPolygon` 实例和一个 `Polygon` 实例。  
  
```
 DECLARE @g geometry = 'MULTIPOINT((1 1),(1 4))'; 
 SELECT @g.STBuffer(1).ToString(); 
 SELECT @g.STBuffer(1.5).ToString(); 
 SELECT @g.STBuffer(1.6).ToString();
 ```  
  
 前两个**选择**语句返回`MultiPolygon`实例，因为参数*距离*小于或等于 1/2 到这两者之间的距离点 (1 1) 和 (1 4)。 第三个**选择**语句返回`Polygon`实例，因为这两个缓冲的实例点 (1 1) 和 (1 4) 重叠。  
  
## <a name="see-also"></a>另请参阅  
 [BufferWithTolerance &#40; geometry 数据类型 &#41;](../../t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type.md)   
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

