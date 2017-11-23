---
title: "MakeValid (geometry 数据类型) |Microsoft 文档"
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
- MakeValid
- MakeValid_TSQL
dev_langs: TSQL
helpviewer_keywords: MakeValid (geometry Data Type)
ms.assetid: 38673010-ab77-4ebb-9c4d-b26b79e3b7ea
caps.latest.revision: "22"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: fd3f338dba1020d2424b69a5794fe27f3e151775
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="makevalid-geometry-data-type"></a>MakeValid（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

将转换无效**几何图形**实例**几何图形**与有效的开放地理空间联盟 (OGC) 类型的实例。
  
## <a name="syntax"></a>语法  
  
```  
  
.MakeValid ()  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**几何图形**  
  
 CLR 返回类型： **SqlGeometry**  
  
## <a name="remarks"></a>注释  
 此方法可能会更改导致的一种**几何图形**实例，以及导致的点**几何图形**实例轻微移位。  
  
## <a name="examples"></a>示例  
 第一个示例创建一个与其自身重叠的无效 `LineString` 实例，并使用 `STIsValid()` 来确认该实例是无效实例。 `STIsValid()` 针对无效实例返回值 0。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 1 1, 1 0, 1 1, 2 2)', 0);  
SELECT @g.STIsValid();  
```  
  
 第二个示例使用 `MakeValid()` 使该实例有效并测试该实例是否的确有效。 `STIsValid()` 针对有效实例返回值 1。  
  
```  
SET @g = @g.MakeValid();  
SELECT @g.STIsValid();  
```  
  
 第三个示例验证是否已将该实例更改为有效实例。  
  
```  
SELECT @g.ToString();  
```  
  
 在此示例中，在选择 `LineString` 实例时，值将作为有效的 `MultiLineString` 实例返回。  
  
```  
MULTILINESTRING ((0 2, 1 1, 2 2), (1 1, 1 0))  
```  
  
 下面的示例将 CircularString 实例转换为 Point 实例。  
  
```  
DECLARE @g geometry = 'CIRCULARSTRING(1 1, 1 1, 1 1)';  
SELECT @g.MakeValid().ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [STIsValid（geometry 数据类型）](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)   
 [几何图形实例上的扩展方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

