---
title: Point（geography 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 10/10/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: b122ee434979bb25c9a1fb0fa1c67887f5cb3eba
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826593"
---
# <a name="point-geography-data-type"></a>Point（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

根据 Point 实例的纬度值和经度值以及空间引用 ID (SRID) 构造一个表示该实例的 geography 实例   。
  
## <a name="syntax"></a>语法  
  
```  
  
Point ( Lat, Long, SRID )  
```  
  
## <a name="arguments"></a>参数  
 *Lat*  
 一个 float 表达式，表示正在生成的 Point 的 Y 坐标   。  
  
 *Long*  
 一个 float 表达式，表示正在生成的 Point 的 X 坐标   。 有关有效的纬度值和经度值的详细信息，请参阅 [Point](../../relational-databases/spatial/point.md)。  
  
 SRID   
 一个 int 表达式，表示希望返回的 geography 实例的[空间引用标识符](https://docs.microsoft.com/sql/relational-databases/spatial/spatial-reference-identifiers-srids)   。  
  
> [!NOTE]  
>  Point（地理数据类型）方法的参数具有与 WKT 相反的坐标。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geography   
  
 CLR 返回类型：**SqlGeography**  
  
## <a name="examples"></a>示例  
 下面的示例使用 `Point()` 创建 `geography` 实例。  
  
```  
DECLARE @g geography;   
SET @g = geography::Point(47.65100, -122.34900, 4326)  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [扩展静态地理方法](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
