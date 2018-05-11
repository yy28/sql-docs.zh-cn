---
title: WritebackTableCreation 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 54969f1710a4abcd079fc3318f1d7c99abc3ce80
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="writebacktablecreation-element-xmla"></a>WritebackTableCreation 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  确定是否将写回表创建期间[过程](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)操作。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Process>  
...  
   <WritebackTableCreation>...</WritebackTableCreation>  
...  
</Process>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[处理](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 Analysis Services 实例上可用的对象的处理选项的详细信息，请参阅[处理多维模型&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。  
  
 值**WritebackTableCreation**元素被限制为下表中列出的字符串之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|*创建*|如果不存在写回表，则创建一个新表。 如果写回表已存在，则会出错。|  
|*CreateAlways*|创建一个新的写回表，并覆盖任何现有的写回表。|  
|*UseExisting*|如果已存在，请使用现有写回表。 如果写回表不存在，则会出错。|  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
