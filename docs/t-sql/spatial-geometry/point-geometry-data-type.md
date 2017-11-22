---
title: "点 (geometry 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Point
- Point_TSQL
dev_langs: TSQL
helpviewer_keywords: Point (geometry Data Type)
ms.assetid: 7a2e593a-4d4c-4214-b0c5-02d1ac46bc66
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d9a12d28b917ab2f6211bef0f07a62301a100bfe
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="point-geometry-data-type"></a>Point（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

构造**几何图形**实例表示**点**从其 X 和 Y 值且 SRID 的实例。
  
## <a name="syntax"></a>语法  
  
```  
  
Point ( X, Y, SRID )  
```  
  
## <a name="arguments"></a>参数  
 *X*  
 是**float**表达式表示的 X 坐标**点**正在生成。  
  
 *Y*  
 是**float**表达式表示的 Y 坐标**点**正在生成。  
  
 *SRID*  
 是**int**表达式表示空间引用标识符 (SRID) 的**几何图形**您希望返回的实例。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**几何图形**  
  
 CLR 返回类型： **SqlGeometry**  
  
## <a name="remarks"></a>注释  
  
## <a name="examples"></a>示例  
 下面的示例使用 `Point()` 创建 `geometry` 实例。  
  
```  
DECLARE @g geometry;   
SET @g = geometry::Point(1, 10, 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [扩展静态几何图形方法](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

