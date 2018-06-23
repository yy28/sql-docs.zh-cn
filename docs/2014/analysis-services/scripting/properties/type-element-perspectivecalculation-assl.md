---
title: 类型元素 (PerspectiveCalculation) (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Type Element (PerspectiveCalculation)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: d7b87aea-3265-4f3c-a7ee-4f3e90f9a0b7
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 242d4d779da87c155371047fd2bb21128da51abf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024419"
---
# <a name="type-element-perspectivecalculation-assl"></a>Type 元素 (PerspectiveCalculation) (ASSL)
  指示的一种[PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<PerspectiveCalculation>  
   ...  
   <Type>...</Type>  
   ...  
</PerspectiveCalculation>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*成员*|“计算成员”|  
|*设置*|命名集|  
  
 对应于的允许值为枚举`Type`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.PerspectiveCalculationType>。  
  
 对应于的父元素`Type`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.PerspectiveCalculation>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  