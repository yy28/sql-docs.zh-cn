---
title: STIsClosed（geography 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIsClosed (geography Data Type)
- STIsClosed_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STIsClosed method
ms.assetid: eba1643f-07c4-4500-8643-b7e90f908147
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 41a0f923e997951e52b23ed0b1c2860a8c1532b0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85736113"
---
# <a name="stisclosed-geography-data-type"></a>STIsClosed（geography 数据类型）
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  如果给定的 geography 实例的起点和终点相同，则返回 1  。 如果每个包含的 geography 实例都是闭合的，则为 geography 集类型返回 1   。 如果该实例不是闭合的，则返回 0。  
  
 这种 geography 数据类型方法支持大于半球的 FullGlobe 实例或空间实例   。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STIsClosed ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：bit   
  
 CLR 返回类型：SqlBoolean   
  
## <a name="remarks"></a>备注  
 如果 geography 实例的任何图形是点，或者如果该实例为空，则此方法返回 0  。  
  
 如果 FullGlobe 实例是 Polygon 或其他类型的实例，则此方法返回 true   。  
  
 所有 Polygon 实例被视为闭合的  。  
  
## <a name="examples"></a>示例  
 下面的示例创建一个 `Polygon` 实例，并使用 `STIsClosed()` 来测试 `Polygon` 是否为闭合的。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.STIsClosed();  
```  
  
## <a name="see-also"></a>另请参阅  
 [地理实例上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
