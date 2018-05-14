---
title: 原始元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ae266466fd503e1f888bdcffd02f3cf2b066050a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="original-element-xmla"></a>Original 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含由原始文件系统存储位置[文件夹](../../../analysis-services/xmla/xml-elements-properties/folder-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Folder>  
   ...  
   <Original>...</Original>  
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
 **原始**元素包含要替换的值的 UNC 路径[新建](../../../analysis-services/xmla/xml-elements-properties/new-element-xmla.md)包含由容器的父元素**文件夹**还原的所有对象的元素或同步，分别期间[还原](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)或[同步](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)命令。 此元素的值进行比较的值[StorageLocation](../../../analysis-services/scripting/properties/storagelocation-element-assl.md)为每个多维数据集、 度量值组或分区的元素，如果找到匹配项，值**新建**元素用来更新**StorageLocation**还原或同步期间的对象。  
  
 有关备份和还原对象的详细信息，请参阅[Backing Up，正在还原，和同步数据库 & #40;XMLA & #41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
