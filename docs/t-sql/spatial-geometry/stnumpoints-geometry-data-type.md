---
title: "STNumPoints (geometry 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- STNumPoints_TSQL
- STNumPoints (geometry Data Type)
dev_langs: TSQL
helpviewer_keywords: STNumPoints (geometry Data Type)
ms.assetid: a19520fc-7f91-4a2c-856f-4d8b99a7e496
caps.latest.revision: "16"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2d84f2bbbfafdb7667d1263d026ef76693fde57d
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="stnumpoints-geometry-data-type"></a>STNumPoints（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  返回每个中的图表中的点数量的总和**几何图形**实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STNumPoints ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型： **int**  
  
 CLR 返回类型： **SqlInt32**  
  
## <a name="remarks"></a>注释  
 此方法计算中的说明的点**几何图形**实例。 重复的点将计算在内。 如果此实例是**集合**类型，此方法返回的点和在每个元素。  
  
## <a name="examples"></a>示例  
 下面的示例创建一个 `LineString` 实例，并使用 `STNumPoints()` 确定该实例说明中使用的点数。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STNumPoints();  
```  
  
## <a name="see-also"></a>另请参阅  
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
