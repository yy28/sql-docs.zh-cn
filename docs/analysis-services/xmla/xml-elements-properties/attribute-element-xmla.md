---
title: 属性元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d96ab99730997f56460ff6ce9c3cf27ddd1f6a41
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="attribute-element-xmla"></a>Attribute 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  定义或筛选执行父 [Insert](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)、 [Update](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)或 [Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md) 命令的属性成员。  
  
## <a name="syntax"></a>語法  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[属性](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md)|  
|子元素|请参阅下表。|  
  
|祖先或父级|子元素|  
|------------------------|-------------------|  
|[Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)、 [Where](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md)|[AttributeName](../../../analysis-services/xmla/xml-elements-properties/attributename-element-xmla.md)、 [Keys](../../../analysis-services/xmla/xml-elements-properties/keys-element-xmla.md)|  
|[Insert](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)、 [Update](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|[AttributeName](../../../analysis-services/xmla/xml-elements-properties/attributename-element-xmla.md)、 [CustomRollup](../../../analysis-services/xmla/xml-elements-properties/customrollup-element-xmla.md)、 [CustomRollupProperties](../../../analysis-services/xmla/xml-elements-properties/customrollupproperties-element-xmla.md)、 [Keys](../../../analysis-services/xmla/xml-elements-properties/keys-element-xmla.md)、 [Name](../../../analysis-services/xmla/xml-elements-properties/name-element-xmla.md)、 [SkippedLevels](../../../analysis-services/xmla/xml-elements-properties/skippedlevels-element-xmla.md)、 [Translations](../../../analysis-services/xmla/xml-elements-properties/translations-element-xmla.md)、 [UnaryOperator](../../../analysis-services/xmla/xml-elements-properties/unaryoperator-element-xmla.md)|  
  
## <a name="remarks"></a>注释  
 **Attribute** 元素定义分别由 **Insert**、 **Update**或 **Drop** 命令来插入、更新或删除的属性成员。 这些命令可以仅对一个属性成员运行一次[属性](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md)集合**插入**，**更新**，和**删除**命令只能包含一个**属性**元素。 但是， **Attributes** 和 **Where** 命令的 **Drop** 元素的 **Update** 集合可以包含多个 **Attribute** 元素，因此您可以在启用写操作的维度中筛选要删除或更新的属性。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)   
 [写入的维度](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
