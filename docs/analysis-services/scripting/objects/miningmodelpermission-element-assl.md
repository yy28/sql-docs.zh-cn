---
title: MiningModelPermission 元素 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6f05a12d5be30826e5a826320f2eb5a6c604456e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="miningmodelpermission-element-assl"></a>MiningModelPermission 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义的权限成员[角色](../../../analysis-services/scripting/objects/role-element-assl.md)元素具有对单个[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningModelPermissions>  
   <MiningModelPermission xsi:type="Permission">  
      <!-- The following elements extend Permission -->  
      <AllowDrillThrough>...</AllowDrillThrough>  
      <AllowBrowsing>...</AllowBrowsing>  
   </MiningModelPermission>  
</MiningModelPermissions>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|[权限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningModelPermissions](../../../analysis-services/scripting/collections/miningmodelpermissions-element-assl.md)|  
|子元素|[AllowBrowsing](../../../analysis-services/scripting/properties/allowbrowsing-element-assl.md)， [AllowDrillThrough](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 在[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，你可以通过添加启用对挖掘结构的钻取**AllowDrillthrough**权限[添加](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md)集合。 如果**AllowDrillthrough**挖掘结构和挖掘模型，任何成员具有的角色上启用[AllowDrillThrough 元素&#40;ASSL&#41; ](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md)对模型的权限可以查询数据挖掘模型，并返回结构列不包含在模型中，通过使用以下语法：  
  
```  
SELECT StructureColumn('<column name>') FROM <model>.CASES  
```  
  
 因此，为了保护敏感数据或个人信息，应该仅在需要时才授予对挖掘模型的 **AllowDrillthrough** 权限。 有关详细信息，请参阅[AllowDrillThrough 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md)。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.MiningModelPermission>。  
  
## <a name="see-also"></a>另请参阅  
 [对象 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
