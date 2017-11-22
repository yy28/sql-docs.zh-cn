---
title: "KeyErrorLogFile 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: KeyErrorLogFile Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: KeyErrorLogFile
helpviewer_keywords: KeyErrorLogFile element
ms.assetid: 1455bb54-03f7-4f25-9d4d-ab75231dd958
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5d7636950dfc39d7289b5af90e657f61642dac27
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对应于的父元素**KeyErrorLogFile**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ErrorConfiguration>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
