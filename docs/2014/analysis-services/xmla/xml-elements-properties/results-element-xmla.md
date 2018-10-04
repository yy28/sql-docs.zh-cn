---
title: 结果元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- results Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.results
- urn:schemas-microsoft-com:xml-analysis#results
- http://schemas.microsoft.com/analysisservices/2003/engine#results
helpviewer_keywords:
- results element
ms.assetid: 3249a17a-7bfa-4753-b605-8f611ba7ae2b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e99728941db468f361535fa675281f880ad3133a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48091357"
---
# <a name="results-element-xmla"></a>results 元素 (XMLA)
  包含一系列[根](root-element-xmla.md)返回的元素[Execute](../xml-elements-methods-execute.md)方法使用[批处理](../xml-elements-commands/batch-element-xmla.md)命令。  
  
 **Namespace** http://schemas.microsoft.com/analysisservices/2003/xmla-multipleresults  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<return>  
   <results>  
      <root>...</root>  
   </results>  
</return>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[返回](return-element-xmla.md)|  
|子元素|[根](root-element-xmla.md)|  
  
## <a name="remarks"></a>备注  
 如果 `Batch` 命令由 `Execute` 方法执行，则 `return` 元素将包含单个 `results` 元素，而非单个 `root` 元素。 `results` 元素的内容取决于用于运行 `Batch` 命令的设置。  
  
 对于非事务性 `Batch` 命令，无论 `results` 命令所执行的命令是否成功完成，`root` 元素都会包含所有这些命令的一个 `Batch` 元素。 但对于事务性 `Batch` 命令，`results` 元素只包含一个 `root` 元素，该元素中包含有 `Batch` 命令中的失败命令的错误信息。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
