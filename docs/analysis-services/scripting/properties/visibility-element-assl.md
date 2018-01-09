---
title: "可见性元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Visibility Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Visibility
helpviewer_keywords: Visibility element
ms.assetid: 59372ebf-af52-4d60-bf9b-bb1644ae9865
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ca271c01c45f87cd9b89740f765e88b81869ceaf
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="visibility-element-assl"></a>Visibility 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]定义的可见性[批注](../../../analysis-services/scripting/objects/annotation-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Annotation>  
   ...  
   <Visibility>...</Visibility>  
   ...  
</Annotation>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*无*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[批注](../../../analysis-services/scripting/objects/annotation-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*SchemaRowset*|该批注在架构行集中是可见的。|  
|*无*|该批注不可见。|  
  
 对应于的允许值为枚举**可见性**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Annotation>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
