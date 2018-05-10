---
title: EnvelopeAngle（geography 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9a0198176abd6d9adad12e892be1734227c14d78
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="envelopeangle-geography-data-type"></a>EnvelopeAngle（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回由 `EnvelopeCenter()` 返回的点与 geography 实例中的点之间的最大角度（以度数为单位）。  
  
 这种 geography 数据类型方法支持大于半球的 FullGlobe 实例或空间实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
EnvelopeAngle( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：float  
  
 CLR 返回类型：SqlDouble  
  
## <a name="remarks"></a>Remarks  
 此方法返回 geography 实例中的点（以度数为单位）。 在与 EnvelopeCenter() 一起使用时，`EnvelopeAngle()` 返回 geography 实例的一个边框圆。  
  
 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中，此方法已扩展到 FullGlobe 实例。  
  
 已删除应用于 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中的 `EnvelopeAngle()` 的半球限制。 但是，对于角度大于 90 度的实例将返回 180 度。 对于跨越多个半球的 geography 实例而言，`EnvelopeAngle()` 并不精确。  
  
## <a name="examples"></a>示例  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';   
SELECT @g.EnvelopeAngle();  
```  
  
## <a name="see-also"></a>另请参阅  
 [Geography 实例上的扩展方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [EnvelopeCenter（geography 数据类型）](../../t-sql/spatial-geography/envelopecenter-geography-data-type.md)  
  
  
