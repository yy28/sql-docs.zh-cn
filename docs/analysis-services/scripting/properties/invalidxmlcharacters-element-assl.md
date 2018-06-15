---
title: InvalidXmlCharacters 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 8c1f382ce5e353c590249d677faff5b5810fd035
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34031588"
---
# <a name="invalidxmlcharacters-element-assl"></a>InvalidXmlCharacters 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  指定源数据中无效 XML 字符的处理方法。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DataItem>  
   ...  
   <InvalidXmlCharacters>...</InvalidXmlCharacters>  
   ...  
</DataItem  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*保留*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此元素的值限定为下表中的字符串之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|*保留*|保留无效 XML 字符。|  
|*删除*|删除无效 XML 字符。|  
|*替换*|用问号 (?) 字符替换无效的 XML 字符。|  
  
 对应于的允许值为枚举**InvalidXmlCharacters**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.InvalidXmlCharacters>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
