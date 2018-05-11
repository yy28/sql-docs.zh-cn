---
title: 值元素 （参数） (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 904d34b8950246b8ba83b15bb9182d6f04216f30
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="value-element-parameter-xmla"></a>Value 元素 (Parameter) (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含由参数的值[参数](../../../analysis-services/xmla/xml-elements-properties/parameter-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Parameter>  
   ...  
   <Value>...</Value>  
   ...  
</Parameter>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Any|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[参数](../../../analysis-services/xmla/xml-elements-properties/parameter-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **值**元素可以存储任何简单 XML 类型，以及 XML Analysis (XMLA)**行集**数据类型，使用中的 XMLA 命令参数[执行](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
