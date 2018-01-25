---
title: "STEndpoint (geometry 数据类型) |Microsoft 文档"
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
- STEndpoint (geometry Data Type)
- STEndpoint_TSQL
dev_langs: TSQL
helpviewer_keywords: STEndpoint (geometry Data Type)
ms.assetid: 61773c45-b568-4e0c-94da-1310c42de7f5
caps.latest.revision: "21"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1ab1d1e533897f3042977902c2b7938dbe048e00
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="stendpoint-geometry-data-type"></a>STEndpoint（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回的终结点**几何图形**实例。
  
## <a name="syntax"></a>语法  
  
```  
  
.STEndPoint ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**几何图形**  
  
 CLR 返回类型： **SqlGeometry**  
  
 打开地理空间联盟 (OGC) 类型：**点**  
  
## <a name="remarks"></a>注释  
 `STEndPoint()`等效于[STPointN](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md) (x.NumPoints())。  
  
 此方法将返回 null，如果在一个空上调用**几何图形**实例。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `LineString` 创建 `STGeomFromText()` 实例，并使用 `STEndpoint()` 检索 `LineString` 的终点。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STEndPoint().ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

