---
title: AttributePermission 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1da791fae7c8b802c8de0642f25025fe311155d4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48074758"
---
# <a name="attributepermission-element-assl"></a>AttributePermission 元素 (ASSL)
  定义的成员的权限[角色](role-element-assl.md)中的单个维度的属性元素具有[多维数据集](cube-element-assl.md)元素。  
  
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
|数据类型和长度|None|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AttributePermissions](../collections/attributepermissions-element-assl.md)|  
|子元素|[AllowedSet](../properties/allowedset-element-assl.md)，[批注](../collections/annotations-element-assl.md)， [AttributeID](../properties/id-element-assl.md)， [DefaultMember](member-element-assl.md)， [DeniedSet](../properties/deniedset-element-assl.md)，[说明](../properties/description-element-assl.md)， [VisualTotals](../properties/visualtotals-element-assl.md)|  
  
## <a name="remarks"></a>备注  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.AttributePermission>。  
  
## <a name="see-also"></a>请参阅  
 [CubeDimensionPermission 数据类型&#40;ASSL&#41;](../data-type/permission-data-type-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
