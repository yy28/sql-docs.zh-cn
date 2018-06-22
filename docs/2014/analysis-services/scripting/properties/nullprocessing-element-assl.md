---
title: NullProcessing 元素 (ASSL) |Microsoft 文档
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
- NullProcessing Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- NullProcessing
helpviewer_keywords:
- NullProcessing element
ms.assetid: 697be5c6-e9a6-4f74-9ff4-5f31400c2178
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 54b75b2e1a7bddd6f7b5df1aeda0311c1b60ff99
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015322"
---
# <a name="nullprocessing-element-assl"></a>NullProcessing Element (ASSL)
  定义如何处理空值。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DataItem>  
   ...  
   <NullProcessing>...</NullProcessing>  
   ...  
</DataItem>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*自动*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*保留*|保留空值。 **注意：** 非重复计数度量值不支持此值。|  
|*错误*|引发空键错误。 值[NullKeyNotAllowed](nullkeynotallowed-element-assl.md)确定实例如何对错误做出响应。 **注意：** 度量值不支持此值。|  
|*UnknownMember*|生成一个未知成员并引发空转换错误。 值[NullKeyConvertedToUnknown](nullkeyconvertedtounknown-element-assl.md)确定实例如何对错误做出响应。 **注意：** 与度量值相关的列不支持此值。|  
|*ZeroOrBlank*|将空值转换为零（对数值数据项）或空白字符串（对字符串数据项）。 **注意：** 此值提供与以前版本的兼容性[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。|  
|*自动*|使用适用于该元素的默认处理方式：<br /><br /> -   *ZeroOrBlank*对于 OLAP 数据项。<br />-   *UnknownMember*对于数据挖掘数据项。|  
  
 对应于的允许值为枚举`NullProcessing`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.NullProcessing>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  