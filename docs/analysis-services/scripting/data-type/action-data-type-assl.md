---
title: 操作数据类型 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b717929c61852836527f00809528ccb8d2b26d8d
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="action-data-type-assl"></a>Action 数据类型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义表示中的操作的抽象基元数据类型[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)元素或[透视](../../../analysis-services/scripting/objects/perspective-element-assl.md)元素。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|基本数据类型|无|  
|派生数据类型|[DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)、 [ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)、 [StandardAction](../../../analysis-services/scripting/data-type/standardaction-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[操作](../../../analysis-services/scripting/collections/actions-element-assl.md)|  
|子元素|[批注](../../../analysis-services/scripting/collections/annotations-element-assl.md)，[应用程序](../../../analysis-services/scripting/properties/application-element-assl.md)，[标题](../../../analysis-services/scripting/properties/caption-element-assl.md)， [CaptionIsMdx](../../../analysis-services/scripting/properties/captionismdx-element-assl.md)，[条件](../../../analysis-services/scripting/properties/condition-element-assl.md)，[说明](../../../analysis-services/scripting/properties/description-element-assl.md)， [ID](../../../analysis-services/scripting/properties/id-element-assl.md)，[调用](../../../analysis-services/scripting/properties/invocation-element-assl.md)，[名称](../../../analysis-services/scripting/properties/name-element-assl.md)，[目标](../../../analysis-services/scripting/properties/target-element-assl.md)， [TargetType](../../../analysis-services/scripting/properties/targettype-element-assl.md)，[翻译](../../../analysis-services/scripting/collections/translations-element-assl.md)，[类型](../../../analysis-services/scripting/properties/type-element-action-assl.md)|  
|派生元素|[DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)、 [ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)、 [StandardAction](../../../analysis-services/scripting/data-type/standardaction-data-type-assl.md)|  
  
## <a name="remarks"></a>注释  
 有关操作的详细信息，请参阅[操作（Analysis Services - 多维数据）](../../../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md)。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>另请参阅  
 [多维数据集元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [透视元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/perspective-element-assl.md)   
 [PerspectiveAction 数据类型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/perspectiveaction-data-type-assl.md)   
 [Analysis Services 脚本语言 XML 数据类型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
