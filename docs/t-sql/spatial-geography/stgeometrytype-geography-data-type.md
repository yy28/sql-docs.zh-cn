---
title: "STGeometryType (geography 数据类型) |Microsoft 文档"
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
- STGeometryType (geography Data Type)
- STGeometryType_TSQL
dev_langs: TSQL
helpviewer_keywords: STGeometryType method
ms.assetid: 3e169ead-a98e-44af-8d33-fd59a955cae4
caps.latest.revision: "17"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7d77afb909987ce56d7922116a954c4f94751bea
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="stgeometrytype-geography-data-type"></a>STGeometryType（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回所表示的开放地理空间联盟 (OGC) 类型名称**geography**实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STGeometryType ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型： **nvarchar （4000)**  
  
 CLR 返回类型： **SqlString**  
  
## <a name="remarks"></a>注释  
 可以由 OGC 类型名称`STGeometryType()`是**点**， **LineString**， **CircularString**， **CompoundCurve**，**多边形**， **CurvePolygon**， **GeometryCollection**， **MultiPoint**， **MultiLineString**，和**MultiPolygon**。  
  
## <a name="examples"></a>示例  
 下面的示例创建一个 `Polygon` 实例并使用 `STGeometryType()` 确认它是多边形。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.STGeometryType();  
```  
  
## <a name="see-also"></a>另请参阅  
 [地理实例上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
