---
title: 新元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- New Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#New
- microsoft.xml.analysis.new
- urn:schemas-microsoft-com:xml-analysis#New
helpviewer_keywords:
- New element
ms.assetid: 1321adcb-67f7-40f0-8f20-b17c1d3e3f17
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 01f159352499625bf5065c96fcbd057590570610
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48222377"
---
# <a name="new-element-xmla"></a>New 元素 (XMLA)
  包含使用的新文件系统存储位置[文件夹](folder-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Folder>  
   ...  
   <New>...</New>  
   ...  
</Folder>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|None|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[文件夹](folder-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 `New` 元素包含一个 UNC 路径，对于执行 `Original` 或 `Folder` 命令时分别还原或同步的所有对象，该路径将替换父 `Restore` 元素所包含的 `Synchronize` 元素值。 `Original` 元素的值将与每个多维数据集、度量值组或分区的 `StorageLocation` 元素值进行比较，如果发现匹配，则在还原或同步期间，此元素的值将用于更新对象的 `StorageLocation`。  
  
 有关备份和还原对象的详细信息，请参阅[备份和还原对象 (XMLA)](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
## <a name="see-also"></a>请参阅  
 [原始元素&#40;XMLA&#41;](original-element-xmla.md)   
 [Restore 元素&#40;XMLA&#41;](../xml-elements-commands/restore-element-xmla.md)   
 [StorageLocation 元素&#40;ASSL&#41;](../../scripting/properties/storagelocation-element-assl.md)   
 [Synchronize 元素&#40;XMLA&#41;](../xml-elements-commands/synchronize-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
