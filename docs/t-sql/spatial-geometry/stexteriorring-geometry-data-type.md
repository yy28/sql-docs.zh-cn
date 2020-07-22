---
title: STExteriorRing（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STExteriorRing_TSQL
- STExteriorRing (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STExteriorRing (geometry Data Type)
ms.assetid: b402b36f-05bf-4c6d-8cd6-76c0fff19db2
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: a70e75cb86187c01f37738efbae8d5ead6bd35e8
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554313"
---
# <a name="stexteriorring-geometry-data-type"></a>STExteriorRing（geometry 数据类型）
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

返回多边形 geometry 实例的外环  。
  
## <a name="syntax"></a>语法  
  
```  
  
.STExteriorRing ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>返回类型
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geometry   
  
 CLR 返回类型：SqlGeometry   
  
 开放地理空间信息联盟 (OGC) 类型：LineString   
  
## <a name="remarks"></a>备注  
 如果 geometry 实例不是多边形，则此方法返回 NULL   。  
  
## <a name="examples"></a>示例  
 以下示例创建 `Polygon` 实例，并使用 `STExteriorRing()` 以 LineString 的形式返回多边形的外环  。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0),(2 2, 2 1, 1 1, 1 2, 2 2))', 0);  
SELECT @g.STExteriorRing().ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

