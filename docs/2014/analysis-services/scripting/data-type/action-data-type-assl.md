---
title: Action 数据类型 (ASSL) |Microsoft Docs
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 77b4ef3f8507d67090b78c00807278d0d7dc6348
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37154968"
---
# <a name="action-data-type-assl"></a>Action 数据类型 (ASSL)
  定义表示中的操作的抽象的基元数据类型[多维数据集](../objects/cube-element-assl.md)元素或[角度来看](../objects/perspective-element-assl.md)元素。  
  
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
|子元素|[批注](../collections/annotations-element-assl.md)，[应用程序](../properties/application-element-assl.md)，[标题](../properties/caption-element-assl.md)， [CaptionIsMdx](../properties/captionismdx-element-assl.md)，[条件](../properties/condition-element-assl.md)，[说明](../properties/description-element-assl.md)， [ID](../properties/id-element-assl.md)，[调用](../properties/invocation-element-assl.md)，[名称](../properties/name-element-assl.md)，[目标](../properties/target-element-assl.md)， [TargetType](../properties/targettype-element-assl.md)，[翻译](../collections/translations-element-assl.md)，[类型](../properties/type-element-action-assl.md)|  
|派生元素|[DrillThroughAction](action-data-type-assl.md)， [ReportAction](reportaction-data-type-assl.md)， [StandardAction](standardaction-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 有关操作的详细信息，请参阅[操作（Analysis Services - 多维数据）](../../multidimensional-models/actions-analysis-services-multidimensional-data.md)。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>请参阅  
 [多维数据集元素&#40;ASSL&#41;](../objects/cube-element-assl.md)   
 [Perspective 元素&#40;ASSL&#41;](../objects/perspective-element-assl.md)   
 [PerspectiveAction 数据类型&#40;ASSL&#41;](perspectiveaction-data-type-assl.md)   
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
