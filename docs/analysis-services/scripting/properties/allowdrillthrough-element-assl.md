---
title: "AllowDrillThrough 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: AllowDrillThrough Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AllowDrillThrough
helpviewer_keywords: AllowDrillThrough element
ms.assetid: 53c9e4a3-a376-447d-a13f-80d845cc9789
caps.latest.revision: "51"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 273c96e4406af12582dd3a8a459573539a357736
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
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
 [Role 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
