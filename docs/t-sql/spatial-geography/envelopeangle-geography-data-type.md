---
title: "EnvelopeAngle (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- EnvelopeAngle
- EnvelopeAngle_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeAngle method
ms.assetid: 14a7ba15-168c-4b08-ba3d-951d73092ac7
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cd410a6eb07c626c7674febad2a427bbd029f98a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="envelopeangle-geography-data-type"></a>EnvelopeAngle（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回由的点之间的最大的角度`EnvelopeCenter()`和中的点**geography**以度为单位的实例。  
  
 这**geography**数据类型方法支持**FullGlobe**实例或大于半球的空间实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
EnvelopeAngle( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型： **float**  
  
 CLR 返回类型： **SqlDouble**  
  
## <a name="remarks"></a>注释  
 此方法返回中的点**geography**以度为单位的实例。 与 EnvelopeCenter()，一起使用时`EnvelopeAngle()`返回边界圆的**geography**实例。  
  
 在[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，此方法已扩展到**FullGlobe**实例。  
  
 应用于的半球限制`EnvelopeAngle()`中[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]已删除。 但是，对于角度大于 90 度的实例将返回 180 度。 `EnvelopeAngle()`不是精确的**geography**跨越多个半球的实例。  
  
## <a name="examples"></a>示例  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';   
SELECT @g.EnvelopeAngle();  
```  
  
## <a name="see-also"></a>另请参阅  
 [地域实例的扩展的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [EnvelopeCenter &#40; geography 数据类型 &#41;](../../t-sql/spatial-geography/envelopecenter-geography-data-type.md)  
  
  

