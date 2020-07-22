---
title: STNumCurves（geography 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STNumCurves
- STNumCurves_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumCurves method (geography)
ms.assetid: e98a56c2-8496-4dfd-9b37-7f3c4ca9b2b5
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 07626f3ded35ee9c4075e08765b76974d1c1b209
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86556044"
---
# <a name="stnumcurves-geography-data-type"></a>STNumCurves（geography 数据类型）
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  返回一维 geography 实例中的曲线数  。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STNumCurves()  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>返回类型
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geography   
  
 CLR 返回类型：SqlGeography   
  
## <a name="remarks"></a>备注  
 一维空间数据类型包括 LineString、CircularString 和 CompoundCurve    。 空的一维 geography 实例返回 0  。  
  
 `STNumCurves`() 仅适用于简单类型，它不适用于 MultiLineString 之类的 geography 集合   。 当 geography 实例不是一维数据类型时，将返回 NULL   。  
  
 对于未初始化的 geography 实例，返回 Null   。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-stnumcurves-on-a-circularstring-instance"></a>A. 对 CircularString 实例使用 STNumCurves()  
 下面的示例演示如何获取 `CircularString` 实例中的曲线数量：  
  
```
 DECLARE @g geography; 
 SET @g = geography::Parse('CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)');  
 SELECT @g.STNumCurves();
 ```  
  
### <a name="b-using-stnumcurves-on-a-compoundcurve-instance"></a>B. 对 CompoundCurve 实例使用 STNumCurves()  
 下面的示例使用 `STNumCurves()` 返回 `CompoundCurve` 实例中的曲线数量。  
  
```
 DECLARE @g geography;  
 SET @g = geography::Parse('COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))');  
 SELECT @g.STNumCurves();
 ```  
  
## <a name="see-also"></a>另请参阅  
 [空间数据类型概述](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [地理实例上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
