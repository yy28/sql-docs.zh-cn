---
title: 类型元素 （绑定） (ASSL) |Microsoft 文档
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
- Type Element (Binding)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: b5f5c485-dc83-4d66-a8d2-e96e96d068f9
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b07c1d781bfdade9228b6c5991b2eb56585cbe85
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017613"
---
# <a name="type-element-binding-assl"></a>Type 元素 (Binding) (ASSL)
  包含属性绑定的类型。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AttributeBinding> <!-- or CubeAttributeBinding -->  
   ...  
   <Type>...</Type>  
   ...  
</AttributeBinding>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AttributeBinding](../data-type/binding-data-type-assl.md)， [CubeAttributeBinding](../data-type/cubeattributebinding-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*全部*|所有级别|  
|*Key*|成员键|  
|*名称*|成员名称|  
|*ReplTest1*|成员值|  
|*转换*|成员翻译|  
|*UnaryOperator*|一元运算符|  
|*SkippedLevels*|跳过的级别|  
|*CustomRollup*|自定义汇总公式|  
|*CustomRollupProperties*|自定义汇总属性|  
  
 对应的父级的元素`Type`分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.AttributeBinding>和<xref:Microsoft.AnalysisServices.CubeAttributeBinding>。  
  
## <a name="see-also"></a>请参阅  
 [绑定数据类型&#40;ASSL&#41;](../data-type/binding-data-type-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  