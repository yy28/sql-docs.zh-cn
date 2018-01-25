---
title: "STIsRing (geometry 数据类型) |Microsoft 文档"
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
- STIsRing_TSQL
- STIsRing (geometry Data Type)
dev_langs: TSQL
helpviewer_keywords: STIsRing (geometry Data Type)
ms.assetid: ea0063be-1c74-4cc4-ac6f-b65321ddfa54
caps.latest.revision: "21"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e54455f50c306b4a13df2c815b75995fc15dc06a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="stisring-geometry-data-type"></a>STIsRing（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

如果返回 1**几何图形**实例满足以下要求：
-   它是**LineString**实例。  
-   该实例为闭合类型。  
-   该实例为简单类型。  
-   如果将返回 0 **LineString**实例不满足要求。  

 有关**几何图形**实例设置为已关闭和简单，同时[STIsClosed()](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)和[STIsSimple()](../../t-sql/spatial-geometry/stissimple-geometry-data-type.md)必须返回 1 时调用的实例上。 若要确定的实例类型**几何图形**，使用[STGeometryType()](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STIsRing ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**位**  
  
 CLR 返回类型： **SqlBoolean**  
  
## <a name="remarks"></a>注释  
 此方法将返回 null 如果实例不是**LineString**。  
  
## <a name="examples"></a>示例  
 下面的示例创建一个 `LineString` 实例并使用 `STIsRing()` 来测试该实例是否为一个环。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0, 0 0)', 0);  
SELECT @g.STIsRing();  
```  
  
## <a name="see-also"></a>另请参阅  
 [STIsClosed（geometry 数据类型）](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)   
 [STGeometryType &#40; geometry 数据类型 &#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)   
 [STIsSimple &#40; geometry 数据类型 &#41;](../../t-sql/spatial-geometry/stissimple-geometry-data-type.md)   
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

