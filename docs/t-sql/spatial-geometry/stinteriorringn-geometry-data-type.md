---
title: "STInteriorRingN (geometry 数据类型) |Microsoft 文档"
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
- STInteriorRingN_TSQL
- STInteriorRingN (geometry Data Type)
dev_langs: TSQL
helpviewer_keywords: STInteriorRingN (geometry Data Type)
ms.assetid: 47310f9f-2cdb-41e0-a6da-7c3cfbf139ac
caps.latest.revision: "21"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e80a67f84c153a8b2daffc0174046af70c972709
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="stinteriorringn-geometry-data-type"></a>STInteriorRingN（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回指定内的环**Polygongeometry**实例。
  
## <a name="syntax"></a>语法  
  
```  
  
.STInteriorRingN ( expression )  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 是**int**介于 1 和中的内环数的表达式**几何图形**实例。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**几何图形**  
  
 CLR 返回类型： **SqlGeometry**  
  
 打开地理空间联盟 (OGC) 类型： **LineString**  
  
## <a name="remarks"></a>注释  
 此方法返回**null**如果**几何图形**实例不是某个多边形。 此方法还会引发**ArgumentOutOfRangeException**如果表达式为大于的环数。 可以使用返回的环数`STNumInteriorRing``()`。  
  
## <a name="examples"></a>示例  
 下面的示例创建`Polygon`实例并使用`STInteriorRingN()`返回作为此多边形的内环**LineString**。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0),(2 2, 2 1, 1 1, 1 2, 2 2))', 0);  
SELECT @g.STInteriorRingN(1).ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

