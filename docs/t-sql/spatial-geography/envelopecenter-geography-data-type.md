---
title: "EnvelopeCenter (geography 数据类型) |Microsoft 文档"
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
- EnvelopeCenter
- EnvelopeCenter_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeCenter method
ms.assetid: dee9d807-faad-45b8-b3f3-7e8aa7d07147
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0638e8793c75ad78aafa12bec1d1f8a3061022c2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="envelopecenter-geography-data-type-"></a>EnvelopeCenter（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回可用作有关边界圆的中心点**geography**实例。  
  
 为了确定该边框圆，实例中的每个点都描述为从地球中心到地球表面上该点的一个向量。 边框圆的中心点是通过平均所有向量计算出来的。 封闭环，在**多边形**实例或**linestring**实例，第一个和最后一个点仅使用一次。  
  
 这**geography**数据类型方法支持**FullGlobe**实例或大于半球的空间实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
EnvelopeCenter( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**地理位置**  
  
 CLR 返回类型： **SqlGeography**  
  
## <a name="remarks"></a>注释  
 此方法返回**点**。 如果用于`EnvelopeAngle()`，`EnvelopeCenter()`返回边界圆的**geography**实例。  
  
> [!NOTE]  
>  `EnvelopeCenter()`返回有关边界圆圈**geography**实例，但结果不能保证生成的最小的边界圆圈。 与此相反，**几何图形**数据类型方法`STEnvelope()`保证时应用于返回的最小值边界框**几何图形**实例。  
  
 在[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和更高版本，返回表示此实例作为信封圆的中心**点**。 对于所有根据 `EnvelopeAngle()` = 180 定义的大型对象，`EnvelopeCenter()` 将返回 (90,0)。  
  
 此方法不精确。  
  
## <a name="examples"></a>示例  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';  
SELECT @g.EnvelopeCenter().ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [地域实例的扩展的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [EnvelopeAngle &#40; geography 数据类型 &#41;](../../t-sql/spatial-geography/envelopeangle-geography-data-type.md)  
  
  

