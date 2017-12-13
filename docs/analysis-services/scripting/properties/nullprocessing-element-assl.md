---
title: "NullProcessing 元素 (ASSL) |Microsoft 文档"
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.custom: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: NullProcessing Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: NullProcessing
helpviewer_keywords: NullProcessing element
ms.assetid: 697be5c6-e9a6-4f74-9ff4-5f31400c2178
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8b5f63a3b5813dc053bc9323b1317a98f92b3303
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="nullprocessing-element-assl"></a>NullProcessing Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]定义如何 null 值处理。  
  
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
  
## <a name="remarks"></a>注释  
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
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
