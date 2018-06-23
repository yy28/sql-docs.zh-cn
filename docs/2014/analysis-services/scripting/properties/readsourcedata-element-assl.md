---
title: ReadSourceData 元素 (ASSL) |Microsoft 文档
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
- ReadSourceData Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ReadSourceData element
ms.assetid: 7da4665a-fba3-4aae-8dee-678dc14d3b05
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: dcbb6ce5b9cda3b17b69558cd60f6030f9e097b1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124425"
---
# <a name="readsourcedata-element-assl"></a>ReadSourceData 元素 (ASSL)
  确定如何唯一的名称中包含的层次结构生成[CubePermission](../objects/cubepermission-element-assl.md)。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CubePermission>  
   ...  
   <ReadSourceData>...</ReadSourceData>  
   ...  
</CubePermission>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*无*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CubePermission](../objects/cubepermission-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*无*|不允许访问计算传递 0 上可用的数据。|  
|*允许*|允许访问计算传递 0 上可用的数据。|  
  
## <a name="remarks"></a>Remarks  
 对应于的父元素`ReadSourceData`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.CubePermission>。  
  
## <a name="see-also"></a>请参阅  
 [多维数据集元素&#40;ASSL&#41;](../objects/cube-element-assl.md)   
 [维度元素&#40;ASSL&#41;](../objects/dimension-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  