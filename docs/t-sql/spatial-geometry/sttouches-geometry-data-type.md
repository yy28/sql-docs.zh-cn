---
title: "STTouches (geometry 数据类型) |Microsoft 文档"
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
- STTouches (geometry Data Type)
- STTouches_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STTouches (geometry Data Type)
ms.assetid: af3650b4-26da-4600-9cc2-1be71dd76a14
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c29c232e585a083b0b4e97b081b66fcf7e03d5fb
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="sttouches-geometry-data-type"></a>STTouches（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

如果返回 1**几何图形**实例逐项涉及另一个**几何图形**实例。 如果它不，返回 0。
  
## <a name="syntax"></a>语法  
  
```  
  
.STTouches ( other_geometry )  
```  
  
## <a name="arguments"></a>参数  
 *other_geometry*  
 是另一种**几何图形**实例要针对的实例上进行比较`STTouches()`调用。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**位**  
  
 CLR 返回类型： **SqlBoolean**  
  
## <a name="remarks"></a>注释  
 两个**几何图形**实例 touch 如果它们的点集相交，但其内部并不相交。  
  
 如果此方法将始终返回 null 的空间引用 Id 为 (Srid)**几何图形**实例不匹配。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `STTouches()` 来测试两个 `geometry` 实例，以查看它们是否接触。  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0, 4 2)', 0);  
SET @h = geometry::STGeomFromText('POINT(1 1)', 0);  
SELECT @g.STTouches(@h);  
```  
  
## <a name="see-also"></a>另请参阅  
 [空间索引概述](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [在几何图形实例的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


