---
title: DefaultMeasure 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DefaultMeasure Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DefaultMeasure
helpviewer_keywords:
- DefaultMeasure element
ms.assetid: ceac8b3d-ebae-463f-9e8c-506281d42792
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f6bb86737fb90fe63d162a421e8627b99a92228d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48087930"
---
# <a name="defaultmeasure-element-assl"></a>DefaultMeasure 元素 (ASSL)
  包含定义的默认度量值的多维表达式 (MDX) 表达式[多维数据集](../objects/cube-element-assl.md)或[角度来看](../objects/perspective-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Cube> <!-- or Perspective -->  
   ...  
   <DefaultMeasure>...</DefaultMeasure>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[多维数据集](../objects/cube-element-assl.md)，[透视](../objects/perspective-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 父级对应的元素`DefaultMeasure`在 Analysis Management Objects (AMO) 对象模型<xref:Microsoft.AnalysisServices.Cube>和<xref:Microsoft.AnalysisServices.Perspective>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
