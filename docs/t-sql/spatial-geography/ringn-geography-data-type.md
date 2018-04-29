---
title: RingN（geography 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- RingN
- RingN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- RingN method
ms.assetid: 30f47275-2727-4d22-bbec-c0c54bcb3ac2
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e55b7990948e84d9a4cb43fe242b8304f3e9cb92
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="ringn-geography-data-type"></a>RingN（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回 geography 实例的指定环：`1 ≤ n ≤ NumRings()`。  
  
## <a name="syntax"></a>语法  
  
```  
  
.RingN (expression )  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 一个 int 表达式，其值介于 1 与 polygon 实例中的环数之间。  
  
## <a name="return-value"></a>返回值  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geography  
  
 CLR 返回类型：SqlGeography  
  
## <a name="remarks"></a>Remarks  
 如果环索引 n 的值小于 1，此方法引发 ArgumentOutOfRangeException。 该环索引的值必须大于或等于 1，而且应当小于或等于 `NumRings()` 返回的数字。  
  
## <a name="examples"></a>示例  
 下面的示例创建一个具有两个环的 `Polygon` 实例并返回第二个环。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653), (-122.357 47.654, -122.357 47.657, -122.349 47.657, -122.349 47.650, -122.357 47.654))', 4326);  
SELECT @g.RingN(2).ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [Geography 实例上的扩展方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [NumRings（geography 数据类型）](../../t-sql/spatial-geography/numrings-geography-data-type.md)  
  
  
