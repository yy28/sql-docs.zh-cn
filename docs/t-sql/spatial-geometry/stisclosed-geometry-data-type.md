---
title: STIsClosed（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIsClosed_TSQL
- STIsClosed (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIsClosed (geometry Data Type)
ms.assetid: 14edbb22-df7b-4b8a-b16c-ac477a5d32c1
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 61c72f4953bfad6d54c46b3b710d2f9c0b9f98d7
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552433"
---
# <a name="stisclosed-geometry-data-type"></a>STIsClosed（geometry 数据类型）
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

如果给定的 geometry 实例的起点和终点相同，则返回 1  。 对于 geometrycollection 类型，如果每个包含的 geometry 实例都是闭合的，则返回 1   。 如果该实例不是闭合的，则返回 0。
  
## <a name="syntax"></a>语法  
  
```  
  
.STIsClosed ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>返回类型
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：bit   
  
 CLR 返回类型：SqlBoolean   
  
## <a name="remarks"></a>备注  
 如果 geometry 实例的任何图形是点，或者如果该实例为空，则此方法返回 0  。  
  
 所有 Polygon 实例被视为闭合的  。  
  
## <a name="examples"></a>示例  
 下面的示例创建一个 `LineString` 实例，并使用 `STIsClosed()` 来测试 `LineString` 是否为闭合的。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STIsClosed();  
```  
  
## <a name="see-also"></a>另请参阅  
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

