---
title: NullKeyNotAllowed 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- NullKeyNotAllowed Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- NullKeyNotAllowed
helpviewer_keywords:
- NullKeyNotAllowed element
ms.assetid: 4ece99eb-954b-4da1-add4-dd9efd5fff0a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0d17edc031d66282b433571b18ef1c32cf6e09bf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48054567"
---
# <a name="nullkeynotallowed-element-assl"></a>NullKeyNotAllowed 元素 (ASSL)
  确定如何[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]处理引擎处理在处理过程中遇到的 null 键错误。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ErrorConfiguration>  
   ...  
   <NullKeyNotAllowed>...</NullKeyNotAllowed>  
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
 在处理过程，如果在不允许空值的键列中遇到空值，则就会发生空键错误，这将迫使抛弃该记录。 但是，此错误发生才[NullProcessing](nullprocessing-element-assl.md)元素`DataItem`的祖先`ErrorConfiguration`父元素设置为*错误*。  
  
 此元素的值限定为下表中的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*IgnoreError*|处理会忽略该错误并继续。|  
|*ReportAndContinue*|处理报告错误并继续。|  
|*ReportAndStop*|处理报告错误并停止。|  
  
 与允许的值相对应的枚举`NullKeyNotAllowed`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.ErrorOption>。  
  
## <a name="see-also"></a>请参阅  
 [ErrorConfiguration 元素&#40;ASSL&#41;](../objects/errorconfiguration-element-assl.md)  
  
  
