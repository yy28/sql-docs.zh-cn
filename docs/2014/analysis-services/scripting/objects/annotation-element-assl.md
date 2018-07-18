---
title: Annotation 元素 (ASSL) |Microsoft Docs
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
- Annotation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Annotation
helpviewer_keywords:
- Annotation element
ms.assetid: 7d75291a-47b4-498a-8ba4-3d093b8513b2
caps.latest.revision: 43
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0453688aab37831c54bad3080a34409b078740bf
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37304497"
---
# <a name="annotation-element-assl"></a>Annotation 元素 (ASSL)
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
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[批注](../collections/annotations-element-assl.md)|  
|子元素|[名称](../properties/name-element-assl.md)，[值](../properties/value-element-assl.md)，[可见性](../properties/visibility-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 `Annotation` 元素为所有对象（不包括仅用于定义复杂数据类型的对象）提供 ASSL 架构的扩展性。 `Value` 元素的 `Annotation` 元素可包含来自非 ASSL 的任何 XML 命名空间的有效 XML，但应遵守以下规则：  
  
-   XML 只能包含元素。  
  
-   每个元素都必须有唯一的名称。 建议 `Name` 元素的 `Annotation` 元素值指向目标命名空间。  
  
 采用这些规则是为了使 `Annotation` 元素的内容能够通过其他接口（如决策支持对象 (DSO)）以一组名称/值对的方式公开。  
  
 在 `Annotation` 元素内，无法保留未用子元素括起来的注释和空格。 此外，所有元素必须可读写；只读元素将被忽略。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Annotation>。  
  
## <a name="see-also"></a>请参阅  
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
