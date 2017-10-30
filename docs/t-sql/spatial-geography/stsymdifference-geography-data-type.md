---
title: "STSymDifference (geography 数据类型) |Microsoft 文档"
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
- STSymDifference (geography Data Type)
- STSymDifference_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STSymDifference (geography Data Type)
ms.assetid: 82bbfa2c-a61b-4f41-9bf8-6f720f363bae
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 079121e8dda953a16bb5d262a0d1c1b2f45d19f4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="stsymdifference-geography-data-type"></a>STSymDifference（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回一个对象，表示之一中的所有点**geography**实例或另一个**geography**实例，但不是在两个实例的那些点。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STSymDifference ( other_geography )  
```  
  
## <a name="arguments"></a>参数  
 *other_geography*  
 是另一种**geography**除了对其调用 STSymDistance() 实例之外的实例。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**地理位置**  
  
 CLR 返回类型： **SqlGeography**  
  
## <a name="remarks"></a>注释  
 如果此方法将始终返回 null 的空间引用标识符 (Srid) **geography**实例不匹配。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持大于半球的空间实例。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的服务器上的可能结果集已扩展到**FullGlobe**实例。  
  
 只有在输入实例包含圆弧线段时，结果才会包含圆弧线段。  
  
## <a name="examples"></a>示例  
  
### <a name="a-computing-the-symmetric-difference-of-two-polygons"></a>A. 计算两个多边形的余集  
 以下示例使用 `STSymDifference()` 计算两个 `Polygon` 实例的余集。  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SET @h = geography::STGeomFromText('POLYGON((-122.351 47.656, -122.341 47.656, -122.341 47.661, -122.351 47.661, -122.351 47.656))', 4326);  
SELECT @g.STSymDifference(@h).ToString();  
```  
  
### <a name="b-computing-the-symmetric-difference-with-fullglobe"></a>B. 计算与 FullGlobe 的余集  
 以下示例计算 `Polygon` 与 `FullGlobe` 的余集。  
  
```
 DECLARE @g geography = 'POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STSymDifference('FULLGLOBE').ToString();
 ```  
  
## <a name="see-also"></a>另请参阅  
 [地域实例上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

