---
title: "STNumCurves (geometry 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STNumCurves method (geometry)
ms.assetid: 20c2fa0b-656b-4519-b34c-cc8f094290d4
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 92cf7af65b64c412aff37311ccf1e9b44484968b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="stnumcurves-geometry-data-type"></a>STNumCurves（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

此方法返回中的曲线数目**几何图形**实例的一维空间数据类型实例时。 一维空间数据类型包括**LineString**， **CircularString**，和**CompoundCurve**。 `STNumCurves`（） 仅适用于简单类型;它并不适用于**几何图形**集合喜欢**MultiLineString**。
  
## <a name="syntax"></a>语法  
  
```  
  
.STNumCurves()  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**几何图形**  
  
 CLR 返回类型： **SqlGeometry**  
  
## <a name="remarks"></a>注释  
 一维空**几何图形**实例，则返回 0。 **NULL**时返回**几何图形**实例不是一维实例或未初始化的实例。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-stnumcurves-on-a-circularstring-instance"></a>A. 对 CircularString 实例使用 STNumCurves()  
 下面的示例演示如何获取 `CircularString` 实例中的曲线数量：  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::Parse('CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0)');  
 SELECT @g.STNumCurves();
 ```  
  
### <a name="b-using-stnumcurves-on-a-compoundcurve-instance"></a>B. 对 CompoundCurve 实例使用 STNumCurves()  
 下面的示例使用 `STNumCurves()` 返回 `CompoundCurve` 实例中的曲线数量。  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0))');  
 SELECT @g.STNumCurves();
 ```  
  
## <a name="see-also"></a>另请参阅  
 [空间数据类型概述](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

