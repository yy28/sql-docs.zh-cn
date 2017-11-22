---
title: "STLength (geometry 数据类型) |Microsoft 文档"
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
- STLength_TSQL
- STLength (geometry Data Type)
dev_langs: TSQL
helpviewer_keywords: STLength (geometry Data Type)
ms.assetid: e34dc620-2a65-4248-b099-fff91830ab98
caps.latest.revision: "20"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 476d1c761939c25ace4dbb67720537dd10a16531
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="stlength-geometry-data-type"></a>STLength（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回中的元素的总长度**几何图形**实例。
  
## <a name="syntax"></a>语法  
  
```  
  
.STLength ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型： **float**  
  
 CLR 返回类型： **SqlDouble**  
  
## <a name="remarks"></a>注释  
 如果**几何图形**实例是否闭合、 其长度的计算方式解决该实例的总长度为; 任何多边形的长度是其外围和点的长度为 0。 任何的长度**geometrycollection**类型是其包含的长度的总和**几何图形**实例。  
  
 STLength() 对有效和无效的 LineString 均适用。 通常，LineString 会因可能由 GPS 跟踪不准确之类的异常引起的段重叠而无效。 STLength() 不会删除重叠或无效的段。 它将重叠和无效的段包括在其返回的长度值中。 MakeValid() 方法可以从 LineString 中删除重叠段。  
  
## <a name="examples"></a>示例  
 下面的示例创建 `LineString` 实例并使用 `STLength()` 确定该实例的长度。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STLength();  
```  
  
## <a name="see-also"></a>另请参阅  
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

