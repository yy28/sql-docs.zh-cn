---
title: IsKey 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- IsKey Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- IsKey
helpviewer_keywords:
- IsKey element
ms.assetid: 523b26c8-5cce-415d-a360-9a0d8724b872
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 525d5de1fb6935c2056dc026b57229535e7557cb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48199007"
---
# <a name="iskey-element-assl"></a>IsKey 元素 (ASSL)
  指示列是否提供中的事例键[MiningStructure](../objects/miningstructure-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ScalarMiningStructureColumn>  
   ...  
   <IsKey>...</IsKey>  
   ...  
</ScalarMiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 可以将一个或多个列指定为每个嵌套表结构级别的键列。  
  
 父级对应的元素`IsKey`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
