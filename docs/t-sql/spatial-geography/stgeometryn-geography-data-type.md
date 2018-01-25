---
title: "STGeometryN (geography 数据类型) |Microsoft 文档"
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
f1_keywords: STGeometryN (geography Data Type)
dev_langs: TSQL
helpviewer_keywords: STGeometryN method
ms.assetid: 53755f69-cd50-475b-b3b8-a1a9157cf03a
caps.latest.revision: "15"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e92224c6ea0aae9ad389353a705f3c1c3c9aa21c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="stgeometryn-geography-data-type"></a>STGeometryN（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

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
 [地理实例上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
