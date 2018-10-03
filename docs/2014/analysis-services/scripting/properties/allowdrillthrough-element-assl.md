---
title: AllowDrillThrough 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AllowDrillThrough Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AllowDrillThrough
helpviewer_keywords:
- AllowDrillThrough element
ms.assetid: 53c9e4a3-a376-447d-a13f-80d845cc9789
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 79abc9833c111c472776d0713a0ca50888cae27d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48090847"
---
# <a name="allowdrillthrough-element-assl"></a>AllowDrillThrough 元素 (ASSL)
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
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|`False`|  
|基数|0-1：可选元素，只显示一次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningModel 元素](../objects/miningmodel-element-assl.md)， [MiningModelPermission](../objects/miningmodelpermission-element-assl.md)， [MiningStructurePermission](../objects/miningstructurepermission-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 父级对应的元素`AllowDrillThrough`在 Analysis Management Objects (AMO) 对象模型<xref:Microsoft.AnalysisServices.MiningModel>， <xref:Microsoft.AnalysisServices.MiningModelPermission>，和<xref:Microsoft.AnalysisServices.MiningStructurePermission>。  
  
## <a name="drillthrough-on-mining-structures"></a>对挖掘结构的钻取功能  
 在中[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，可以定义`AllowDrillthrough`为挖掘结构和挖掘模型的权限。 当将此权限分配给某个角色后，任一该角色的成员即可查询数据挖掘模型，然后返回未包含在该模型中的结构列。 例如，您创建了一个只使用客户键列、客户收入列和客户采购列的模型。 如果对该模型启用钻取功能，则用户可返回挖掘结构其他列中的信息，如客户电子邮件或客户名称。  
  
 因此，为了保护敏感数据，将列添加到挖掘结构时一定要谨慎。 另外，请仅在需要时才对某个结构授予 `AllowDrillthrough` 权限。  
  
 若要钻取到结构列，请使用具有以下形式之一的查询：  
  
 `SELECT * FROM <structure>.CASES`  
  
 或多个  
  
 `SELECT StructureColumn('<structure-column-name>') FROM <model>.CASES`  
  
## <a name="see-also"></a>请参阅  
 [Role 元素&#40;ASSL&#41;](../objects/role-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
