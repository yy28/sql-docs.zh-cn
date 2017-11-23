---
title: "NumRings (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- NumRings_TSQL
- NumRings
dev_langs: TSQL
helpviewer_keywords: NumRings method
ms.assetid: 0e4e4fa2-b608-4cc4-98ba-0845ddb4214c
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4816f581690b5d68d970310a406de3f48ddb4fff
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="numrings-geography-data-type"></a>NumRings（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回的环中总数**多边形**实例。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **geography**键入，外部和内部环没有区分开，因为可将任何环是外部环。  
  
## <a name="syntax"></a>语法  
  
```  
  
.NumRings ()  
```  
  
## <a name="return-type"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型： **int**  
  
 CLR 返回类型： **SqlInt32**  
  
## <a name="remarks"></a>注释  
 如果这不是，此方法将返回 NULL**多边形**实例，并将返回 0，如果该实例为空。 此方法是精确方法。  
  
## <a name="examples"></a>示例  
 下面的示例创建一个具有两个环的 `Polygon` 实例并确认该实例具有两个环。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653), (-122.357 47.654, -122.357 47.657, -122.349 47.657, -122.349 47.650, -122.357 47.654))', 4326);  
SELECT @g.NumRings();  
```  
  
## <a name="see-also"></a>另请参阅  
 [地理实例上的扩展方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
