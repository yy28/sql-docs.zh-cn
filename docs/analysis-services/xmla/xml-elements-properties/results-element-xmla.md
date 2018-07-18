---
title: 结果元素 (XMLA) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7fc64d6b31f1b05d8bf5b4d1c80d75dff0583e86
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37968659"
---
# <a name="results-element-xmla"></a>results 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含一系列[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)返回的元素[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法使用[批处理](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)命令。  
  
 **Namespace** `http://schemas.microsoft.com/analysisservices/2003/xmla-multipleresults`  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<return>  
   <results>  
      <root>...</root>  
   </results>  
</return>  
```  
  
## <a name="element-characteristics"></a>元素的特性  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[返回](../../../analysis-services/xmla/xml-elements-properties/return-element-xmla.md)|  
|子元素|[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 如果**批处理**由执行命令**Execute**方法，**返回**元素包含一个**结果**元素而不是单一**根**元素。 内容**结果**元素取决于用于运行设置**批处理**命令。  
  
 对于非事务性**批处理**命令，**结果**元素包含一个**根**执行的每个命令的元素**批处理**命令是否成功或未成功完成该命令。 对于事务性**批处理**命令，**结果**元素只包含一个**根**元素，它包含有关在中失败的命令**批处理**命令。  
  
## <a name="see-also"></a>另请参阅
 [属性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
