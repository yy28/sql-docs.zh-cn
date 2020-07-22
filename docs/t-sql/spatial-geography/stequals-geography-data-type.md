---
title: STEquals（geography 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STEquals_TSQL
- STEquals (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STEquals method
ms.assetid: 0766ff37-0b9e-49bf-83c0-019f4354fe44
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 730e84147c4201f9eca316335d2328dd50ceae76
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552498"
---
# <a name="stequals-geography-data-type"></a>STEquals（geography 数据类型）
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  如果一个 geography 实例表示的点集与另一个 geography 实例表示的点集相同，则返回 1   。 否则，返回 0。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STEquals ( other_geography )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>参数
 other_geography   
 与对其调用 `STEquals()` 的实例进行比较的其他 geography 实例。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：bit   
  
 CLR 返回类型：SqlBoolean   
  
## <a name="remarks"></a>备注  
 如果 geography 实例的空间引用 ID (SRID) 不匹配，则此方法始终返回 null  。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `STGeomFromText()` 创建两个等效但又不完全相等的 `geography` 实例，并使用 `STEquals()` 测试它们的等效性。 因为 `LINESTRING` 和 `POINT` 包含在 `POLYGON` 中，所以这两个实例相等。  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('GEOMETRYCOLLECTION(POLYGON((-122.368 47.658, -122.338 47.649, -122.338 47.658, -122.368 47.658, -122.368 47.658)), LINESTRING(-122.360 47.656, -122.343 47.656), POINT (-122.35 47.656))', 4326);  
SET @h = geography::STGeomFromText('POLYGON((-122.368 47.658, -122.338 47.649, -122.338 47.658, -122.368 47.658, -122.368 47.658))', 4326);  
SELECT @g.STEquals(@h);  
```  
  
## <a name="see-also"></a>另请参阅  
 [地理实例上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
