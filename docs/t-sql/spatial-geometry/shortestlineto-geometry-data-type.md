---
title: "ShortestLineTo (geometry 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 08/03/2017
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
dev_langs:
- TSQL
helpviewer_keywords:
- ShortestLineTo method (geometry)
ms.assetid: 39a2d0e4-4f93-4e94-a27e-6ad9537cfe74
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 08e83f7bb1993d3b55a48e5e3714c75d4bd33429
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="shortestlineto-geometry-data-type"></a>ShortestLineTo（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

返回**LineString**实例表示的最短距离两者之间的两个点**几何图形**实例。 长度**LineString**返回实例是这两者之间的距离**几何图形**实例。
  
## <a name="syntax"></a>语法  
  
```  
  
.ShortestLineTo ( geometry_other )  
```  
  
## <a name="arguments"></a>参数  
 *geometry_other*  
 第二个**几何图形**实例调用**几何图形**实例尝试确定到的最短距离。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**几何图形**  
  
 CLR 返回类型： **SqlGeometry**  
  
## <a name="remarks"></a>注释  
 该方法返回**LineString**实例与终结点上的两个非交叉边框**几何图形**要比较的实例。 长度**LineString**返回的等于之间的两个的最短距离**几何图形**实例。 一个空**LineString**实例时返回两个**几何图形**实例相互交叉。  
  
## <a name="examples"></a>示例  
  
### <a name="a-calling-shortestlineto-on-non-intersecting-instances"></a>A. 在不相交的实例上调用 ShortestLineTo()  
 该示例确定 `CircularString` 和 `LineString` 实例之间的最短距离，并返回连接这两个点的 `LineString` 实例：  
  
```
 DECLARE @g1 geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
 DECLARE @g2 geometry = 'LINESTRING(-4 7, 7 10, 3 7)';  
 SELECT @g1.ShortestLineTo(@g2).ToString();
 ```  
  
### <a name="b-calling-shortestlineto-on-intersecting-instances"></a>B. 在相交的实例上调用 ShortestLineTo()  
 该示例返回空 `LineString` 实例，因为 `LineString` 实例与 `CircularString` 实例相交：  
  
```
 DECLARE @g1 geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
 DECLARE @g2 geometry = 'LINESTRING(0 5, 7 10, 3 7)';  
 SELECT @g1.ShortestLineTo(@g2).ToString();
 ```  
  
## <a name="see-also"></a>另请参阅  
 [ShortestLineTo &#40; geography 数据类型 &#41;](../../t-sql/spatial-geography/shortestlineto-geography-data-type.md)  
  
  

