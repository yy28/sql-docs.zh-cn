---
title: "BufferWithCurves (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 08/11/2017
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
- BufferWithCurves
- BufferWithCurves_TSQL
dev_langs: TSQL
helpviewer_keywords: BufferWithCurves method (geography)
ms.assetid: abf0a11c-c99c-4faa-bf80-3ae8e04d7bfb
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 12b9abd82133c7f2c42f43dd436e223b1b0173f1
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="bufferwithcurves-geography-data-type"></a>BufferWithCurves（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  返回**geography**表示的所有组的实例中调用的点的距离**geography**实例小于或等于*距离*参数。  
  
## <a name="syntax"></a>语法  
  
```  
  
.BufferWithCurves ( distance )  
```  
  
## <a name="arguments"></a>参数  
 *距离*  
 是**float** ，表示点构成缓冲区的最大距离可以来自地域实例。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**地理位置**  
  
 CLR 返回类型： **SqlGeography**  
  
## <a name="exceptions"></a>异常  
 以下条件将引发**ArgumentException**。  
  
-   没有为方法传递任何参数，例如，`@g.BufferWithCurves()`  
  
-   为方法传递了非数值参数，例如，`@g.BufferWithCurves('a')`  
  
-   **NULL**传递给方法，如`@g.BufferWithCurves(NULL)`  
  
## <a name="remarks"></a>注释  
 下表显示为不同距离值返回的结果。  
  
|距离值|类型维度|返回的空间类型|  
|--------------------|---------------------|---------------------------|  
|距离 < 0|0 或 1|空**GeometryCollection**实例|  
|距离\<0|2 或更大|A **CurvePolygon**或**GeometryCollection**与负缓冲区的实例。<br /><br /> 注意： 负缓冲区可能创建一个空**GeometryCollection**|
|距离 = 0|所有维度|调用的复制**geography**实例|  
|距离 > 0|所有维度|**CurvePolygon**或**GeometryCollection**实例|  
  
> [!NOTE]  
>  由于*距离*是**float**，可以相当非常小的值为零的计算中。  在这种情况，然后调用一份**geography**返回实例。  
  
 如果**字符串**参数传递给方法，则它将转换为**float**或它会引发`ArgumentException`。  
  
## <a name="examples"></a>示例  
  
### <a name="a-calling-bufferwithcurves-with-a-parameter-value--0-on-one-dimensional-geography-instance"></a>A. 使用 < 0 的参数值对一维 geography 实例调用 BufferWithCurves()  
 以下示例返回一个空 `GeometryCollection` 实例：  
  
 ```sql
 DECLARE @g geography= 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(-1).ToString();
``` 
  
### <a name="b-calling-bufferwithcurves-with-a-parameter-value--0-on-a-two-dimensional-geography-instance"></a>B. 使用 < 0 的参数值对二维 geography 实例调用 BufferWithCurves()  
 以下示例返回一个具有负缓冲区的 `CurvePolygon` 实例：  
  
 ```sql
 DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.BufferWithCurves(-1).ToString()
 ```  
  
### <a name="c-calling-bufferwithcurves-with-a-parameter-value--0-that-returns-an-empty-geometrycollection"></a>C. 使用 < 0 的参数值调用 BufferWithCurves()，它返回一个空 GeometryCollection  
 下面的示例演示所发生的情况时*距离*参数等于-2:  
  
 ```sql
 DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.BufferWithCurves(-2).ToString();
 ```  
  
 这**选择**语句返回`GEOMETRYCOLLECTION EMPTY`  
  
### <a name="d-calling-bufferwithcurves-with-a-parameter-value--0"></a>D. 使用 = 0 的参数值调用 BufferWithCurves()  
 下面的示例返回一份调用**geography**实例：  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(0).ToString();
 ```  
  
### <a name="e-calling-bufferwithcurves-with-a-non-zero-parameter-value-that-is-extremely-small"></a>E. 使用极小的非零参数值调用 BufferWithCurves()  
 下面的示例也会返回一份调用**geography**实例：  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 DECLARE @distance float = 1e-20;  
 SELECT @g.BufferWithCurves(@distance).ToString();
 ```  
  
### <a name="f-calling-bufferwithcurves-with-a-parameter-value--0"></a>F. 使用 > 0 的参数值调用 BufferWithCurves()  
 以下示例返回 `CurvePolygon` 实例：  

 ```sql
 DECLARE @g geography= 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(2).ToString();
 ```  
### <a name="g-passing-a-valid-string-parameter"></a>G. 传递有效的字符串参数  
 以下示例返回与前面相同的 `CurvePolygon` 实例，但为方法传递一个字符串参数：  

 ```sql
 DECLARE @g geography= 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves('2').ToString();
```  
  
### <a name="h-passing-an-invalid-string-parameter"></a>H. 传递无效的字符串参数  
 以下示例将引发错误：  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)'  
 SELECT @g.BufferWithCurves('a').ToString();
 ```  
  
 请注意，前面的两个示例为 `BufferWithCurves()` 方法传递字符串文字。 第一个示例有效，因为可以将字符串文字转换为数值。 但第二个示例引发 `ArgumentException`。  
  
## <a name="see-also"></a>另请参阅  
 [地域实例的扩展的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [BufferWithCurves &#40; geometry 数据类型 &#41;](../../t-sql/spatial-geometry/bufferwithcurves-geometry-data-type.md)  
  
  
