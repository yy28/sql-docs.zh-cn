---
title: WritebackTableCreation 元素 (XMLA) |Microsoft Docs
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
- WritebackTableCreation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#WritebackTableCreation
- microsoft.xml.analysis.writebacktablecreation
- http://schemas.microsoft.com/analysisservices/2003/engine#WritebackTableCreation
helpviewer_keywords:
- WritebackTableCreation element
ms.assetid: e9579d63-e28c-4d4e-9f4a-21c5da24c276
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9908cf615ef5f767b72e639023b0444f02e71f7a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37319207"
---
# <a name="writebacktablecreation-element-xmla"></a>WritebackTableCreation 元素 (XMLA)
  确定是否将写回表创建期间[进程](../xml-elements-commands/process-element-xmla.md)操作。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Process>  
...  
   <WritebackTableCreation>...</WritebackTableCreation>  
...  
</Process>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[处理](../xml-elements-commands/process-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 Analysis Services 实例上可用的对象处理选项的详细信息，请参阅[多维模型对象处理](../../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。  
  
 `WritebackTableCreation` 元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*创建*|如果不存在写回表，则创建一个新表。 如果写回表已存在，则会出错。|  
|*CreateAlways*|创建一个新的写回表，覆盖任何现有的写回表。|  
|*UseExisting*|如果已存在，请使用现有写回表。 如果写回表不存在，则会出错。|  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
