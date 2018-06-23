---
title: 属性元素 (XMLA) |Microsoft 文档
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
- Attribute Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Attribute
- microsoft.xml.analysis.attribute
- urn:schemas-microsoft-com:xml-analysis#Attribute
helpviewer_keywords:
- Attribute element
ms.assetid: 0df9cf44-dc5f-4234-8a5a-daac8aabc0d6
caps.latest.revision: 17
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 665626323e435eeed50b73f4d94de4506dba4f19
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017183"
---
# <a name="attribute-element-xmla"></a>Attribute 元素 (XMLA)
  定义或筛选器中的属性的成员父级[插入](../xml-elements-commands/insert-element-xmla.md)，[更新](../xml-elements-commands/update-element-xmla.md)，或[删除](../xml-elements-commands/drop-element-xmla.md)命令执行。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Attributes>  
   ...  
   <Attribute>  
      <AttributeName>...</AttributeName>  
      <Keys>...</Keys>  
      <!-- The following elements are included only for attributes contained in the Attributes element of a parent Insert or Update command -->  
      <Name>...</Name>  
      <Translations>...</Translations>  
      <CustomRollup>...</CustomRollup>  
      <CustomRollupProperties>...</CustomRollupProperties>  
      <UnaryOperator>...</UnaryOperator>  
      <SkippedLevels>...</SkippedLevels>  
   </Attribute>  
   ...  
</Attributes>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[属性](attributes-element-xmla.md)|  
  
 **子元素**  
  
|||  
|-|-|  
|**祖先或父级**|**子元素**|  
|[删除](../xml-elements-commands/drop-element-xmla.md)，[其中](name-element-xmla.md)，[密钥](keys-element-xmla.md)|  
|[插入](../xml-elements-commands/insert-element-xmla.md)，[更新](../xml-elements-commands/update-element-xmla.md)|[AttributeName](name-element-xmla.md)， [CustomRollup](customrollup-element-xmla.md)， [CustomRollupProperties](properties-element-xmla.md)，[密钥](keys-element-xmla.md)，[名称](name-element-xmla.md)， [SkippedLevels](skippedlevels-element-xmla.md)，[翻译](translations-element-xmla.md)， [UnaryOperator](unaryoperator-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `Attribute`元素定义插入、 更新或删除，分别由的属性成员`Insert`， `Update`，或`Drop`命令。 这些命令可以仅对一个属性成员运行一次[属性](attributes-element-xmla.md)集合`Insert`， `Update`，和`Drop`命令只能包含一个`Attribute`元素。 但是，`Attributes` 和 `Where` 命令的 `Drop` 元素的 `Update` 集合可以包含多个 `Attribute` 元素，因此您可以在启用写操作的维度中筛选要删除或更新的属性。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)   
 [启用写操作的维度](../../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  