---
title: STAsText（geography 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STAsText (geography Data Type)
- STAsText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STAsText method
ms.assetid: d3d2635d-ca6c-4205-9d6c-eb939ee314fd
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 17a7d957b5c85ef21889af21de03f6cc2154ac62
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86555165"
---
# <a name="stastext-geography-data-type"></a>STAsText（geography 数据类型）
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  返回 geography 实例的开放地理空间信息联盟 (OGC) 熟知文本 (WKT) 表示形式  。 此文本将不包含该实例传递的任何 Z（标高）或 M（度量）值。  
  
 这种 geography 数据类型方法支持大于半球的 FullGlobe 实例或空间实例   。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STAsText ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>返回类型
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：nvarchar(max)   
  
 CLR 返回类型：**SqlChars**  
  
## <a name="remarks"></a>备注  
 geography 实例的 OGC 类型可通过调用 [STGeometryType()](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md) 来确定。  
  
 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中，服务器上可能返回的结果集已扩展到 FullGlobe 实例  。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `STAsText()` 根据文本创建一个从 (-122.360, 47.656) 到 (-122.343, 47.656) 的 `LineString``geography` 实例。 然后，它以文本的形式返回结果。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>另请参阅  
 [地理实例上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
