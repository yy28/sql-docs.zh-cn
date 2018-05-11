---
title: NullKeyConvertedToUnknown 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c3d101e2577a7e691aae685bcf821979b5640182
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="nullkeyconvertedtounknown-element-assl"></a>NullKeyConvertedToUnknown 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  指定遇到空转换错误时要执行的操作。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ErrorConfiguration>  
   ...  
      <NullKeyConvertedToUnknown>...</NullKeyConvertedToUnknown>  
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
 空转换错误发生时遇到的键列中 null 值并将其解释为**未知**成员。 仅当，但是，发生此错误[NullProcessing](../../../analysis-services/scripting/properties/nullprocessing-element-assl.md)元素[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)的祖先**ErrorConfiguration**父元素设置为*UnknownMember*。  
  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*IgnoreError*|处理将忽略该错误并继续。|  
|*ReportAndContinue*|处理报告错误并继续。|  
|*ReportAndStop*|处理报告错误并停止。|  
  
 对应于的允许值为枚举**NullKeyConvertedToUnknown**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ErrorOption>。  
  
## <a name="see-also"></a>另请参阅  
 [ErrorConfiguration 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
