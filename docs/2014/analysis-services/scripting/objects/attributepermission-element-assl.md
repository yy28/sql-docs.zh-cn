---
title: AttributePermission 元素 (ASSL) |Microsoft 文档
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
- AttributePermission Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AttributePermission
helpviewer_keywords:
- AttributePermission element
ms.assetid: efc8aa63-3959-4b2e-98f8-2a9c424298c2
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5ee5d846cdf849959bc1a916dd82fd95de60e6e8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026876"
---
# <a name="attributepermission-element-assl"></a>AttributePermission 元素 (ASSL)
  定义的权限的成员[角色](role-element-assl.md)元素对中的各个维度的特性[多维数据集](cube-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AttributePermissions>  
   <AttributePermission>  
      <AttributeID>...</AttributeID>  
      <Description>...</Description>  
      <DefaultMember>...</DefaultMember>  
            <VisualTotals>...</VisualTotals>  
      <AllowedSet>...</AllowedSet>  
            <DeniedSet>...</DeniedSet>  
      <Annotations>...</Annotations>  
   </AttributePermission>  
</AttributePermissions>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AttributePermissions](../collections/attributepermissions-element-assl.md)|  
|子元素|[AllowedSet](../properties/allowedset-element-assl.md)，[批注](../collections/annotations-element-assl.md)， [AttributeID](../properties/id-element-assl.md)， [DefaultMember](member-element-assl.md)， [DeniedSet](../properties/deniedset-element-assl.md)，[说明](../properties/description-element-assl.md)， [VisualTotals](../properties/visualtotals-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.AttributePermission>。  
  
## <a name="see-also"></a>请参阅  
 [CubeDimensionPermission 数据类型&#40;ASSL&#41;](../data-type/permission-data-type-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  