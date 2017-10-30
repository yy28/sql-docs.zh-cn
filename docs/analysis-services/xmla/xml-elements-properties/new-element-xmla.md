---
title: "新元素 (XMLA) |Microsoft 文档"
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
- New Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#New
- microsoft.xml.analysis.new
- urn:schemas-microsoft-com:xml-analysis#New
helpviewer_keywords:
- New element
ms.assetid: 1321adcb-67f7-40f0-8f20-b17c1d3e3f17
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5eade126deeecbe8b224077d506c8231587f739d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="new-element-xmla"></a>New 元素 (XMLA)
  包含新的文件系统存储位置由[文件夹](../../../analysis-services/xmla/xml-elements-properties/folder-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Folder>  
   ...  
   <New>...</New>  
   ...  
</Folder>  
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
|父元素|[文件夹](../../../analysis-services/xmla/xml-elements-properties/folder-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **新建**元素包含替换的值的 UNC 路径**原始**包含由容器的父元素**文件夹**还原或同步，所有对象的元素分别在**还原**或**同步**命令。 值**原始**元素进行比较的值**StorageLocation**为每个多维数据集、 度量值组或分区的元素，如果找到匹配项，则此元素的值用于更新**StorageLocation**还原或同步期间的对象。  
  
 有关备份和还原对象的详细信息，请参阅[备份和还原对象 (XMLA)](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
## <a name="see-also"></a>另请参阅  
 [原始元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/original-element-xmla.md)   
 [还原元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [StorageLocation 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/storagelocation-element-assl.md)   
 [同步元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [属性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

