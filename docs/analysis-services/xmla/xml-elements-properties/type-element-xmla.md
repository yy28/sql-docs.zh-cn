---
title: 类型元素 (XMLA) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Type Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.type
- http://schemas.microsoft.com/analysisservices/2003/engine#Type
- urn:schemas-microsoft-com:xml-analysis#Type
helpviewer_keywords:
- Type element
ms.assetid: 5d898123-a635-402a-be86-8249d7304fa4
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a6480eec04a32ee76ee4cd83f8df096b2d18e879
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="type-element-xmla"></a>Type 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  确定要执行的处理的类型[过程](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)元素。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Process>  
...  
   <Type>...</Type>  
...  
</Process>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[处理](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 有关处理提供给对象的实例上的选项的详细信息[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，请参阅[处理多维模型&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。  
  
 值**类型**元素被限制为下表中列出的字符串之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|*ProcessFull*|删除受影响的对象中的所有数据，然后处理该受影响的对象。|  
|*ProcessAdd*|将新数据添加到受影响的对象。|  
|*ProcessUpdate*|刷新受影响的对象中的数据。|  
|*ProcessIndexes*|创建或重新生成受影响的对象中的索引和聚合。|  
|*ProcessScriptCache*|如果已处理该多维数据集，则服务器将重新生成 MDX 脚本缓存。 如果未处理，将引发一个错误。<br /><br /> **请注意**仅适用于多维数据集。|  
|*ProcessData*|仅处理受影响的对象中的数据。|  
|*ProcessDefault*|检测受影响的对象的状态，然后对受影响的对象执行合适的处理选项，使之完全优化并使它恢复到完全处理的状态。|  
|*ProcessClear*|删除受影响的对象和所有相关对象中的数据。|  
|*ProcessStructure*|仅处理受影响的对象的结构。|  
|*ProcessClearStructureOnly*|仅清除受影响的对象中的数据。|  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
