---
title: 撰写 MergePartitions 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4cfe28f42c56e73109b3d3d939f433e48b09ed43
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="mergepartitions-element-xmla"></a>MergePartitions 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  将一个或多个源分区的数据合并到目标分区，，然后删除源分区。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Command>  
   <MergePartitions>  
      <Sources>...</Sources>  
      <Target>...</Target>  
   </MergePartitions>  
</Command>  
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
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[源](../../../analysis-services/xmla/xml-elements-properties/sources-element-xmla.md)，[目标](../../../analysis-services/xmla/xml-elements-properties/target-element-xmla.md)|  
  
## <a name="remarks"></a>注释  
 所有对象中的引用**源**和**目标**元素必须指向相同的度量值组中的不同分区。 否则，将会出错。  
  
## <a name="see-also"></a>另请参阅  
 [命令 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
