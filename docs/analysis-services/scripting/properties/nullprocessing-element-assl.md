---
title: NullProcessing 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 9e5fbc3682a614dc1599347ec030348ae10bb2c0
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34038361"
---
# <a name="nullprocessing-element-assl"></a>NullProcessing Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*自动*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>備註  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*保留*|保留空值。<br /><br /> 注意： 此值不支持非重复计数度量值。|  
|*错误*|引发空键错误。 值[NullKeyNotAllowed](../../../analysis-services/scripting/properties/nullkeynotallowed-element-assl.md)确定实例如何对错误做出响应。<br /><br /> 注意： 此值不支持度量值。|  
|*UnknownMember*|生成一个未知成员并引发空转换错误。 值[NullKeyConvertedToUnknown](../../../analysis-services/scripting/properties/nullkeyconvertedtounknown-element-assl.md)确定实例如何对错误做出响应。<br /><br /> 注意： 与度量值相关的列不支持此值。|  
|*ZeroOrBlank*|将空值转换为零（对数值数据项）或空白字符串（对字符串数据项）。<br /><br /> 注意： 此值提供与以前版本的兼容性[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。|  
|*自动*|使用适用于该元素的默认处理方式：<br /><br /> 对于 OLAP 数据项，使用*ZeroOrBlank* 。<br /><br /> 对于数据挖掘数据项，使用*UnknownMember* 。|  
  
 对应于的允许值为枚举**NullProcessing**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.NullProcessing>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
