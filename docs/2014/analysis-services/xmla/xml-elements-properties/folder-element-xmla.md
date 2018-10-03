---
title: Folder 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Folder Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.folder
- http://schemas.microsoft.com/analysisservices/2003/engine#Folder
- urn:schemas-microsoft-com:xml-analysis#Folder
helpviewer_keywords:
- Folder element
ms.assetid: 87b305b0-57e3-4ec3-9d80-f1bcf3ce7540
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 70c5258edefa19d2858c40648aa742f75a9a1e49
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48055119"
---
# <a name="folder-element-xmla"></a>Folder 元素 (XMLA)
  包含要更新的文件系统存储位置[位置](location-element-xmla.md)期间[还原](../xml-elements-commands/restore-element-xmla.md)或[同步](../xml-elements-commands/synchronize-element-xmla.md)命令。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Folders>  
   ...  
   <Folder>  
      <Original>...</Original>  
      <New>...</New>  
   </Folder>  
   ...  
</Folders>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[文件夹](folders-element-xmla.md)|  
|子元素|[新](new-element-xmla.md)，[原始](original-element-xmla.md)|  
  
## <a name="remarks"></a>备注  
 如果指定 `Folder` 元素，当备份文件（对于 `Restore` 命令）或源实例上的数据库（对于 `Synchronize` 命令）中包含的对象的存储位置与 `Original` 元素的值相匹配时，该位置将更改为 `New` 元素的值。  
  
 有关备份和还原对象的详细信息，请参阅[备份、 还原和同步数据库&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
## <a name="see-also"></a>请参阅  
 [StorageLocation 元素&#40;ASSL&#41;](../../scripting/properties/storagelocation-element-assl.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
