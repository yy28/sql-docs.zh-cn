---
title: "STPointOnSurface (geometry 数据类型) |Microsoft 文档"
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
- STPointOnSurface (geometry Data Type)
- STPointOnSurface_TSQL
dev_langs: TSQL
helpviewer_keywords: STPointOnSurface (geometry Data Type)
ms.assetid: 23b2b8eb-4176-49fb-ace0-92398928d60e
caps.latest.revision: "21"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 281015af6d0c580b27b9f9256c79b0a7e7f1e14a
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="stpointonsurface-geometry-data-type"></a>STPointOnSurface（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回的任意时间点的内部位于**几何图形**实例。
  
## <a name="syntax"></a>语法  
  
```  
  
.STPointOnSurface ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**几何图形**  
  
 CLR 返回类型： **SqlGeometry**  
  
 打开地理空间联盟 (OGC) 类型：**点**  
  
## <a name="remarks"></a>注释  
 如果该实例不为空，则此方法返回 Null。  
  
## <a name="examples"></a>示例  
 下面的示例创建一个 `Polygon` 实例，并使用 `STPointOnSurface()` 查找该实例上的点。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0),(2 2, 2 1, 1 1, 1 2, 2 2))', 0);  
SELECT @g.STPointOnSurface().ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

