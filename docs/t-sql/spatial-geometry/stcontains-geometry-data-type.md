---
title: "STContains (geometry 数据类型) |Microsoft 文档"
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
- STContains (geometry Data Type)
- STContains_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STContains (geometry Data Type)
ms.assetid: 865ceca1-9200-45ed-a7d8-e286e2679fdc
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1a56fd873786ed78c54f5c9f11059b06d30c6ed0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="stcontains-geometry-data-type"></a>STContains（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

如果返回 1**几何图形**实例完全包含另一个**几何图形**实例。 如果它不，返回 0。
  
## <a name="syntax"></a>语法  
  
```  
  
.STContains ( other_geometry )  
```  
  
## <a name="arguments"></a>参数  
 *other_geometry*  
 是另一种**几何图形**实例要针对的实例上进行比较`STContains()`调用。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**位**  
  
 CLR 返回类型： **SqlBoolean**  
  
## <a name="remarks"></a>注释  
 `STContains()`始终返回 null 如果的空间引用 Id 为 (Srid)**几何图形**实例不匹配。  
  
## <a name="examples"></a>示例  
 以下示例使用 `STContains()` 测试两个 `geometry` 实例，以查看第一个实例是否包含第二个实例。  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 2 0, 2 2, 0 2, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POINT(1 1)', 0);  
SELECT @g.STContains(@h);  
```  
  
## <a name="see-also"></a>另请参阅  
 [空间索引概述](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [在几何图形实例的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


