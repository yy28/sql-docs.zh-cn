---
title: ReorientObject（geography 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ReorientObject
- ReorientObject_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ReorientObject method (geography)
ms.assetid: e2a1a4f1-211b-4e82-abed-03fc7140a83c
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 6865a5246f7bb0afa7dd280041e98fada88c3099
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86555173"
---
# <a name="reorientobject-geography-data-type"></a>ReorientObject（geography 数据类型）
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

返回 geography 实例以及互换的内部区域和外部区域  。  
  
这种 geography 数据类型方法支持大于半球的 FullGlobe 实例或空间实例   。  
  
## <a name="syntax"></a>语法  
  
```  
  
.ReorientObject (geography)  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>参数
_地理_  
对其调用 `ReorientObject()` 的另一个 geography 实例。  
  
## <a name="return-value"></a>返回值  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geography   
  
CLR 返回类型：SqlGeography   
  
## <a name="remarks"></a>备注  
此方法更改 GeometryCollection 中所有 Polygons 的环方向，但不删除或更改给定集合中的任何 Points或 LineStrings。  
  
如果将 GeometryCollection  传递给此方法，则会重新调整集合中的每个实例，但不会重新调整整个集合。  
  
## <a name="examples"></a>示例  
  
```  
DECLARE @R GEOGRAPHY = GEOGRAPHY::Parse('Polygon((-10 -10, -10 10, 10 10, 10 -10, -10 -10))');  
SELECT @R.ReorientObject().STAsText();  
--Result: POLYGON ((10 10, -10 10, -10 -10, 10 -10, 10 10))  
```  
  
## <a name="see-also"></a>另请参阅  
[地理实例上的扩展方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
