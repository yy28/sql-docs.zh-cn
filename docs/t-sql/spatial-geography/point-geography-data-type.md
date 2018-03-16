---
title: "Point（geography 数据类型）| Microsoft Docs"
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f37072d64159d5d8bfb1d44a64dd017adf0fceed
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="point-geography-data-type"></a>Point（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

根据 Point 实例的纬度值和经度值以及空间引用 ID (SRID) 构造一个表示该实例的 geography 实例。
  
## <a name="syntax"></a>语法  
  
```  
  
Point ( Lat, Long, SRID )  
```  
  
## <a name="arguments"></a>参数  
 Lat  
 一个 float 表达式，表示正在生成的 Point 的 X 坐标。  
  
 Long  
 一个 float 表达式，表示正在生成的 Point 的 Y 坐标。 有关有效的纬度值和经度值的详细信息，请参阅 [Point](../../relational-databases/spatial/point.md)。  
  
 SRID  
 一个 int 表达式，表示希望返回的 geography 实例的 SRID。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geography  
  
 CLR 返回类型：SqlGeography  
  
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
 [扩展静态地理方法](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
