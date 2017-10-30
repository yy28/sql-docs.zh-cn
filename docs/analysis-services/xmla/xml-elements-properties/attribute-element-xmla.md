---
title: "属性元素 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Attribute Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Attribute
- microsoft.xml.analysis.attribute
- urn:schemas-microsoft-com:xml-analysis#Attribute
helpviewer_keywords:
- Attribute element
ms.assetid: 0df9cf44-dc5f-4234-8a5a-daac8aabc0d6
caps.latest.revision: 17
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2ac9985902b6e91fd2f69b2cc7b7ea3eec6cc79e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="attribute-element-xmla"></a>Attribute 元素 (XMLA)
  定义或筛选器中的属性的成员父级[插入](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)，[更新](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)，或[删除](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)命令执行。  
  
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
|[删除](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)，[其中](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md)|[AttributeName](../../../analysis-services/xmla/xml-elements-properties/attributename-element-xmla.md)，[密钥](../../../analysis-services/xmla/xml-elements-properties/keys-element-xmla.md)|  
|[插入](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)，[更新](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|[AttributeName](../../../analysis-services/xmla/xml-elements-properties/attributename-element-xmla.md)， [CustomRollup](../../../analysis-services/xmla/xml-elements-properties/customrollup-element-xmla.md)， [CustomRollupProperties](../../../analysis-services/xmla/xml-elements-properties/customrollupproperties-element-xmla.md)，[密钥](../../../analysis-services/xmla/xml-elements-properties/keys-element-xmla.md)，[名称](../../../analysis-services/xmla/xml-elements-properties/name-element-xmla.md)， [SkippedLevels](../../../analysis-services/xmla/xml-elements-properties/skippedlevels-element-xmla.md)，[翻译](../../../analysis-services/xmla/xml-elements-properties/translations-element-xmla.md)， [UnaryOperator](../../../analysis-services/xmla/xml-elements-properties/unaryoperator-element-xmla.md)|  
  
## <a name="remarks"></a>注释  
 **Attribute** 元素定义分别由 **Insert**、 **Update**或 **Drop** 命令来插入、更新或删除的属性成员。 这些命令可以仅对一个属性成员运行一次[属性](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md)集合**插入**，**更新**，和**删除**命令只能包含一个**属性**元素。 但是， **Attributes** 和 **Where** 命令的 **Drop** 元素的 **Update** 集合可以包含多个 **Attribute** 元素，因此您可以在启用写操作的维度中筛选要删除或更新的属性。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)   
 [写入的维度](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  

