---
title: MultiPoint | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-spatial
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: MultiPoint geometry subtype [SQL Server]
ms.assetid: 2aaab211-3aba-4dbd-90b7-095d997b1f62
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 425b5024aac9db4e30d8042b115d20041a957b1c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="multipoint"></a>MultiPoint
  **MultiPoint** 是零个点或更多个点的集合。 **MultiPoint** 实例的边界为空。  
  
## <a name="examples"></a>示例  
 下面的示例创建一个 `geometry MultiPoint` 实例，该实例的 SRID 为 23 且包含两个点：一个点的坐标为 (2, 3)，另一个点的坐标为 (7, 8)，Z 值为 9.5。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT((2 3), (7 8 9.5))', 23);  
```  
  
 该 `MultiPoint` 实例也可使用 `STMPointFromText()` 表示，如下所示。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STMPointFromText('MULTIPOINT((2 3), (7 8 9.5))', 23);  
```  
  
 下面的示例使用方法 `STGeometryN()` 来检索有关集合中第一个点的说明。  
  
```  
SELECT @g.STGeometryN(1).STAsText();  
```  
  
## <a name="see-also"></a>另请参阅  
 [点](../../relational-databases/spatial/point.md)   
 [空间数据 (SQL Server)](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
