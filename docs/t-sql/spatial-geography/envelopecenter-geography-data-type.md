---
title: EnvelopeCenter（geography 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f72f27b98f97cfe15d853a961d194cfb7d1f25ad
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="envelopecenter-geography-data-type-"></a>EnvelopeCenter（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回一个点，该点可用作 geography 实例的边框圆的圆心。  
  
 为了确定该边框圆，实例中的每个点都描述为从地球中心到地球表面上该点的一个向量。 边框圆的中心点是通过平均所有向量计算出来的。 对于闭合的圆圈，无论是在 polygon 实例中还是在 linestring 实例中，第一个点和最后一个点都只使用一次。  
  
 这种 geography 数据类型方法支持大于半球的 FullGlobe 实例或空间实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
EnvelopeCenter( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geography  
  
 CLR 返回类型：SqlGeography  
  
## <a name="remarks"></a>Remarks  
 此方法返回一个点。 在与 `EnvelopeAngle()` 一起使用时，`EnvelopeCenter()` 返回 geography 实例的一个边框圆。  
  
> [!NOTE]  
>  `EnvelopeCenter()` 返回 geography 实例的一个边框圆，但是不保证结果能够产生最小的边框圆。 与此相反，geometry 数据类型方法 `STEnvelope()` 在应用于 geometry 实例时可以保证返回最小的边框圆。  
  
 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和更高版本中，将表示此实例信封的圆的中心作为“点”返回。 对于所有根据 `EnvelopeAngle()` = 180 定义的大型对象，`EnvelopeCenter()` 将返回 (90,0)。  
  
 此方法不精确。  
  
## <a name="examples"></a>示例  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';  
SELECT @g.EnvelopeCenter().ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [Geography 实例上的扩展方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [EnvelopeAngle（geography 数据类型）](../../t-sql/spatial-geography/envelopeangle-geography-data-type.md)  
  
  
