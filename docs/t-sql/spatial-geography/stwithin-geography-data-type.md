---
title: "STWithin (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STWithin method (geography)
ms.assetid: 6fc745cc-7976-418a-a89a-c267e64ab3a2
caps.latest.revision: 7
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c0347f3ceb94b52aab11378dbb058dd49b60e7b1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="stwithin-geography-data-type"></a>STWithin（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  如果返回 1 **geography**实例空间是在另一个**geography**实例; 否则，返回 0。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STWithin ( other_geography )  
```  
  
## <a name="arguments"></a>参数  
 *other_geography*  
 是另一种**geography**实例要针对的实例上进行比较`STWithin()`调用。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**位**  
  
 CLR 返回类型： **SqlBoolean**  
  
## <a name="remarks"></a>注释  
 如果此方法将始终返回 null 的空间引用 Id 为 (Srid) **geography**实例不匹配。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `STWithin()` 来测试两个 `geography` 实例，以查看第一个实例是否完全包含在第二个实例中。  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::Parse('POLYGON ((-120.533 46.566, -118.283 46.1, -122.3 47.45, -120.533 46.566))');  
SET @h = geography::Parse('CURVEPOLYGON (COMPOUNDCURVE (CIRCULARSTRING (-122.200928 47.454094, -122.810669 47.00648, -122.942505 46.687131, -121.14624 45.786679, -119.119263 46.183634), (-119.119263 46.183634, -119.273071 47.107523), CIRCULARSTRING (-119.273071 47.107523, -120.640869 47.569114, -122.200928 47.454094)))');  
SELECT @g.STWithin(@h);  
```  
  
  

