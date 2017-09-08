---
title: "筛选器 (geometry 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Filter
- Filter_TSQL
- Filter (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Filter method
ms.assetid: 3d629a39-157e-4159-a3ca-a3c2e0ed4160
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: de93cc3be1f1a571b82c2d9ff2943af222f4f337
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="filter-geometry-data-type"></a>Filter（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

提供快速、 只索引交集方法可确定一个方法**几何图形**实例与另一个相交**几何图形**实例，假设索引可用。
  
如果返回 1**几何图形**实例可能与另一个相交**几何图形**实例。 此方法可能会产生 false 正返回时，，则准确结果可能为计划依赖项。 返回准确的 0 值 （true 负返回），如果没有的交集**几何图形**找到实例。
  
在索引不可用，或未使用的位置的情况下，该方法将返回与相同的值**STIntersects()**使用相同的参数调用时。
  
## <a name="syntax"></a>语法  
  
```  
  
.Filter ( other_geometry )  
```  
  
## <a name="arguments"></a>参数  
 *other_geometry*  
 是另一种**几何图形**实例要针对对其调用 Filter() 实例进行比较。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**位**  
  
 CLR 返回类型： **SqlBoolean**  
  
## <a name="remarks"></a>注释  
 此方法是不具有确定性的方法，而且不精确。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `Filter()` 确定两个 `geometry` 实例是否彼此相交。  
  
```  
CREATE TABLE sample (id int primary key, g geometry);  
GO  
INSERT INTO sample VALUES  
   (0, geometry::Point(0, 0, 0)),  
   (1, geometry::Point(0, 1, 0)),  
   (2, geometry::Point(0, 2, 0)),  
   (3, geometry::Point(0, 3, 0)),  
   (4, geometry::Point(0, 4, 0));  
  
CREATE SPATIAL INDEX sample_idx ON sample(g)  
WITH (bounding_box = (-8000, -8000, 8000, 8000));  
GO  
SELECT id  
FROM sample   
WHERE g.Filter(geometry::Parse('POLYGON((-1 -1, 1 -1, 1 1, -1 1, -1 -1))')) = 1;  
```  
  
## <a name="see-also"></a>另请参阅  
 [在几何图形实例的扩展的方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [STIntersects（geography 数据类型）](../../t-sql/spatial-geometry/stintersects-geometry-data-type.md)  
  
  


