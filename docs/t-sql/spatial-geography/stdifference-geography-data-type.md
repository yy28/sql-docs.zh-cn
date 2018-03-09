---
title: "STDifference (geography 数据类型) |Microsoft 文档"
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
- STDifference_TSQL
- STDifference (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDifference (geography Data Type)
ms.assetid: 1cde5054-b91a-41bb-812a-08c9308738af
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9898254d43c4586f787d5e7eb68e457137be5554
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="stdifference-geography-data-type"></a>STDifference（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回一个对象，表示该点集从一个**geography**位于外部另一个实例**geography**实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STDifference ( other_geography )  
```  
  
## <a name="arguments"></a>参数  
 *other_geography*  
 是另一种**geography** ，该值指示该点以从对其调用 STDifference() 实例中删除的实例。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**地理位置**  
  
 CLR 返回类型： **SqlGeography**  
  
## <a name="exceptions"></a>异常  
 此方法将引发**ArgumentException**如果实例包含对跖边缘。  
  
## <a name="remarks"></a>注释  
 如果此方法将始终返回 null 的空间引用标识符 (Srid) **geography**实例不匹配。  
  
 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，可能返回的结果集在服务器上已扩展到**FullGlobe**实例。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持大于半球的空间实例。 只有在输入实例包含圆弧线段时，结果才会包含圆弧线段。 此方法不精确。  
  
## <a name="examples"></a>示例  
  
### <a name="a-computing-the-difference-between-two-geography-instances"></a>A. 计算两个地理实例之间的差值  
 下面的示例使用`STDifference()`来计算两个区别**geography**实例。  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SET @h = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STDifference(@h).ToString();  
```  
  
### <a name="b-using-a-fullglobe-with-stdifference"></a>B. 将 FullGlobe 与 STDifference() 结合使用  
 下面的示例使用 `FullGlobe` 实例。 第一个结果是一个空的 `GeometryCollection`，第二个结果是 `Polygon` 实例。 当 `STDifference()` 实例为参数时，`GeometryCollection` 返回一个空的 `FullGlobe`。 调用 `geography` 实例的每个点都包含在 `FullGlobe` 实例中。  
  
```
 DECLARE @g geography = 'POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 DECLARE @h geography = 'FULLGLOBE';  
 SELECT @g.STDifference(@h).ToString(),  
 @h.STDifference(@g).ToString();
 ```  
  
## <a name="see-also"></a>另请参阅  
 [地理实例上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
