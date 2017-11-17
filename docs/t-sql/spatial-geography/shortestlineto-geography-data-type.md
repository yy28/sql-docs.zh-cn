---
title: "ShortestLineTo (geography 数据类型) |Microsoft 文档"
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
- ShortestLineTo_TSQL
- ShortestLineTo
dev_langs:
- TSQL
helpviewer_keywords:
- ShortestLineTo method (geography)
ms.assetid: 9d7c9885-5d1b-49ae-af31-5ef9fb8acaba
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: acb6d16fbf1413a81a05582bc203a7e768b70c75
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="shortestlineto-geography-data-type"></a>ShortestLineTo（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  返回**LineString**实例表示的最短距离两者之间的两个点**geography**实例。 长度**LineString**返回实例是这两者之间的距离**geography**实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
.ShortestLineTo ( geography_other )  
```  
  
## <a name="arguments"></a>参数  
 *geography_other*  
 指定第二个**geography**实例调用**geography**实例尝试确定到的最短距离。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**地理位置**  
  
 CLR 返回类型： **SqlGeography**  
  
## <a name="remarks"></a>注释  
 该方法返回**LineString**实例与终结点上的两个非交叉边框**geography**要比较的实例。 长度**LineString**返回的等于之间的两个的最短距离**geography**实例。 一个空**LineString**实例时返回两个**geography**实例相互交叉。  
  
## <a name="examples"></a>示例  
  
### <a name="a-calling-shortestlineto-on-non-intersecting-instances"></a>A. 在不相交的实例上调用 ShortestLineTo()  
 该示例确定 `CircularString` 和 `LineString` 实例之间的最短距离，并返回连接这两个点的 `LineString` 实例：  
  
 ```
 DECLARE @g1 geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 DECLARE @g2 geography = 'LINESTRING(-119.119263 46.183634, -119.273071 47.107523, -120.640869 47.569114, -122.200928 47.454094)';  
 SELECT @g1.ShortestLineTo(@g2).ToString();
 ```  
  
### <a name="b-calling-shortestlineto-on-intersecting-instances"></a>B. 在相交的实例上调用 ShortestLineTo()  
 该示例返回空 `LineString` 实例，因为 `LineString` 实例与 `CircularString` 实例相交：  
  
 ```
 DECLARE @g1 geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 DECLARE @g2 geography = 'LINESTRING(-119.119263 46.183634, -119.273071 47.107523, -120.640869 47.569114, -122.348 47.649, -122.681 47.655)';  
 SELECT @g1.ShortestLineTo(@g2).ToString();
``` 
  
## <a name="see-also"></a>另请参阅  
 [地域实例的扩展的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  

