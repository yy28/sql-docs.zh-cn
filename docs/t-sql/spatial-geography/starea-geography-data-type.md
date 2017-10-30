---
title: "STArea (geography 数据类型) |Microsoft 文档"
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
- STArea (geography Data Type)
- STArea_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STArea method
ms.assetid: cfc0b0e0-7fde-431a-863f-d13f3b1b1bef
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e96ee94983746e162990b8eadad4f6affb4f92fd
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="starea-geography-data-type"></a>STArea（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回的总表面积**geography**实例。 在使用的空间引用标识符的度量值的单元方形内返回结果为 STArea() **geography**实例; 例如，如果实例的 SRID 4326，STArea() 返回的结果中平方米。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STArea ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型： **float**  
  
 CLR 返回类型： **SqlDouble**  
  
## <a name="remarks"></a>注释  
 如果将 STArea() 返回 0 **geography**实例包含仅 0 和 1 维图形，或是否为空。  
  
> [!NOTE]  
>  上的方法**geography**数据类型的生成一个度量值返回值将具有不同的结果基于在方法中使用的实例的 SRID。 Srid 的详细信息，请参阅[空间引用标识符 &#40;Srid &#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md).  
  
## <a name="examples"></a>示例  
 下面的示例使用`STArea()`创建`Polygon``geography`实例，并计算在多边形区域。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.STArea();  
```  
  
## <a name="see-also"></a>另请参阅  
 [地域实例上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

