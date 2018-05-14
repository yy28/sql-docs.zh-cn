---
title: 对象元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 56de6684969db18c66d57c95e3dec589a48fed89
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="object-element-xmla"></a>Object 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含父元素使用的对象引用。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Alter> <!-- or any of the parent elements in the Element Relationships table -->  
...  
   <Object>  
      <!-- One or more object identifiers, depending on the parent element -->  
   </Object>  
...  
</Alter>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|请参阅下表。|  
  
|祖先或父级|基数|  
|------------------------|-----------------|  
|[Alter](../../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)|0-1：可出现一次且仅出现一次的可选元素。|  
|其他|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Alter](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)，[备份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)， [ClearCache](../../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md)，[删除](../../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)， [DesignAggregations](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)，[锁](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)， [NotifyTableChange](../../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md)，[过程](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)，[订阅](../../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md)，[同步](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|  
|子元素|必需的 Analysis Services 脚本语言 (ASSL) 元素。 指定通过列出的对象，并且其上级的 ID 元素 (不包括**服务器**对象。)例如，以下**对象**元素确定分区：<br /><br /> `<Object>`<br /><br /> `<DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>`<br /><br /> `<CubeID>Adventure Works</CubeID>`<br /><br /> `<MeasureGroupID>Internet Sales</MeasureGroupID>`<br /><br /> `<PartitionID>Inernet_Sales_2001</PartitionID>`<br /><br /> `</Object>`|  
  
## <a name="remarks"></a>注释  
 标识符的显示顺序并不重要。  
  
 有关**Alter**元素、 实例[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]如果用作默认对象**对象**未指定元素。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
