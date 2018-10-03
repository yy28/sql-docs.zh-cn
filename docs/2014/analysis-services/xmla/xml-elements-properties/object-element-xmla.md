---
title: 对象元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Object Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Object
- urn:schemas-microsoft-com:xml-analysis#Object
- microsoft.xml.analysis.object
helpviewer_keywords:
- Object element
ms.assetid: 99470537-2c4a-4072-9613-940c41c12487
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e4fb7e25b9e813487b612bbd6269c2f080d85f5e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48178747"
---
# <a name="object-element-xmla"></a>Object 元素 (XMLA)
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
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|祖先或父级： [Alter](../xml-elements-commands/create-element-xmla.md) &#124; 0-1： 可出现一次且仅一次出现的可选元素。<br /><br /> 祖先或父级： 所有其他&#124;1-1： 出现一次且仅一次出现的必需的元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Alter](../xml-elements-commands/alter-element-xmla.md)，[备份](../xml-elements-commands/backup-element-xmla.md)， [ClearCache](../xml-elements-commands/clearcache-element-xmla.md)，[删除](../xml-elements-commands/delete-element-xmla.md)， [DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md)，[锁](../xml-elements-commands/lock-element-xmla.md)， [NotifyTableChange](../xml-elements-commands/notifytablechange-element-xmla.md)，[过程](../xml-elements-commands/process-element-xmla.md)，[订阅](../xml-elements-commands/subscribe-element-xmla.md)，[同步](../xml-elements-commands/synchronize-element-xmla.md)|  
|子元素|必需的 Analysis Services 脚本语言 (ASSL) 元素。 通过列出对象及其祖先（不包含 `Server` 对象）的 ID 元素指定这些必需元素。例如，以下 `Object` 元素标识分区：<br /><br /> `<Object>`<br /><br /> `<DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>`<br /><br /> `<CubeID>Adventure Works</CubeID>`<br /><br /> `<MeasureGroupID>Internet Sales</MeasureGroupID>`<br /><br /> `<PartitionID>Inernet_Sales_2001</PartitionID>`<br /><br /> `</Object>`|  
  
## <a name="remarks"></a>备注  
 标识符的显示顺序并不重要。  
  
 有关`Alter`元素、 的实例[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]如果用作默认对象`Object`未指定元素。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
