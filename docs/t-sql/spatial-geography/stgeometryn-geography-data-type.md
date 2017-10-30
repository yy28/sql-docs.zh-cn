---
title: "STGeometryN (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STGeometryN (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeometryN method
ms.assetid: 53755f69-cd50-475b-b3b8-a1a9157cf03a
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d5d11dc77ce692543068cba6739ef982bc8264c8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="stgeometryn-geography-data-type"></a>STGeometryN（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回指定**geography**中的元素**GeometryCollection**或子类型之一。 上的子类型时使用 STGeometryN() **GeometryCollection**，如**MultiPoint**或**MultiLineString**，此方法返回**地理位置**实例如果调用，N = 1。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STGeometryN ( expression )  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 是**int** 1 之间的数的表达式**geography**实例**GeometryCollection**。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**地理位置**  
  
 CLR 返回类型： **SqlGeography**  
  
## <a name="remarks"></a>注释  
 此方法将返回 null 如果参数大于的结果[STNumGeometries()](../../t-sql/spatial-geography/stnumgeometries-geography-data-type.md)并且会在引发**ArgumentOutOfRangeException**如果*表达式*参数为小于 1。  
  
## <a name="examples"></a>示例  
 下面的示例创建`MultiPoint``geography`实例并使用`STGeometryN()`查找第二个`geography`实例**GeometryCollection**。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('MULTIPOINT(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STGeometryN(2).ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [地域实例上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

