---
title: "STIsValid (geography 数据类型) |Microsoft 文档"
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
dev_langs: TSQL
helpviewer_keywords: STIsValid method (geography)
ms.assetid: 1bfe787f-ddf0-4fc7-af6a-570a58faab23
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 89ccf357cdf80dd4140a407b0d364b404b745e81
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="stisvalid-geography-data-type"></a>STIsValid（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  返回 true 如果**geography**实例是格式正确并被识别为有效的地理对象基于其开放地理空间联盟 (OGC) 类型。 返回 false 如果**geography**实例不是格式正确。 此方法是精确方法。  
  
 此 geography 数据类型方法支持**FullGlobe**实例或大于半球的空间实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STIsValid ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**位**  
  
 CLR 返回类型： **SqlBoolean**  
  
## <a name="remarks"></a>注释  
 OGC 种**geography**实例可以通过调用来确定[STGeometryType()](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]唯一有效的生成**geography**实例，但允许存储和检索集合中的无效的实例。 可使用 `MakeValid()` 方法检索表示无效实例的相同点集的有效实例。  
  
## <a name="examples"></a>示例  
 下面的示例创建一个空的 `geography` 实例并使用 `STIsValid()` 来测试该实例是否有效。  
  
```  
DECLARE @g geography = geography::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 4326);  
SELECT @g.STIsValid();  
DECLARE @g geography  
```  
  
## <a name="see-also"></a>另请参阅  
 [STGeometryType &#40; geography 数据类型 &#41;](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md)   
 [MakeValid（geography 数据类型）](../../t-sql/spatial-geography/makevalid-geography-data-type.md)   
 [地理实例上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
