---
title: ID 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 48e2b36cd38e1f505ac6d788fdc1f88aec9f19df
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="id-element-xmla"></a>ID 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  标识对其执行父锁[锁](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)或[解锁](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Lock> <!-- or Unlock>  
   ...  
   <ID>...</ID>  
   ...  
</Lock>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[锁定](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)，[解锁](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **ID**元素包含用于标识锁的全局唯一标识符 (GUID)。  
  
## <a name="see-also"></a>另请参阅  
 [Object 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)   
 [模式元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/mode-element-xmla.md)   
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
