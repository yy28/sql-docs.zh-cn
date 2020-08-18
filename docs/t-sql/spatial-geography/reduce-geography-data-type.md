---
description: Reduce（geography 数据类型）
title: Reduce（geography 数据类型）
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Reduce_TSQL
- Reduce
dev_langs:
- TSQL
helpviewer_keywords:
- Reduce method
ms.assetid: c5dfa8c1-6764-41d8-9150-f3cb30633d3e
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: ab2f24276cb3f151adf4e1418fd141180171a633
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88359873"
---
# <a name="reduce-geography-data-type-"></a>Reduce（geography 数据类型）
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  返回给定 geography 实例的近似值，该值通过对实例运行具有给定公差的 Douglas-Peucker 算法来生成  。  
  
 这种 geography 数据类型方法支持大于半球的 FullGlobe 实例或空间实例   。  
  
## <a name="syntax"></a>语法  
  
```  
  
.Reduce ( tolerance )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>参数

|术语|定义|
|----|----------|
|tolerance|类型为 float 的值  。 tolerance 是输入到 Douglas-Peucker 算法的公差  。 tolerance 必须为正数  。|  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geography  
  
 CLR 返回类型：SqlGeography  
  
## <a name="remarks"></a>备注  
 对于集合类型，此算法单独作用于包含在该实例中的每个 tolerance  。 此算法不修改 Point 实例  。  
  
 此方法将尝试保留 LineString 实例的终结，但是可能为了保留有效结果而无法实现此目的  。  
  
 如果使用负值调用 `Reduce()`，此方法将产生 ArgumentException  。 在 `Reduce()` 中使用的公差必须为正数。  
  
 通过删除除起点和终点之外的所有点，Douglas-Peucker 算法可用于 geography 实例中的每个曲线或圆环  。 然后，它再将已删除的点添加回去，从偏离中心最远的点开始，直到所有点与结果的距离都在 tolerance 范围之内  。 然后，如果必要，使结果变得有效，因为必须保证有一个有效的结果。  
  
 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中，此方法已扩展到 FullGlobe 实例  。  
  
 此方法不精确。  
  
## <a name="examples"></a>示例  
 以下示例创建一个 `LineString` 实例，并使用 `Reduce()` 简化该实例。  
  
```  
DECLARE @g geography = 'LineString(120 45, 120.1 45.1, 199.9 45.2, 120 46)'  
SELECT @g.Reduce(10000).ToString()  
```  
  
## <a name="see-also"></a>另请参阅  
 [地理实例上的扩展方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
