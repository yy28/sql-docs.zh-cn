---
title: 操作数据类型 (ASSL) |Microsoft 文档
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
- Action Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Action data type
ms.assetid: 8c4d2ff7-17e1-4e74-bec7-637e0b191acf
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 18047bc8a33c92e6bcd434e1a472917c269272e5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124648"
---
# <a name="action-data-type-assl"></a>Action 数据类型 (ASSL)
  定义表示中的操作的抽象基元数据类型[多维数据集](../objects/cube-element-assl.md)元素或[透视](../objects/perspective-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Action>  
   <Name>...</Name>  
   <ID>...</ID>  
   <Caption>...</Caption>  
      <CaptionIsMdx>...</CaptionIsMdx>  
      <Translations>...</Translations>  
   <TargetType>...</TargetType>  
   <Target>...</Target>  
   <Condition>...</Condition>  
   <Type>...</Type>  
   <Invocation>...</Invocation>  
   <Application>...</Application>  
      <Description>...</Description>  
      <Annotations>...</Annotations>  
</Action>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|InclusionThresholdSetting|  
|派生数据类型|[DrillThroughAction](action-data-type-assl.md)， [ReportAction](reportaction-data-type-assl.md)， [StandardAction](standardaction-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[操作](../collections/actions-element-assl.md)|  
|子元素|[Annotations](../collections/annotations-element-assl.md), [Application](../properties/application-element-assl.md), [Caption](../properties/caption-element-assl.md), [CaptionIsMdx](../properties/captionismdx-element-assl.md), [Condition](../properties/condition-element-assl.md), [Description](../properties/description-element-assl.md), [ID](../properties/id-element-assl.md), [Invocation](../properties/invocation-element-assl.md), [Name](../properties/name-element-assl.md), [Target](../properties/target-element-assl.md), [TargetType](../properties/targettype-element-assl.md), [Translations](../collections/translations-element-assl.md), [Type](../properties/type-element-action-assl.md)|  
|派生元素|[DrillThroughAction](action-data-type-assl.md)， [ReportAction](reportaction-data-type-assl.md)， [StandardAction](standardaction-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 有关操作的详细信息，请参阅[操作（Analysis Services - 多维数据）](../../multidimensional-models/actions-analysis-services-multidimensional-data.md)。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>请参阅  
 [多维数据集元素&#40;ASSL&#41;](../objects/cube-element-assl.md)   
 [透视元素&#40;ASSL&#41;](../objects/perspective-element-assl.md)   
 [PerspectiveAction 数据类型&#40;ASSL&#41;](perspectiveaction-data-type-assl.md)   
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  