---
title: "STIsSimple (geometry 数据类型) |Microsoft 文档"
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
- STIsSimple_TSQL
- STIsSimple (geometry Data Type)
dev_langs: TSQL
helpviewer_keywords: STIsSimple (geometry Data Type)
ms.assetid: da8f45d4-4f9c-405d-b883-760eb5344a71
caps.latest.revision: "20"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5240f2a8c9dc28f9256db87106fdcfaf0b689034
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="stissimple-geometry-data-type"></a>STIsSimple（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

如果返回 1**几何图形**实例很简单，定义通过开放地理空间联盟 (OGC)。 如果将返回 0**几何图形**实例不是简单。
  
## <a name="syntax"></a>语法  
  
```  
  
.STIsSimple ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**位**  
  
 CLR 返回类型： **SqlBoolean**  
  
## <a name="remarks"></a>注释  
 为简单，**几何图形**实例必须满足所有以下要求：  
  
-   实例的每个图形不能与自身相交，但其终点除外。  
  
-   实例的任何两个图形可在某个点上相交，但两个边界上的点除外。  
  
## <a name="examples"></a>示例  
 下面的示例创建一个非简单 `LineString` 实例，该实例与自身相交并使用 `STIsSimple()` 来测试 `LineString` 是否为简单类型。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 0 2, 2 0)', 0);  
SELECT @g.STIsSimple();  
```  
  
## <a name="see-also"></a>另请参阅  
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

