---
title: "NullKeyNotAllowed 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: NullKeyNotAllowed Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: NullKeyNotAllowed
helpviewer_keywords: NullKeyNotAllowed element
ms.assetid: 4ece99eb-954b-4da1-add4-dd9efd5fff0a
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: dfb9349ff91eae2c4e783f347f5df978d27c95c2
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="nullkeynotallowed-element-assl"></a>NullKeyNotAllowed 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]确定如何[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]处理引擎处理处理过程中遇到 null 键错误。  
  
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
|父元素|[ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 在处理过程，如果在不允许空值的键列中遇到空值，则就会发生空键错误，这将迫使抛弃该记录。 仅当，但是，发生此错误[NullProcessing](../../../analysis-services/scripting/properties/nullprocessing-element-assl.md)元素**DataItem**的祖先**ErrorConfiguration**父元素设置为*错误*。  
  
 此元素的值限定为下表中的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*IgnoreError*|处理将忽略该错误并继续。|  
|*ReportAndContinue*|处理报告错误并继续。|  
|*ReportAndStop*|处理报告错误并停止。|  
  
 对应于的允许值为枚举**NullKeyNotAllowed**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ErrorOption>。  
  
## <a name="see-also"></a>另请参阅  
 [ErrorConfiguration 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)  
  
  
