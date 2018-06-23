---
title: 异常元素 (XMLA) |Microsoft 文档
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
- Exception Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Exception
- urn:schemas-microsoft-com:xml-analysis#Exception
- microsoft.xml.analysis.exception
helpviewer_keywords:
- Exception element
ms.assetid: 0be4cc2f-c03e-490a-a6f7-8b1ede5d09ba
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 824743a3e8aeb7d735d6844dd1b025de06e09e9d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025516"
---
# <a name="exception-element-xmla"></a>Exception 元素 (XMLA)
  表示从返回了异常[发现](../xml-elements-methods-discover.md)或[执行](../xml-elements-methods-execute.md)方法调用。  
  
 **Namespace** http://schemas.microsoft.com/analysisservices/2003/exception  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<root>  
   ...  
   <Exception />  
   ...  
</root>  
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
|父元素|[根](root-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 如果在执行 `Discover` 方法调用或 `Execute` 方法调用中的单个 XMLA 命令时发生使该方法或命令不能完成的错误，则该方法或命令的 `root` 元素将包含一个 `Exception` 元素和一个 `Messages` 元素。 `Exception` 元素指示发生了使方法或命令不能成功执行的错误，而 `Messages` 元素包含与该错误相关的错误消息或警告消息的列表。  
  
## <a name="see-also"></a>请参阅  
 [消息元素&#40;XMLA&#41;](messages-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  