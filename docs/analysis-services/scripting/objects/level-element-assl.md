---
title: 级别元素 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a40db1f1d57aadd8acdb029126239ff90b2c4933
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34031458"
---
# <a name="level-element-assl"></a>Level 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义中的级别[层次结构](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)元素。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Levels](../../../analysis-services/scripting/collections/levels-element-assl.md)|  
|子元素|[批注](../../../analysis-services/scripting/collections/annotations-element-assl.md)，[说明](../../../analysis-services/scripting/properties/description-element-assl.md)， [HideMemberIf](../../../analysis-services/scripting/properties/hidememberif-element-assl.md)， [ID](../../../analysis-services/scripting/properties/id-element-assl.md)，[名称](../../../analysis-services/scripting/properties/name-element-assl.md)， [SourceAttributeID](../../../analysis-services/scripting/properties/sourceattributeid-element-assl.md)，[翻译](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 此数据类型在任何部署模式下均没有限制（1-多维和数据挖掘、2-SharePoint 和 3 表格）。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Level>。  
  
## <a name="see-also"></a>另请参阅  
 [对象 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
