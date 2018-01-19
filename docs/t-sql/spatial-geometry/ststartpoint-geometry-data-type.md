---
title: "STStartPoint (geometry 数据类型) |Microsoft 文档"
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
- STStartPoint_TSQL
- STStartPoint (geometry Data Type)
dev_langs: TSQL
helpviewer_keywords: STStartPoint (geometry Data Type)
ms.assetid: 049917db-3f76-4053-8cd2-bc54158e89bc
caps.latest.revision: "20"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 10783ac688124de5ef5ed19f59d4817599b4a9a0
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="ststartpoint-geometry-data-type"></a>STStartPoint（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回的起始点**几何图形**实例。
  
## <a name="syntax"></a>语法  
  
```  
  
.STStartPoint ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**几何图形**  
  
 CLR 返回类型： **SqlGeometry**  
  
 打开地理空间联盟 (OGC) 类型：**点**  
  
## <a name="remarks"></a>注释  
 `STStartPoint()`等效于[STPointN](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md) (1)。  
  
## <a name="examples"></a>示例  
 下面的示例创建一个 `LineString` 实例，并使用 `STStartPoint()` 检索该实例的起点。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0;  
SELECT @g.STStartPoint().ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [STPointN（geometry 数据类型）](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md)   
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

