---
title: MultiPoint | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- dbe-spatial
ms.topic: conceptual
helpviewer_keywords:
- MultiPoint geometry subtype [SQL Server]
ms.assetid: 2aaab211-3aba-4dbd-90b7-095d997b1f62
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3c4f76eed814be25a50fe0c0b8ed090672515dbb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48048693"
---
# <a name="multipoint"></a>MultiPoint
  一个`MultiPoint`是零个或多个点的集合。 `MultiPoint` 实例的边界为空。  
  
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
  
## <a name="see-also"></a>请参阅  
 [点](point.md)   
 [空间数据 (SQL Server)](spatial-data-sql-server.md)  
  
  
