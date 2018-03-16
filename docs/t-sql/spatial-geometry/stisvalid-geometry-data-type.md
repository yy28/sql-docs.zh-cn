---
title: "STIsValid（geometry 数据类型）| Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STIsValid (geometry Data Type)
- STIsValid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STIsValid (geometry Data Type)
ms.assetid: 6da39bea-0f67-4660-98fc-d7214f9b2138
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 436cab211eceff9eb286b4e44e90aa3f64b9d03c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="stisvalid-geometry-data-type"></a>STIsValid（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

根据 **geometry** 实例的开放地理空间信息联盟 (OGC) 类型，如果可确定该实例的格式正确，则返回 true。 如果 **geometry** 实例格式不正确，则返回 false。
  
## <a name="syntax"></a>语法  
  
```  
  
.STIsValid ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：bit  
  
 CLR 返回类型：SqlBoolean  
  
## <a name="remarks"></a>Remarks  
 geometry 实例的 OGC 类型可通过调用 [STGeometryType()](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md) 来确定。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 只生成有效的 **geometry** 实例，但允许存储和检索无效的实例。 可使用 `MakeValid()` 方法检索表示任何无效实例的相同点集的有效实例。  
  
## <a name="examples"></a>示例  
 下面的示例创建一个空的 `geometry` 实例并使用 `STIsValid()` 来测试该实例是否有效。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STIsValid();  
```  
  
## <a name="see-also"></a>另请参阅  
 [STGeometryType（geometry 数据类型）](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)   
 [MakeValid（geometry 数据类型）](../../t-sql/spatial-geometry/makevalid-geometry-data-type.md)   
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

