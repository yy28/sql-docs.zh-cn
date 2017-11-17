---
title: "STPointN (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- STPointN_TSQL
- STPointN (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPointN method
ms.assetid: 47670feb-b9e0-4b4b-af83-b9bba7da66ac
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 15a196cf9ac1c5f560a2eeee3d0262829f88480b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="stpointn-geography-data-type"></a>STPointN（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回在指定的点**geography**实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STPointN ( expression )  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 是**int**介于 1 和中的点的数目的表达式**geography**实例。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**地理位置**  
  
 CLR 返回类型： **SqlGeography**  
  
 打开地理空间联盟 (OGC) 类型：**点**  
  
## <a name="remarks"></a>注释  
 如果**geography**实例为用户创建，则 STPointN() 返回由指定的点*表达式*由在其中它们最初已输入的顺序排序的点。  
  
 如果**geography**系统构造实例，则 STPointN() 返回由指定的点*表达式*通过相同顺序排序的所有点，它们将为输出： 先按**geography**实例，然后按实例 （如果适用） 内环和内环的点。 此顺序是确定的。  
  
 如果使用等于或大于 1 的值调用此方法，则它将引发**ArgumentOutOfRangeException**。  
  
 如果使用大于实例中点数的值来调用此方法，则返回 Null。  
  
## <a name="examples"></a>示例  
 下面的示例创建 `LineString` 实例，并使用 `STPointN()` 检索实例说明中的第二个点。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STPointN(2).ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [地域实例上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

