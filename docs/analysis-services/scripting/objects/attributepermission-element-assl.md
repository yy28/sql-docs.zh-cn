---
title: AttributePermission 元素 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 09002c565cb9c4d385a42fcc3969ac28f458ed6e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34033658"
---
# <a name="attributepermission-element-assl"></a>AttributePermission 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义的权限的成员[角色](../../../analysis-services/scripting/objects/role-element-assl.md)元素对中的各个维度的特性[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)元素。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AttributePermissions](../../../analysis-services/scripting/collections/attributepermissions-element-assl.md)|  
|子元素|[AllowedSet](../../../analysis-services/scripting/properties/allowedset-element-assl.md)，[批注](../../../analysis-services/scripting/collections/annotations-element-assl.md)， [AttributeID](../../../analysis-services/scripting/properties/attributeid-element-assl.md)， [DefaultMember](../../../analysis-services/scripting/properties/defaultmember-element-assl.md)， [DeniedSet](../../../analysis-services/scripting/properties/deniedset-element-assl.md)，[说明](../../../analysis-services/scripting/properties/description-element-assl.md)， [VisualTotals](../../../analysis-services/scripting/properties/visualtotals-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.AttributePermission>。  
  
## <a name="see-also"></a>另请参阅  
 [CubeDimensionPermission 数据类型&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/cubedimensionpermission-data-type-assl.md)   
 [对象 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
