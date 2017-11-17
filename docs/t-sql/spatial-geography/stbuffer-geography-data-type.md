---
title: "STBuffer (geography 数据类型) |Microsoft 文档"
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
- STBuffer (geography Data Type)
- STBuffer_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STBuffer (geography Data Type)
ms.assetid: cb4deab8-642b-44d9-b3d9-85114d64021e
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2fa06f270ad653e9c8e43a5ec5456257e785670e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="stbuffer-geography-data-type"></a>STBuffer（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  返回表示的所有联合的地理位置对象点从其距离**geography**实例小于或等于指定的值。  
  
 此 geography 数据类型方法支持**FullGlobe**实例或大于半球的空间实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STBuffer ( distance )  
```  
  
## <a name="arguments"></a>参数  
 *距离*  
 是类型的值**float** (**double** .NET Framework 中) 指定的距离**geography**围绕其计算的缓冲区的实例。  
  
 缓冲区的最大距离不能超过 0.999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 1/2 地球圆的周长) 或完整的全球范围。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**地理位置**  
  
 CLR 返回类型： **SqlGeography**  
  
## <a name="remarks"></a>注释  
 Stbuffer （） 中与相同的方式计算缓冲区[BufferWithTolerance](../../t-sql/spatial-geography/bufferwithtolerance-geography-data-type.md)，并指定*容差*= abs(distance) \* .001 和*相对* = **false**。  
  
 负缓冲区中删除的边界的给定距离内的所有点**geography**实例。  
  
 `STBuffer()`将返回**FullGlobe**实例在某些情况下; 例如，`STBuffer()`返回**FullGlobe**实例时的缓冲区距离大于从赤道到极地的距离。 缓冲区不能超过完整的地球。  
  
 此方法将引发**ArgumentException**中**FullGlobe**实例其中的缓冲区距离超过以下限制：  
  
 0.999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 1/2 地球圆的周长)  
  
 最大距离限制允许将缓冲区构造得尽可能灵活。  
  
 Theorectical 和计算的缓冲区之间的错误是最大 (容差，范围 * 1.E 7)，容差 = 距离\*.001。 有关扩展盘区的详细信息，请参阅[geography 数据类型方法引用](http://msdn.microsoft.com/library/028e6137-7128-4c74-90a7-f7bdd2d79f5e)。  
  
## <a name="examples"></a>示例  
 下面的示例创建`LineString``geography`实例。 然后，它使用 `STBuffer()` 返回该实例的 1 米内的区域。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STBuffer(1).ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [BufferWithTolerance &#40; geography 数据类型 &#41;](../../t-sql/spatial-geography/bufferwithtolerance-geography-data-type.md)   
 [地域实例上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

