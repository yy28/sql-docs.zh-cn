---
title: "Folder 元素 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Folder Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.folder
- http://schemas.microsoft.com/analysisservices/2003/engine#Folder
- urn:schemas-microsoft-com:xml-analysis#Folder
helpviewer_keywords: Folder element
ms.assetid: 87b305b0-57e3-4ec3-9d80-f1bcf3ce7540
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0efdb0e0f6d070f57f65c9ee074f076569d2d6d5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="folder-element-xmla"></a>Folder 元素 (XMLA)
  包含要更新的文件系统存储位置[位置](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)期间元素[还原](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)或[同步](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)命令。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[文件夹](../../../analysis-services/xmla/xml-elements-properties/folders-element-xmla.md)|  
|子元素|[新](../../../analysis-services/xmla/xml-elements-properties/new-element-xmla.md)，[原始](../../../analysis-services/xmla/xml-elements-properties/original-element-xmla.md)|  
  
## <a name="remarks"></a>注释  
 **文件夹**元素，如果指定，更改存储位置的对象包含通过备份文件 (对于**还原**命令) 或源实例上的数据库 (有关**同步**命令) 的值都匹配**原始**为的值的元素**新建**元素。  
  
 有关备份和还原对象的详细信息，请参阅[Backing Up，正在还原，和同步数据库 &#40;XMLA &#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>另请参阅  
 [StorageLocation 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/storagelocation-element-assl.md)   
 [属性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
