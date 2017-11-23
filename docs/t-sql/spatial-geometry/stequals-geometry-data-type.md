---
title: "STEquals (geometry 数据类型) |Microsoft 文档"
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
- STEquals (geometry Data Type)
- STEquals_TSQL
dev_langs: TSQL
helpviewer_keywords: STEquals (geometry Data Type)
ms.assetid: 808f0e25-9e68-4ba7-9329-07ec950698f3
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e6038e3dbf825fd94590cfdb1562ff5b36ffb80e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="stequals-geometry-data-type"></a>STEquals（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

如果返回 1**几何图形**实例表示相同的点将设置为另一个**几何图形**实例。 如果它不，返回 0。
  
## <a name="syntax"></a>语法  
  
```  
  
.STEquals ( other_geometry )  
```  
  
## <a name="arguments"></a>参数  
 *other_geometry*  
 是另一种**几何图形**实例要针对的实例上进行比较`STEquals()`调用。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**位**  
  
 CLR 返回类型： **SqlBoolean**  
  
## <a name="remarks"></a>注释  
 如果此方法将始终返回 null 的空间引用 Id 为 (Srid)**几何图形**实例不匹配。  
  
## <a name="examples"></a>示例  
 下面的示例创建两个`geometry`实例`STGeomFromText()`，是相等的但不是完全相等，并使用`STEquals()`若要测试其是否相等。  
  
```  
DECLARE @g geometry  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0, 4 2)', 0);  
SET @h = geometry::STGeomFromText('MULTILINESTRING((4 2, 2 0), (0 2, 2 0))', 0);  
SELECT @g.STEquals(@h);  
```  
  
## <a name="see-also"></a>另请参阅  
 [空间索引概述](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

