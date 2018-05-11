---
title: 序号元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 88c2409d42fc23f017989218d8ea87172d1b8d3d
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="ordinal-element-assl"></a>Ordinal 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  指示要绑定到集合（如键和翻译）中的序号。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AttributeBinding> <!-- or CubeAttributeBinding -->  
   ...  
   <Ordinal>...</Ordinal>  
   ...  
</AttributeBinding>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Integer|  
|默认值|**0**|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)， [CubeAttributeBinding](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **AttributeBinding**和**CubeAttributeBinding**元素在其中[类型](../../../analysis-services/scripting/properties/type-element-binding-assl.md)属性设置为*密钥*或*转换*可以绑定到反过来绑定到数据源视图中的列集合的属性。 值**序号**元素确定哪一列到**AttributeBinding**或**CubeAttributeBinding**引用该集合中。  
  
 对应的父级的元素**序号**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.AttributeBinding>和<xref:Microsoft.AnalysisServices.CubeAttributeBinding>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
