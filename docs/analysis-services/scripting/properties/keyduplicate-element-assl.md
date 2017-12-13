---
title: "KeyDuplicate 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: KeyDuplicate Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: KeyDuplicate
helpviewer_keywords: KeyDuplicate element
ms.assetid: d7000b8b-e81f-4401-8738-00c2e0f73a59
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3ae40ac43c34daef29a1c69218e057e47ccbced6
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="keyduplicate-element-assl"></a>KeyDuplicate 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]确定如何[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]如果遇到一个处理过程中处理重复键错误。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ErrorConfiguration>  
   ...  
      <KeyDuplicate>...</KeyDuplicate>  
   ...  
</ErrorConfiguration>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*IgnoreError*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 仅在维度处理期间，多次遇到属性键时才会生成“重复键”错误。 因为属性键必须是唯一的，因此 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 丢弃重复的记录。 “重复键”错误通常指示维度设计（特别是属性间的关系）中的缺陷。  
  
 此元素的值限定为下表中的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*IgnoreError*|处理应忽略错误并继续。|  
|*ReportAndContinue*|处理应报告错误并继续。|  
|*ReportAndStop*|处理应报告错误并停止。|  
  
 对应于的允许值为枚举**KeyDuplicate**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ErrorOption>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
