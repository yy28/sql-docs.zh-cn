---
title: ID 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 86a24d14a0c9e198c879e4dce092f430a4755871
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48110127"
---
# <a name="id-element-xmla"></a>ID 元素 (XMLA)
  标识要对其执行父锁[锁](../xml-elements-commands/lock-element-xmla.md)或[解锁](../xml-elements-commands/unlock-element-xmla.md)元素。  
  
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
|默认值|None|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[锁](../xml-elements-commands/lock-element-xmla.md)，[解锁](../xml-elements-commands/unlock-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 `ID` 元素包含用于标识锁的全局唯一标识符 (GUID)。  
  
## <a name="see-also"></a>请参阅  
 [对象元素&#40;XMLA&#41;](object-element-xmla.md)   
 [Mode 元素&#40;XMLA&#41;](mode-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
