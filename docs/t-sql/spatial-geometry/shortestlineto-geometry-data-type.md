---
title: ShortestLineTo（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- ShortestLineTo method (geometry)
ms.assetid: 39a2d0e4-4f93-4e94-a27e-6ad9537cfe74
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f2d92d90c363cd17844d905a7d0108b0f148a007
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47631842"
---
# <a name="shortestlineto-geometry-data-type"></a>ShortestLineTo（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

返回一个包含两个点的 **LineString** 实例，这两个点表示两个 **geometry** 实例之间的最短距离。 返回的 **LineString** 实例长度是两个 **geometry** 实例之间的距离。
  
## <a name="syntax"></a>语法  
  
```  
  
.ShortestLineTo ( geometry_other )  
```  
  
## <a name="arguments"></a>参数  
 *geometry_other*  
 第二个 **geometry** 实例，执行调用的 **geometry** 实例尝试确定与该实例之间的最短距离。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geometry  
  
 CLR 返回类型：SqlGeometry  
  
## <a name="remarks"></a>Remarks  
 该方法返回一个 **LineString** 实例，它包含的端点位于所比较的两个不相交 **geometry** 实例的边界上。 返回的 **LineString** 长度等于两个 **geometry** 实例之间的最短距离。 当两个 **geometry** 实例彼此相交时，将返回空的 **LineString** 实例。  
  
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
 [ShortestLineTo（geography 数据类型）](../../t-sql/spatial-geography/shortestlineto-geography-data-type.md)  
  
  

