---
title: STContains（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STContains (geometry Data Type)
- STContains_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STContains (geometry Data Type)
ms.assetid: 865ceca1-9200-45ed-a7d8-e286e2679fdc
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 0244ff677c11d40153afb302243bd714e3438480
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86555983"
---
# <a name="stcontains-geometry-data-type"></a>STContains（geometry 数据类型）
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

如果一个 **geometry** 实例完全包含另一个 **geometry** 实例，则返回 1。 否则，返回 0。
  
## <a name="syntax"></a>语法  
  
```  
  
.STContains ( other_geometry )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>参数
 *other_geometry*  
 将与调用 `STContains()` 的实例进行比较的另一个 geometry 实例。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：bit   
  
 CLR 返回类型：SqlBoolean   
  
## <a name="remarks"></a>备注  
 如果 **geometry** 实例的空间引用 ID (SRID) 不匹配，则 `STContains()` 始终返回 null。  
  
## <a name="examples"></a>示例  
 以下示例使用 `STContains()` 测试两个 `geometry` 实例，以查看第一个实例是否包含第二个实例。  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 2 0, 2 2, 0 2, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POINT(1 1)', 0);  
SELECT @g.STContains(@h);  
```  
  
## <a name="see-also"></a>另请参阅  
 [空间索引概述](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

