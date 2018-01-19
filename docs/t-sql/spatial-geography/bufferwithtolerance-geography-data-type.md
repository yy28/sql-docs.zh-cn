---
title: "BufferWithTolerance (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- BufferWithTolerance_TSQL
- BufferWithTolerance
dev_langs: TSQL
helpviewer_keywords: BefferWithTolerance method
ms.assetid: f1783e6b-0f17-464f-b1c7-1c3f7d8aa042
caps.latest.revision: "20"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 07c9278bc7c277a0991f0f55cad18f496c514cde
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="bufferwithtolerance-geography-data-type"></a>BufferWithTolerance（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回一个表示所有点的联合的几何对象值从其距离**geography**实例小于或等于指定的值，从而使指定容差。  
  
 此 geography 数据类型方法支持**FullGlobe**实例或大于半球的空间实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
.BufferWithTolerance ( distance, tolerance, relative )  
```  
  
## <a name="arguments"></a>参数  
 *distance*  
 是**float**表达式指定的距离**geography**围绕其计算的缓冲区的实例。  
  
 缓冲区的最大距离不能超过 0.999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 1/2 地球圆的周长) 或完整的全球范围。  
  
 *tolerance*  
 是**float**表达式指定的缓冲区距离的容差。  
  
 *容差*值指中返回的线性近似的理想的缓冲区距离的最大变体。  
  
 例如，点的理想缓冲区距离为圆圈，但是这必须与多边形近似。 公差越小，多边形具有的点就越多，这将增加结果的复杂度，但可减少错误。  
  
 最小限制为距离的 0.1%，任何小于此限制的公差都将向上舍入到此最小限制。  
  
 *relative*  
 是**位**指定是否*容差*值是相对或绝对。 如果 'TRUE' 或 1，容差是相对和计算的产品为*容差*参数和角速度范围\*的椭圆体赤道半径。 如果 'FALSE' 或 0，容差是绝对和*容差*值是绝对的最大变体中返回的线性近似的理想的缓冲区距离。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**地理位置**  
  
 CLR 返回类型： **SqlGeography**  
  
## <a name="remarks"></a>注释  
 此方法将引发**ArgumentException**如果*距离*不是一个数字 (NAN)，或者如果*距离*为正或负无穷大。  此方法还会引发**ArgumentException**如果*容差*是零 (0)，而不是数字 (NaN)，负数，或正或负无穷。  
  
 `STBuffer()`将返回**FullGlobe**实例在某些情况下; 例如，`STBuffer()`返回**FullGlobe**上两个两极的缓冲区距离大于从赤道到距离时实例极地。  
  
 此方法将引发**ArgumentException**中**FullGlobe**实例其中的缓冲区距离超过以下限制：  
  
 0.999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 1/2 地球圆的周长)  
  
 Theorectical 和计算的缓冲区之间的错误是最大 (容差，范围\*1.E 7) 容差所在的值*容差*参数。 有关扩展盘区的详细信息，请参阅[geography 数据类型方法引用](http://msdn.microsoft.com/library/028e6137-7128-4c74-90a7-f7bdd2d79f5e)。  
  
 此方法不精确。  
  
## <a name="examples"></a>示例  
 下面的示例创建 `Point` 实例，并使用 `BufferWithTolerance()` 获取环绕该实例的大致缓冲区。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.BufferWithTolerance(1, .5, 0).ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [STBuffer &#40; geography 数据类型 &#41;](../../t-sql/spatial-geography/stbuffer-geography-data-type.md)   
 [地理实例上的扩展方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
