---
title: STGeometryType（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeometryType_TSQL
- STGeometryType (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeometryType (geometry Data Type)
ms.assetid: 224cdc83-aa83-4ad4-bb82-b7481031e910
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3c91ae4decb540d80e371153504121ee22bf3ccc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47663455"
---
# <a name="stgeometrytype-geometry-data-type"></a>STGeometryType（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回由 **geometry** 实例表示的开放地理空间信息联盟 (OGC) 类型名称。
  
## <a name="syntax"></a>语法  
  
```  
  
.STGeometryType ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：nvarchar(4000)  
  
 CLR 返回类型：SqlString  
  
## <a name="remarks"></a>Remarks  
 `STGeometryType()` 可以返回的 OGC 类型名称包括 Point、LineString、CircularString、CompoundCurve、Polygon、CurvePolygon、GeometryCollection、MultiPoint、MultiLineString 和 MultiPolygon。  
  
## <a name="examples"></a>示例  
 下面的示例创建一个 `Polygon` 实例并使用 `STGeometryType()` 确认它是多边形。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0))', 0);  
SELECT @g.STGeometryType();  
```  
  
## <a name="see-also"></a>另请参阅  
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

