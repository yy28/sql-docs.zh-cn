---
title: "UnknownMember 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- UnknownMember Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- UnknownMember
helpviewer_keywords:
- UnknownMember element
ms.assetid: 5558961e-e3c6-4f4e-817d-5b12b0734c03
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5da9cdc237512a47a27b21691864b3da523ce70a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="unknownmember-element-assl"></a>UnknownMember 元素 (ASSL)
  指示未知成员是否可见。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Dimension>  
      ...  
   <UnknownMember>...</UnknownMember>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*无*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*可见*|未知成员存在并显示。|  
|*隐藏*|未知成员存在，但不显示。|  
|*无*|未知成员未使用。|  
  
 对应于的允许值为枚举**UnknownMember**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.UnknownMemberBehavior>。  
  
## <a name="see-also"></a>另请参阅  
 [UnknownMemberName 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/unknownmembername-element-assl.md)   
 [UnknownMemberTranslation 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/unknownmembertranslation-element-assl.md)   
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
