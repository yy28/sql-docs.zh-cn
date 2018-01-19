---
title: "InstanceOf (geometry 数据类型) |Microsoft 文档"
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
- InstanceOf
- InstanceOf_TSQL
dev_langs: TSQL
helpviewer_keywords: InstanceOf (geometry Data Type)
ms.assetid: fdea1248-29a4-4bab-a60d-a1b359b5e109
caps.latest.revision: "26"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 524e084112d2b9a8b7fe51188d50e9f518aba488
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="instanceof-geometry-data-type"></a>InstanceOf（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

测试方法**几何图形**实例是否与指定的类型相同。 如果返回 1 的一种**几何图形**实例与指定的类型相同，或如果指定的类型是祖先的实例类型; 否则，返回 0。
  
## <a name="syntax"></a>语法  
  
```  
  
.InstanceOf (geometry_type )  
```  
  
## <a name="arguments"></a>参数  
 *geometry_type*  
 是**nvarchar （4000)** 15 中公开的类型之一指定字符串**几何图形**类型层次结构。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**位**  
  
 CLR 返回类型： **SqlBoolean**  
  
## <a name="remarks"></a>注释  
 该方法的输入必须是以下之一：**几何图形**，**点**，**曲线**， **LineString**， **CircularString**， **CompoundCurve**，**面**，**多边形**， **CurvePolygon**， **GeometryCollection**， **MultiSurface**， **MultiPolygon**， **MultiCurve**， **MultiLineString**，和**MultiPoint**。 此方法将引发**ArgumentException**如果其他任何字符串用于输入。  
  
## <a name="examples"></a>示例  
 下面的示例创建一个 `MultiPoint` 实例，并使用 `InstanceOf()` 查看该实例是否为 `GeometryCollection`。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT(0 0, 13.5 2, 7 19)', 0);  
SELECT @g.InstanceOf('GEOMETRYCOLLECTION');  
```  
  
## <a name="see-also"></a>另请参阅  
 [几何图形实例上的扩展方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

