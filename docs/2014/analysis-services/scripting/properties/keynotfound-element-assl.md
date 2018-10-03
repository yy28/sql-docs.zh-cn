---
title: KeyNotFound 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- KeyNotFound Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- KeyNotFound
helpviewer_keywords:
- KeyNotFound element
ms.assetid: 2a93bbfa-2409-4e94-8b68-926532895a4c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7e8a2233797d3d9ddeecc91d5c2b5f096866d624
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48156597"
---
# <a name="keynotfound-element-assl"></a>KeyNotFound 元素 (ASSL)
  指定如何[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]时遇到引用完整性错误的响应。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ErrorConfiguration>  
   ...  
      <KeyNotFound>...</KeyNotFound>  
   ...  
</ErrorConfiguration>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*ReportAndContinue*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ErrorConfiguration](../objects/errorconfiguration-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 当依赖表中的外键值在父表中没有对应条目时会引发引用完整性错误。 当 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 处理维度时，如果其中的事实数据表引用该维度的维度表中不存在的外键值，或者当 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 处理分区时，分区中包含的某个维度的维度主表引用另一个关联维度表中不存在的键值，则会引发此错误。 （如果是具有父子层次结构和父属性的维度，则当分区中包含的某个维度的维度主表引用同一维度表中不存在的键值时，也会引发此错误。）  
  
 此元素的值限定为下表中的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*IgnoreError*|处理应忽略错误并继续。|  
|*ReportAndContinue*|处理应报告错误并继续。|  
|*ReportAndStop*|处理应报告错误并停止。|  
  
 与允许的值相对应的枚举`KeyNotFound`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.ErrorOption>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
