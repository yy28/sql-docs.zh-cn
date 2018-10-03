---
title: Mode 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Mode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Mode
- microsoft.xml.analysis.mode
- http://schemas.microsoft.com/analysisservices/2003/engine#Mode
helpviewer_keywords:
- Mode element
ms.assetid: 43a54181-6494-48c3-b14b-376d8939fa9f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e768d9ef176a05d4fe7622a520c9ac98f1d71d81
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48072407"
---
# <a name="mode-element-xmla"></a>Mode 元素 (XMLA)
  标识父对象使用的模式[锁](../xml-elements-commands/lock-element-xmla.md)元素时指定的对象上创建锁。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Lock>  
   ...  
   <Mode>...</Mode>  
   ...  
</Lock>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|None|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[锁](../xml-elements-commands/lock-element-xmla.md)，[解锁](../xml-elements-commands/unlock-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 父级 `Lock` 元素使用 `Mode` 元素确定要为对象创建的锁的类型。 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*CommitShared*|对指定对象建立一个共享锁。 还可以为同一对象创建其他共享锁。<br /><br /> 共享的锁将阻止包含写操作，如事务[Execute](../xml-elements-methods-execute.md)方法调用运行[Alter](../xml-elements-commands/alter-element-xmla.md)命令，对指定的对象，从提交之前删除该共享的锁。 共享的锁不会阻止包含读的操作，如事务[Discover](../xml-elements-methods-discover.md)方法调用或`Execute`方法调用运行[语句](../xml-elements-commands/statement-element-xmla.md)命令的提交。|  
|*CommitExclusive*|对指定对象建立一个排他锁。 不可为同一对象创建其他共享锁或排他锁。<br /><br /> 排他锁可阻止指定对象的包含写或读操作的事务的提交，阻止会一直持续到该排他锁被删除为止。|  
  
## <a name="see-also"></a>请参阅  
 [ID 元素&#40;XMLA&#41;](id-element-xmla.md)   
 [对象元素&#40;XMLA&#41;](object-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
