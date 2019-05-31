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
manager: craigg
ms.openlocfilehash: e2945b08eaf0a22c6c83bd412e97c729bedfdfea
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/20/2019
ms.locfileid: "65936351"
---
# <a name="reorientobject-geography-data-type"></a>ReorientObject（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

返回 geography 实例以及互换的内部区域和外部区域  。  
  
这种 geography 数据类型方法支持大于半球的 FullGlobe 实例或空间实例   。  
  
## <a name="syntax"></a>语法  
  
```  
  
.ReorientObject (geography)  
```  
  
## <a name="arguments"></a>参数  
_地理_  
对其调用 `ReorientObject()` 的另一个 geography 实例  。  
  
## <a name="return-value"></a>返回值  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geography   
  
CLR 返回类型：**SqlGeography**  
  
## <a name="remarks"></a>Remarks  
此方法更改 GeometryCollection  中所有 Polygons  的环方向，但不删除或更改给定集合中的任何 Points  或 LineStrings  。  
  
如果将 GeometryCollection  传递给此方法，则会重新调整集合中的每个实例，但不会重新调整整个集合。  
  
## <a name="examples"></a>示例  
  
```  
DECLARE @R GEOGRAPHY = GEOGRAPHY::Parse('Polygon((-10 -10, -10 10, 10 10, 10 -10, -10 -10))');  
SELECT @R.ReorientObject().STAsText();  
--Result: POLYGON ((10 10, -10 10, -10 -10, 10 -10, 10 10))  
```  
  
## <a name="see-also"></a>另请参阅  
[地理实例上的扩展方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
