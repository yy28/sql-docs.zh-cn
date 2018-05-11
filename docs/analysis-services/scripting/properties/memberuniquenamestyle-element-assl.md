---
title: MemberUniqueNameStyle 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0c79a42cc8958c4c1dfa9ad7174e991a39620ff3
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="memberuniquenamestyle-element-assl"></a>MemberUniqueNameStyle 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  确定如何唯一名称的层次结构中包含的成员生成[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CubeDimension>  
   ...  
   <MemberUniqueNameStyle>...</MemberUniqueNameStyle>  
   ...  
</CubeDimension>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*本机*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>備註  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*本机*|该实例自动确定成员的唯一名称。|  
|*NamePath*|该实例将生成由每个级别和成员标题组成的复合名称。|  
  
## <a name="remarks"></a>注释  
 对应于的父元素**MemberUniqueNameStyle**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.CubeDimension>。  
  
## <a name="see-also"></a>另请参阅  
 [多维数据集元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [维度元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [CubeDimension 数据类型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)  
  
  
