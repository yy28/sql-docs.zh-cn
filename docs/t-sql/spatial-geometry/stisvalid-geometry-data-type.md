---
title: "STIsValid (geometry 数据类型) |Microsoft 文档"
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
- STIsValid (geometry Data Type)
- STIsValid_TSQL
dev_langs: TSQL
helpviewer_keywords: STIsValid (geometry Data Type)
ms.assetid: 6da39bea-0f67-4660-98fc-d7214f9b2138
caps.latest.revision: "23"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 436cab211eceff9eb286b4e44e90aa3f64b9d03c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="stisvalid-geometry-data-type"></a>STIsValid（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回 true 如果**几何图形**实例是格式良好，基于其开放地理空间联盟 (OGC) 类型。 返回 false 如果**几何图形**实例不是格式正确。
  
## <a name="syntax"></a>语法  
  
```  
  
.STIsValid ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**位**  
  
 CLR 返回类型： **SqlBoolean**  
  
## <a name="remarks"></a>注释  
 OGC 种**几何图形**实例可以通过调用来确定[STGeometryType()](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]唯一有效的生成**几何图形**实例，但允许存储和检索集合中的无效的实例。 可使用 `MakeValid()` 方法检索表示任何无效实例的相同点集的有效实例。  
  
## <a name="examples"></a>示例  
 下面的示例创建一个空的 `geometry` 实例并使用 `STIsValid()` 来测试该实例是否有效。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STIsValid();  
```  
  
## <a name="see-also"></a>另请参阅  
 [STGeometryType &#40; geometry 数据类型 &#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)   
 [MakeValid（geometry 数据类型）](../../t-sql/spatial-geometry/makevalid-geometry-data-type.md)   
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

