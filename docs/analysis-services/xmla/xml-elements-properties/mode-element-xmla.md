---
title: "模式元素 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Mode Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Mode
- microsoft.xml.analysis.mode
- http://schemas.microsoft.com/analysisservices/2003/engine#Mode
helpviewer_keywords: Mode element
ms.assetid: 43a54181-6494-48c3-b14b-376d8939fa9f
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3e2047c923e6c205990c58602e1694f645ef97c2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="mode-element-xmla"></a>Mode 元素 (XMLA)
  标识要使用由容器的父模式[锁](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)元素在指定的对象上创建锁时。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Lock>  
   ...  
   <Mode>...</Mode>  
   ...  
</Lock>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[锁定](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)，[解锁](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 父**锁**元素使用**模式**元素来确定的锁的对象创建的类型。 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*CommitShared*|对指定对象建立一个共享锁。 还可以为同一对象创建其他共享锁。<br /><br /> 共享的锁可防止事务包含写入操作，如[执行](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法调用运行[Alter](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)命令，对指定的对象，从提交之前删除的共享的锁。 共享的锁不会阻止事务包含读取的操作，如[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法调用或**执行**方法调用运行[语句](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)命令，从正在提交。|  
|*CommitExclusive*|对指定对象建立一个排他锁。 不可为同一对象创建其他共享锁或排他锁。<br /><br /> 排他锁可阻止指定对象的包含写或读操作的事务的提交，阻止会一直持续到该排他锁被删除为止。|  
  
## <a name="see-also"></a>另请参阅  
 [ID 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/id-element-xmla.md)   
 [Object 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)   
 [属性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
