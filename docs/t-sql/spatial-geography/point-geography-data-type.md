---
title: "点 (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 07/30/2017
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
f1_keywords:
- Point
- Point_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Point method
- Point (geography Data Type)
ms.assetid: 0dc6f422-7aae-4016-b7f4-3289fa8f989c
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7cefb6e199bbd4617b1fc2f6f71d9bb3997445dc
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="point-geography-data-type"></a>Point（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

构造**geography**实例表示**点**从其纬度和经度值和空间引用标识符 (SRID) 的实例。
  
## <a name="syntax"></a>语法  
  
```  
  
Point ( Lat, Long, SRID )  
```  
  
## <a name="arguments"></a>参数  
 *Lat*  
 是**float**表达式表示的 x 坐标**点**正在生成。  
  
 *长*  
 是**float**表达式表示的 y 坐标**点**正在生成。 有关有效的纬度和经度值的详细信息，请参阅[点](../../relational-databases/spatial/point.md)。  
  
 *SRID*  
 是**int**表达式表示的 SRID **geography**您希望返回的实例。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**地理位置**  
  
 CLR 返回类型： **SqlGeography**  
  
> [!NOTE]  
>  Point（地理数据类型）方法的参数具有与 WKT 相反的坐标。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `Point()` 创建 `geography` 实例。  
  
```  
DECLARE @g geography;   
SET @g = geography::Point(47.65100, -122.34900, 4326)  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [扩展静态 Geography 方法](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  

