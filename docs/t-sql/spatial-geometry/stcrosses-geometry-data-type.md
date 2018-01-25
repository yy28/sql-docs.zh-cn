---
title: "STCrosses (geometry 数据类型) |Microsoft 文档"
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
- STCrosses (geometry Data Type)
- STCrosses_TSQL
dev_langs: TSQL
helpviewer_keywords: STCrosses (geometry Data Type)
ms.assetid: 3e3fc065-555a-4bee-8b71-e92f3dc62a4f
caps.latest.revision: "21"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f1b1588649574e16f3bf46ae6d3fa06079f16a39
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="stcrosses-geometry-data-type"></a>STCrosses（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

如果返回 1**几何图形**实例交叉点**几何图形**实例。 如果它不，返回 0。
  
## <a name="syntax"></a>语法  
  
```  
  
.STCrosses ( other_geometry )  
```  
  
## <a name="arguments"></a>参数  
 *other_geometry*  
 是另一种**几何图形**实例要针对的实例上进行比较`STCrosses()`调用。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**位**  
  
 CLR 返回类型： **SqlBoolean**  
  
## <a name="remarks"></a>注释  
 两个**几何图形**实例跨如果以下条件都为 true:  
  
-   这两个交集**几何图形**实例导致其维度的源的最大尺寸小于几何图形**几何图形**实例。  
  
-   交集集是内部到这两个源**几何图形**实例。  
  
 如果此方法将始终返回 null 的空间引用 Id 为 (Srid)**几何图形**实例不匹配。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `STCrosses()` 来测试两个 `geometry` 实例，以查看它们是否相交。  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0)', 0);  
SET @h = geometry::STGeomFromText('LINESTRING(0 0, 2 2)', 0);  
SELECT @g.STCrosses(@h);  
```  
  
## <a name="see-also"></a>另请参阅  
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

