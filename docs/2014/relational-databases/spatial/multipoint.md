---
title: MultiPoint | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MultiPoint geometry subtype [SQL Server]
ms.assetid: 2aaab211-3aba-4dbd-90b7-095d997b1f62
caps.latest.revision: 15
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 0106449b66e1f4c55edd28abfd4e2fab67626080
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127495"
---
# <a name="multipoint"></a>MultiPoint
  A`MultiPoint`是零个或多个点的集合。 `MultiPoint` 实例的边界为空。  
  
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
  
  