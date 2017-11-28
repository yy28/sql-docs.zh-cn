---
title: "STPointN (geometry 数据类型) |Microsoft 文档"
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
- STPointN_TSQL
- STPointN (geometry Data Type)
dev_langs: TSQL
helpviewer_keywords: STPointN (geometry Data Type)
ms.assetid: 8f0bb3b7-5cd9-42c2-b9f8-f04628653bd0
caps.latest.revision: "22"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6e35a1bc7b4466a688274a825de3a34081149207
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="stpointn-geometry-data-type"></a>STPointN（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回中的指定的点**几何图形**实例。
  
## <a name="syntax"></a>语法  
  
```  
  
.STPointN ( expression )  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 是**int**介于 1 和中的点的数目的表达式**几何图形**实例。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**几何图形**  
  
 CLR 返回类型： **SqlGeometry**  
  
 打开地理空间联盟 (OGC) 类型：**点**  
  
## <a name="remarks"></a>注释  
 如果**几何图形**实例是用户创建，`STPointN()`返回由指定的点*表达式*由在其中它们最初已输入的顺序排序的点。  
  
 如果**几何图形**构造实例时由系统`STPointN()`返回由指定的点*表达式*通过相同顺序排序的所有点，它们将为输出： 先几何图形，然后按由环内的几何图形 （如果适用），然后在环内的点。 此顺序是确定的。  
  
 如果使用等于或大于 1 的值调用此方法，则它将引发**ArgumentOutOfRangeException**。  
  
 如果使用大于实例中点数的值来调用此方法，则返回 Null。  
  
## <a name="examples"></a>示例  
 下面的示例创建 `LineString` 实例，并使用 `STPointN()` 检索实例说明中的第二个点。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STPointN(2).ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

