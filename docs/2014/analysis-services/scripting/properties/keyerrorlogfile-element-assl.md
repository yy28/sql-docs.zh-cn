---
title: KeyErrorLogFile 元素 (ASSL) |Microsoft 文档
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
- KeyErrorLogFile Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- KeyErrorLogFile
helpviewer_keywords:
- KeyErrorLogFile element
ms.assetid: 1455bb54-03f7-4f25-9d4d-ab75231dd958
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3387498c26e0bf690b2934ea9e1ee99107414c04
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015516"
---
# <a name="keyerrorlogfile-element-assl"></a>KeyErrorLogFile 元素 (ASSL)
  包含记录处理错误的文件名。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ErrorConfiguration>  
   ...  
      <KeyErrorLogFile>...</KeyErrorLogFile>  
   ...  
</ErrorConfiguration>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ErrorConfiguration](../objects/errorconfiguration-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 对应于的父元素`KeyErrorLogFile`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ErrorConfiguration>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  