---
title: Filter（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 328ff71b368382a1aa9a06f9ca9274089679c729
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33064024"
---
# <a name="filter-geometry-data-type"></a>Filter（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

一种方法，可提供一种快速、仅索引相交的方法，用于确定一个 **geometry** 实例是否与另一个 **geometry** 实例相交（假定有可用索引）。
  
如果一个 **geometry** 实例与另一个 **geometry** 实例存在相交的可能，则返回 1。 该方法可能产生假正返回，并且确切结果可能依赖于计划。 如果 **geometry** 实例之间不存在相交，则返回精确的 0 值（真负返回）。
  
在无可用索引或未使用索引的情况下，该方法返回的值将与使用相同参数调用 STIntersects() 返回的值相同。
  
## <a name="syntax"></a>语法  
  
```  
  
.Filter ( other_geometry )  
```  
  
## <a name="arguments"></a>参数  
 *other_geometry*  
 将与调用 Filter() 的实例进行比较的另一个 geometry 实例。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：bit  
  
 CLR 返回类型：SqlBoolean  
  
## <a name="remarks"></a>Remarks  
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
 [Geometry 实例上的扩展方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [STIntersects（geography 数据类型）](../../t-sql/spatial-geometry/stintersects-geometry-data-type.md)  
  
  

