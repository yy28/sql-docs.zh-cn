---
title: 级别元素 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Level Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- LEVEL
helpviewer_keywords:
- Level element
ms.assetid: 66ee2c16-d6b8-4dd3-879f-1f2b6923bc43
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 028375d525ec0197aec24a9005fd3f5f0e8fe769
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129979"
---
# <a name="level-element-assl"></a>Level 元素 (ASSL)
  定义中的级别[层次结构](hierarchy-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Levels>  
      <Level>  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</Description>  
      <SourceAttributeID>...</SourceAttributeID>  
      <HideMemberIf>...</HideMemberIf>  
      <Translations>...</Translations>  
      <Annotations>...</Annotations>  
   </Level>  
</Levels>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Levels](../collections/levels-element-assl.md)|  
|子元素|[批注](../collections/annotations-element-assl.md)，[说明](../properties/description-element-assl.md)， [HideMemberIf](../properties/hidememberif-element-assl.md)， [ID](../properties/id-element-assl.md)，[名称](../properties/name-element-assl.md)， [SourceAttributeID](../properties/attributeid-element-assl.md)，[翻译](../collections/translations-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 此数据类型在任何部署模式下均没有限制（1-多维和数据挖掘、2-SharePoint 和 3 表格）。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Level>。  
  
## <a name="see-also"></a>请参阅  
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  