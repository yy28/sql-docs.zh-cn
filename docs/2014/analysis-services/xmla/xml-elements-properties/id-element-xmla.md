---
title: ID 元素 (XMLA) |Microsoft 文档
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
- ID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#ID
- urn:schemas-microsoft-com:xml-analysis#ID
- microsoft.xml.analysis.id
helpviewer_keywords:
- ID element
ms.assetid: f7d67599-6a70-4455-bfdb-1d127e5eff4e
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 78cfec49d1af81336d8cfadcb9f502294f1326da
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015959"
---
# <a name="id-element-xmla"></a>ID 元素 (XMLA)
  标识对其执行父锁[锁](../xml-elements-commands/lock-element-xmla.md)或[解锁](../xml-elements-commands/unlock-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Lock> <!-- or Unlock>  
   ...  
   <ID>...</ID>  
   ...  
</Lock>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[锁定](../xml-elements-commands/lock-element-xmla.md)，[解锁](../xml-elements-commands/unlock-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `ID` 元素包含用于标识锁的全局唯一标识符 (GUID)。  
  
## <a name="see-also"></a>请参阅  
 [对象元素&#40;XMLA&#41;](object-element-xmla.md)   
 [模式元素&#40;XMLA&#41;](mode-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  