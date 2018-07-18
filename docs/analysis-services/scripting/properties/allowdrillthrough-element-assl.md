---
title: AllowDrillThrough 元素 (ASSL) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 25bad363975494fc8bd6c8cb343a165d8bb85f85
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34036008"
---
# <a name="allowdrillthrough-element-assl"></a>AllowDrillThrough 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  确定是否允许在父元素上执行钻取操作。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningModel> <!-- or MiningModelPermission -->  
<!-- or MiningStructurePermission -->   ...  
   <AllowDrillThrough>...</AllowDrillThrough>  
   ...  
</MiningModel>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|**False**|  
|基数|0-1：可选元素，只显示一次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningModel 元素](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)， [MiningModelPermission](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md)， [MiningStructurePermission](../../../analysis-services/scripting/objects/miningstructurepermission-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对应的父级的元素**AllowDrillThrough**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.MiningModel>， <xref:Microsoft.AnalysisServices.MiningModelPermission>，和<xref:Microsoft.AnalysisServices.MiningStructurePermission>。  
  
## <a name="drillthrough-on-mining-structures"></a>对挖掘结构的钻取功能  
 在[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，你可以定义**AllowDrillthrough**为挖掘结构和挖掘模型的权限。 当将此权限分配给某个角色后，任一该角色的成员即可查询数据挖掘模型，然后返回未包含在该模型中的结构列。 例如，您创建了一个只使用客户键列、客户收入列和客户采购列的模型。 如果对该模型启用钻取功能，则用户可返回挖掘结构其他列中的信息，如客户电子邮件或客户名称。  
  
 因此，为了保护敏感数据，将列添加到挖掘结构时一定要谨慎。 另外，请仅在需要时才对某个结构授予 **AllowDrillthrough** 权限。  
  
 若要钻取到结构列，请使用具有以下形式之一的查询：  
  
 `SELECT * FROM <structure>.CASES`  
  
 或  
  
 `SELECT StructureColumn('<structure-column-name>') FROM <model>.CASES`  
  
## <a name="see-also"></a>另请参阅  
 [Role 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
