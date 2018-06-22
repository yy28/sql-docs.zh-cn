---
title: 表达式元素 (ASSL) |Microsoft 文档
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
- Expression Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Expression
helpviewer_keywords:
- Expression element
ms.assetid: a9491b21-5279-4531-b6a5-9e8022060dd8
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b56f4d09e59644b63d11c4becbb999f0536479d0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015340"
---
# <a name="expression-element-assl"></a>Expression 元素 (ASSL)
  包含定义父元素内容的多维表达式 (MDX)。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CellPermission> <!-- or StandardAction -->  
   ...  
   <Expression>...</Expression>  
   ...  
</CellPermission>  
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
|父元素|[CellPermission](../objects/cellpermission-element-assl.md)， [StandardAction](../data-type/action-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 有关`CellPermission`元素，`Expression`元素包含一个逻辑的 MDX 表达式，标识适用于由的权限的单元格[访问](access-element-assl.md)元素`CellPermission`元素。 如果 `Expression` 元素的 `CellPermission` 元素值为空，则将忽略 `CellPermission` 元素。  
  
 对于 `StandardAction` 元素，`Expression` 元素包含一个表示操作内容的 MDX 表达式。 如果 `Expression` 元素的 `StandardAction` 元素值为空，则将忽略 `StandardAction` 元素。  
  
 在 Analysis Management Objects (AMO) 对象模型中，与父级对应的元素为 <xref:Microsoft.AnalysisServices.CellPermission> 和 <xref:Microsoft.AnalysisServices.StandardAction>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  