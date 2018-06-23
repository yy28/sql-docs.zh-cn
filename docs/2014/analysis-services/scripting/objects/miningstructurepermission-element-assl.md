---
title: MiningStructurePermission 元素 (ASSL) |Microsoft 文档
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
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0c74423bfbf199825dc707d80e21c5b5a4555cc8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028447"
---
# <a name="miningstructurepermission-element-assl"></a>MiningStructurePermission 元素 (ASSL)
  定义的权限的成员[角色](role-element-assl.md)元素具有对单个[MiningStructure](miningstructure-element-assl.md)元素。  
  
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
|父元素|[添加](../collections/miningstructurepermissions-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.MiningStructurePermission>。  
  
 在[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，权限`AllowDrillthrough`已扩展为适用于挖掘结构。 当向角色分配此权限时，任何作为该角色成员的用户均可使用以下语法直接查询挖掘结构：  
  
```  
SELECT <structure column list> FROM <structure>.CASES  
```  
  
 此外，如果对挖掘结构和挖掘模型均启用了 `AllowDrillthrough`，则用户可以使用下面的语法来查询未包含在挖掘模型中的结构列：  
  
```  
SELECT StructureColumn('<structure column name>' FROM <model>.CASES  
```  
  
 例如，创建使用客户键客户收入，只有列的模型和客户购买。 通过使用钻取，用户可返回未包含在挖掘模型中的其他结构列，如客户联系信息等。  
  
 因此，若要保护敏感数据或个人信息，应构造数据源视图来屏蔽个人信息，并且仅在需要时才授予针对结构的 `AllowDrillthrough` 权限。  
  
 有关详细信息，请参阅[钻取查询（数据挖掘）](../../data-mining/drillthrough-queries-data-mining.md)。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.AnalysisServices.MiningModel.AllowDrillThrough%2A>   
 <xref:Microsoft.AnalysisServices.AdomdClient.MiningModel.AllowDrillThrough%2A>   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  