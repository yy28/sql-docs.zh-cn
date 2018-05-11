---
title: 设置元素 (ASSL) 的格式 |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 344730d6f46a3772252a91d6672f44b7f54e1123
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="format-element-assl"></a>Format 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含所需的格式的[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DataItem>  
   ...  
   <Format>...</Format>  
      ...  
</DataItem>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 允许值**格式**元素是 Microsoft Office Excel 格式和字符串*TrimRight*， *TrimLeft*， *TrimAll*，和*TrimNone*。 用于进行裁剪， *TrimRight*是默认设置。  
  
 此元素的值限定为下表中的字符串之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|任何 Excel 格式的字符串|根据指定的命名格式字符串或自定义格式字符串设置数据的格式。 可指定 Excel 支持的任何格式的字符串。|  
|*TrimAll*|对数据的左侧和右侧进行修整。|  
|*TrimLeft*|对数据的左侧进行修整。|  
|*TrimNone*|不修整数据。|  
|*TrimRight*|对数据的右侧进行修整。|  
  
 对应于的父元素**格式**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.DataItem>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
