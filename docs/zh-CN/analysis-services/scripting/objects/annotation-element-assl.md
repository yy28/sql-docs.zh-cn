---
title: 批注元素 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Annotation Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Annotation
helpviewer_keywords:
- Annotation element
ms.assetid: 7d75291a-47b4-498a-8ba4-3d093b8513b2
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 91290ec4f4b0ba29fb8b14d5cb6602ba4db7ed36
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="annotation-element-assl"></a>Annotation 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含用于扩展 Analysis Services 脚本语言 (ASSL) 架构的元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Annotations>  
   <Annotation>  
      <Name>...</Name>  
      <Visibility>...</Visibility>  
      <Value>...</Value>  
   </Annotation>  
</Annotations >  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[批注](../../../analysis-services/scripting/collections/annotations-element-assl.md)|  
|子元素|[名称](../../../analysis-services/scripting/properties/name-element-assl.md)，[值](../../../analysis-services/scripting/properties/value-element-assl.md)，[可见性](../../../analysis-services/scripting/properties/visibility-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 **批注**元素，还提供扩展性之外使用只是为了定义复杂数据类型的所有对象的 ASSL 架构。 **值**元素**批注**元素可以包含有效的 XML 与任何 XML 命名空间以外 ASSL，需遵循以下规则：  
  
-   XML 只能包含元素。  
  
-   每个元素都必须有唯一的名称。 建议的值**名称**元素**批注**元素引用的目标命名空间。  
  
 这些规则来允许的内容而**批注**元素将公开为一组的名称/值对通过其他接口，如决策支持对象 (DSO)。  
  
 注释和内的空白**批注**无法保留不包含在子元素的元素。 此外，所有元素必须可读写；只读元素将被忽略。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Annotation>。  
  
## <a name="see-also"></a>另请参阅  
 [对象 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
