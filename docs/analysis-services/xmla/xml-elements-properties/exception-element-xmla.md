---
title: 异常元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e5b9847f1328fb0f0c7b6c1503708ca0b75b585c
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="exception-element-xmla"></a>Exception 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  表示从返回了异常[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)或[执行](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法调用。  
  
 **命名空间** `http://schemas.microsoft.com/analysisservices/2003/exception`  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<root>  
   ...  
   <Exception />  
   ...  
</root>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 如果在执行期间发生错误**发现**中的方法调用或单个 XMLA 命令**执行**完成之后，可以防止方法或命令的方法调用**根**为该方法或命令元素包含**异常**元素和**消息**元素。 **异常**元素指示发生了错误的阻止方法或命令成功执行，与**消息**元素包含的错误或警告消息的列表与错误相关。  
  
## <a name="see-also"></a>另请参阅  
 [消息元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/messages-element-xmla.md)   
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
