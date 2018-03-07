---
title: "STCurveN (geography 数据类型) |Microsoft 文档"
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
- STCurveN
- STCurveN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveN method (geography)
ms.assetid: 99ef7100-2c4b-4f07-8d66-b343da94b023
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 59709f07fa84c24942ed14a8f8af7e776643913f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="stcurven-geography-data-type"></a>STCurveN（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回从指定的曲线**geography**实例，它是**LineString**， **CircularString**，或**CompoundCurve**。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STCurveN( n )  
```  
  
## <a name="arguments"></a>参数  
 *n*  
 是**int**介于 1 和中的曲线数之间的表达式**geography**实例。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**地理位置**  
  
 CLR 返回类型： **SqlGeography**  
  
## <a name="exceptions"></a>异常  
 如果 n < 1 则**ArgumentOutOfRangeException**引发。  
  
## <a name="remarks"></a>注释  
 **NULL**时返回以下条件时发生。  
  
-   **Geography**实例声明，但未实例化  
  
-   **Geography**实例为空  
  
-   n 超过中的曲线数目**geography**实例 (请参阅[STNumCurves &#40; geography 数据类型 &#41;](../../t-sql/spatial-geography/stnumcurves-geography-data-type.md)  
  
-   维度**geography**实例不等于 (请参阅[STDimension &#40; geography 数据类型 &#41;](../../t-sql/spatial-geography/stdimension-geography-data-type.md)  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-stcurven-on-a-circularstring"></a>A. 在 CircularString 上使用 STCurveN()  
 下面的示例返回在第二个曲线**CircularString**实例：  
  
```
 DECLARE @g geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 该示例返回：  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
### <a name="b-using-stcurven-on-a-compoundcurve"></a>B. 在 CompoundCurve 上使用 STCurveN()  
 下面的示例返回在第二个曲线**CompoundCurve**实例：  
  
```
 DECLARE @g geography = 'COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 该示例返回：  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
### <a name="c-using-stcurven-on-a-compoundcurve-containing-three-circularstrings"></a>C. 在包含三个 CircularString 的 CompoundCurve 实例上使用 STCurveN()  
 下面的示例使用**CompoundCurve**将合并三个单独的实例**CircularString**入同一实例曲线序列与前面的示例：  
  
```
 DECLARE @g geography = 'COMPOUNDCURVE (CIRCULARSTRING (-122.358 47.653, -122.348 47.649, -122.348 47.658), CIRCULARSTRING(-122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 该示例返回：  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
 `STCurveN()` 返回相同的结果，而无论使用的是哪种熟知文本 （WKT） 格式。  
  
### <a name="d-testing-for-validity-before-calling-stcurve"></a>D. 在调用 STCurve() 之前测试有效性  
 下面的示例演示如何确保 *n* 是否有效，然后才能调用 STCurveN() 方法：  
  
```
 DECLARE @g geography;  
 DECLARE @n int;  
 SET @n = 2;  
 SET @g = geography::Parse('LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)');  
 IF @n >= 1 AND @n <= @g.STNumCurves()  
 BEGIN  
 SELECT @g.STCurveN(@n).ToString();  
 END
  ```  
  
## <a name="see-also"></a>另请参阅  
 [地理实例上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
