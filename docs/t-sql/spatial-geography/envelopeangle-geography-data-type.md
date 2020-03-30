---
title: EnvelopeAngle（geography 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EnvelopeAngle
- EnvelopeAngle_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeAngle method
ms.assetid: 14a7ba15-168c-4b08-ba3d-951d73092ac7
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: e3289956dd79c852eef6534ad1f72623ad4dcaa6
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "68066466"
---
# <a name="envelopeangle-geography-data-type"></a>EnvelopeAngle（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回由 `EnvelopeCenter()` 返回的点与 geography 实例中的点之间的最大角度（以度数为单位）  。  
  
 这种 geography 数据类型方法支持大于半球的 FullGlobe 实例或空间实例   。  
  
## <a name="syntax"></a>语法  
  
```  
  
EnvelopeAngle( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：float   
  
 CLR 返回类型：SqlDouble   
  
## <a name="remarks"></a>备注  
 此方法返回 geography 实例中的点（以度数为单位）  。 在与 EnvelopeCenter() 一起使用时，`EnvelopeAngle()` 返回 geography 实例的一个边框圆  。  
  
 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中，此方法已扩展到 FullGlobe 实例  。  
  
 已删除应用于 `EnvelopeAngle()` 中的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 的半球限制。 但是，对于角度大于 90 度的实例将返回 180 度。 对于跨越多个半球的 geography 实例而言，`EnvelopeAngle()` 并不精确  。  
  
## <a name="examples"></a>示例  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';   
SELECT @g.EnvelopeAngle();  
```  
  
## <a name="see-also"></a>另请参阅  
 [Geography 实例上的扩展方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [EnvelopeCenter（geography 数据类型）](../../t-sql/spatial-geography/envelopecenter-geography-data-type.md)  
  
  
