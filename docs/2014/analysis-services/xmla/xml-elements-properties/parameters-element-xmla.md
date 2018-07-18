---
title: Parameters 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Parameters Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Parameters
- urn:schemas-microsoft-com:xml-analysis#Parameters
- microsoft.xml.analysis.parameters
helpviewer_keywords:
- Parameters element
ms.assetid: d46454a1-a1d1-4aa8-95ea-54be22a53e83
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 87836c6ca9f33c100b3ba10ba91379370e787773
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37158858"
---
# <a name="parameters-element-xmla"></a>Parameters 元素 (XMLA)
  包含一系列[参数](parameter-element-xmla.md)所使用的元素[Execute](../xml-elements-methods-execute.md)方法。  
  
 **Namespace**：`urn:schemas-microsoft-com:xml-analysis`  
  
## <a name="syntax"></a>语法  
  
```  
  
<Execute>  
...  
   <Parameters>  
      <Parameter>...</Parameter>  
   </Parameters>  
...  
</Execute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[执行](../xml-elements-methods-execute.md)|  
|子元素|[参数](parameter-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 某些 XML for Analysis (XMLA) 命令，如[进程](../xml-elements-commands/process-element-xmla.md)命令，可能需要其他信息。 `Parameters` 元素可提供一种机制，从而为 XMLA 命令提供附加信息，包括成块信息。  
  
 如果 XMLA 命令不使用 `Parameters` 元素，则该元素可以在调用 `Execute` 方法时省略。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
