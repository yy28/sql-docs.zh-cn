---
title: 设置元素 (ASSL) 的格式 |Microsoft 文档
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
- Format Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Format
helpviewer_keywords:
- Format element
ms.assetid: 881ea707-52a7-46f7-ba16-ac2ec44eca22
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b7434ba5d6e2db8d2a2e665fa333799b6b2e9eb8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128865"
---
# <a name="format-element-assl"></a>Format 元素 (ASSL)
  包含所需的格式的[DataItem](../data-type/dataitem-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DataItem>  
   ...  
   <Format>...</Format>  
      ...  
</DataItem>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 允许值`Format`元素是 Microsoft Office Excel 格式和字符串*TrimRight*， *TrimLeft*， *TrimAll*，和*TrimNone*。 用于进行裁剪， *TrimRight*是默认设置。  
  
 此元素的值限定为下表中的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|任何 Excel 格式的字符串|根据指定的命名格式字符串或自定义格式字符串设置数据的格式。 可指定 Excel 支持的任何格式的字符串。|  
|*TrimAll*|对数据的左侧和右侧进行修整。|  
|*TrimLeft*|对数据的左侧进行修整。|  
|*TrimNone*|不修整数据。|  
|*TrimRight*|对数据的右侧进行修整。|  
  
 对应于的父元素`Format`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.DataItem>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  