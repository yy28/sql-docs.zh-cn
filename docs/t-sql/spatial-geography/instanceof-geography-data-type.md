---
title: InstanceOf（geography 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- InstanceOf
- InstanceOf_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- InstanceOf method
ms.assetid: 1eaed0e4-1c72-45a9-9926-5b513335cf33
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e0ef6816efa98d3e9b2da27525d700fb4eba2501
ms.sourcegitcommit: c3b190f8f87a4c80bc9126bb244896197a6dc453
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852992"
---
# <a name="instanceof-geography-data-type"></a>InstanceOf（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

测试 **geography** 实例是否与指定的类型相同。  
  
## <a name="syntax"></a>语法  
  
```sql  
  
.InstanceOf ( 'geography_type')  
```  
  
## <a name="arguments"></a>参数  
*geography_type*  
**nvarchar(4000)** 字符串，用于指定 **geography** 类型层次结构中公开的 16 个类型之一。  
  
## <a name="return-types"></a>返回类型  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：bit  
  
CLR 返回类型：**SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
如果 **geography** 实例的类型与指定的类型相同，或者指定的类型是该实例类型的上级，则返回 1；否则，返回 0。  
  
这种 geography 数据类型方法支持大于半球的 FullGlobe 实例或空间实例。  
  
方法的输入必须是以下类型之一：Geometry、Point、Curve、LineString、CircularString、Surface、Polygon、CurvePolygon、**GeometryCollection**、**MultiSurface**、**MultiPolygon、MultiCurve、MultiLineString**、**MultiPoint** 或 **FullGlobe**。  
  
如果将任何其他字符串用于输入，此方法将引发 `ArgumentException`。  
  
此方法不精确。  
  
## <a name="examples"></a>示例  
以下示例创建一个 `MultiPoint` 实例，并使用 `InstanceOf()` 查看该实例是否为 `GeometryCollection`。  
  
```sql  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('MULTIPOINT(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.InstanceOf('GEOMETRYCOLLECTION');  
```  
  
## <a name="see-also"></a>另请参阅  
 [地理实例上的扩展方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
