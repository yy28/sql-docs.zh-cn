---
title: 类型元素 (XMLA) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Type Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.type
- http://schemas.microsoft.com/analysisservices/2003/engine#Type
- urn:schemas-microsoft-com:xml-analysis#Type
helpviewer_keywords:
- Type element
ms.assetid: 5d898123-a635-402a-be86-8249d7304fa4
caps.latest.revision: 15
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 38b4442afe95f06d9a6f437e906c01b7386d91ae
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026622"
---
# <a name="type-element-xmla"></a>Type 元素 (XMLA)
  确定要执行的处理的类型[过程](../xml-elements-commands/process-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Process>  
...  
   <Type>...</Type>  
...  
</Process>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[处理](../xml-elements-commands/process-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 有关处理提供给对象的实例上的选项的详细信息[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，请参阅[多维模型对象处理](../../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。  
  
 `Type` 元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
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
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  