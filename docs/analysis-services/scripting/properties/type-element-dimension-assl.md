---
title: 类型元素 （维度） (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3af3168c39f685702154bb7c76435bd1d241a642
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34039361"
---
# <a name="type-element-dimension-assl"></a>Type 元素 (Dimension) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  提供有关维度内容的信息。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Dimension>  
      ...  
   <Type>...</Type>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*Regular*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[维度](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 某些值**类型**，例如*帐户*，确定特定的行为。  
  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*Regular*|该维度是一个常规维度。|  
|*Time*|该维度是一个时间维度。<br /><br /> 注意： 此值指示维度支持特定于时间维度的功能。|  
|*Geography*|维度包含地域属性。|  
|*组织*|维度包含单位属性。|  
|*物料清单*|维度包含物料清单属性。|  
|*帐户*|维度包含帐户相关属性。<br /><br /> 注意： 此值指示维度支持特定于帐户维度的功能。|  
|*Customers*|维度包含客户相关属性。|  
|*产品*|维度包含产品相关属性。|  
|*方案*|维度包含方案相关属性。|  
|*Quantitative*|维度包含定量属性。|  
|*实用工具*|维度包含效用属性。|  
|*货币*|维度包含货币属性。|  
|*费率*|维度包含汇率属性。|  
|*Channel*|维度包含渠道属性。|  
|*Promotion*|维度包含促销相关属性。|  
  
 对应于的允许值为枚举**类型**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.DimensionType>。  
  
 对应于的父元素**类型**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Dimension>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
