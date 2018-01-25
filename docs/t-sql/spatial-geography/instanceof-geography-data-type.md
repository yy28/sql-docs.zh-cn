---
title: "InstanceOf (geography 数据类型) |Microsoft 文档"
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
- InstanceOf
- InstanceOf_TSQL
dev_langs: TSQL
helpviewer_keywords: InstanceOf method
ms.assetid: 1eaed0e4-1c72-45a9-9926-5b513335cf33
caps.latest.revision: "28"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1178b0287c167666216b090a87c6c9dd645622f7
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="instanceof-geography-data-type"></a>InstanceOf（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  如果测试**geography**实例是否与指定的类型相同。  
  
## <a name="syntax"></a>语法  
  
```  
  
.InstanceOf ( 'geography_type')  
```  
  
## <a name="arguments"></a>参数  
 *geography_type*  
 是**nvarchar （4000)** 16 中公开的类型之一指定字符串**geography**类型层次结构。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**位**  
  
 CLR 返回类型： **SqlBoolean**  
  
## <a name="remarks"></a>注释  
 如果返回 1 的一种**geography**实例与指定的类型相同，或如果指定的类型是祖先的实例类型; 否则，返回 0。  
  
 这**geography**数据类型方法支持**FullGlobe**实例或大于半球的空间实例。  
  
 该方法的输入必须是以下之一： Geometry、 点、 曲线、 LineString、 CircularString、 面、 Polygon、 CurvePolygon， **GeometryCollection**， **MultiSurface**， **MultiPolygon、 MultiCurve、 MultiLineString**， **MultiPoint**，或**FullGlobe**。  
  
 如果将任何其他字符串用于输入，此方法将引发 `ArgumentException`。  
  
 此方法不精确。  
  
## <a name="examples"></a>示例  
 下面的示例创建`MultiPoint`实例并使用`InstanceOf()`实例是否为`GeometryCollection`。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('MULTIPOINT(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.InstanceOf('GEOMETRYCOLLECTION');  
```  
  
## <a name="see-also"></a>另请参阅  
 [地理实例上的扩展方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
