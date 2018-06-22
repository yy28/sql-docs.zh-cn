---
title: 多维数据集元素 (XMLA) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Cube Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.cube
- urn:schemas-microsoft-com:xml-analysis#Cube
- http://schemas.microsoft.com/analysisservices/2003/engine#Cube
helpviewer_keywords:
- Cube element
ms.assetid: 2e8662f4-fb2e-43af-b70a-9e0b5872c9b9
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 3627c62dd8277ff0c86d66f453afd66ad01005c7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016193"
---
# <a name="cube-element-xmla"></a>Cube 元素 (XMLA)
  标识包含由父维度的多维数据集[对象](object-element-dimension-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Object>  
   ...  
   <Cube>...</Cube>  
   ...  
</Object>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[对象](object-element-dimension-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Cube` 元素是包含多维数据集名称的对象标识符，该多维数据集包含由 `Object` 元素表示的维度。  
  
## <a name="see-also"></a>请参阅  
 [数据库元素&#40;XMLA&#41;](database-element-xmla.md)   
 [维度元素&#40;XMLA&#41;](dimension-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  