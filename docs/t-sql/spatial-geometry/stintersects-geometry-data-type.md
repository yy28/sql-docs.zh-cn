---
title: STIntersects（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIntersects (geometry Data Type)
- STIntersects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STIntersects (geometry Data Type)
ms.assetid: 7c18f5be-5a29-422e-8ca7-d8a5f38e03f5
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: c3f4d6e606ba37283fee75da148cfe1a54d3cf00
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554268"
---
# <a name="stintersects-geometry-data-type"></a>STIntersects（geometry 数据类型）
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

如果一个 **geometry** 实例与另一个 **geometry** 实例相交，则返回 1。 否则，返回 0。
  
## <a name="syntax"></a>语法  
  
```  
  
.STIntersects ( other_geometry )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>参数
 *other_geometry*  
 将与调用 `STIntersects()` 的实例进行比较的另一个 geometry 实例。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：bit   
  
 CLR 返回类型：SqlBoolean   
  
## <a name="remarks"></a>备注  
 如果 geometry 实例的空间引用 ID (SRID) 不匹配，则此方法始终返回 null  。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `STIntersects()` 确定两个 `geometry` 实例是否彼此相交。  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0, 4 2)', 0);  
SET @h = geometry::STGeomFromText('POINT(1 1)', 0);  
SELECT @g.STIntersects(@h);  
```  
  
## <a name="see-also"></a>另请参阅  
 [空间索引概述](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

