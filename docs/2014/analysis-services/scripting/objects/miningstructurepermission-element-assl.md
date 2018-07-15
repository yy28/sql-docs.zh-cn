---
title: MiningStructurePermission 元素 (ASSL) |Microsoft Docs
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
- MiningStructurePermission Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningStructurePermission
helpviewer_keywords:
- MiningStructurePermission element
ms.assetid: 4ba2bfd2-9003-4eed-8049-a74d452894ea
caps.latest.revision: 43
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2f3789cd5b5b72048b9c9163c11bebf4fe5a77d5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37295487"
---
# <a name="miningstructurepermission-element-assl"></a>MiningStructurePermission 元素 (ASSL)
  定义的成员的权限[角色](role-element-assl.md)元素具有对单个[MiningStructure](miningstructure-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningStructurePermissions>  
   <MiningStructurePermission xsi:type="Permission">  
      <AllowDrillthrough>...</AllowDrillthrough>  
  
      <!-- This element also inherits all the child elements listed in Permission -->  
   </MiningStructurePermission>  
</MiningStructurePermissions>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|[权限](../data-type/permission-data-type-assl.md)|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningStructurePermissions](../collections/miningstructurepermissions-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.MiningStructurePermission>。  
  
 在中[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，该权限`AllowDrillthrough`已扩展为将应用于挖掘结构。 当向角色分配此权限时，任何作为该角色成员的用户均可使用以下语法直接查询挖掘结构：  
  
```  
SELECT <structure column list> FROM <structure>.CASES  
```  
  
 此外，如果对挖掘结构和挖掘模型均启用了 `AllowDrillthrough`，则用户可以使用下面的语法来查询未包含在挖掘模型中的结构列：  
  
```  
SELECT StructureColumn('<structure column name>' FROM <model>.CASES  
```  
  
 例如，创建使用客户密钥，客户的收入，只有列的模型和客户购买。 通过使用钻取，用户可返回未包含在挖掘模型中的其他结构列，如客户联系信息等。  
  
 因此，若要保护敏感数据或个人信息，应构造数据源视图来屏蔽个人信息，并且仅在需要时才授予针对结构的 `AllowDrillthrough` 权限。  
  
 有关详细信息，请参阅[钻取查询（数据挖掘）](../../data-mining/drillthrough-queries-data-mining.md)。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.AnalysisServices.MiningModel.AllowDrillThrough%2A>   
 <xref:Microsoft.AnalysisServices.AdomdClient.MiningModel.AllowDrillThrough%2A>   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
