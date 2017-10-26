---
title: "MiningStructurePermission 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MiningStructurePermission Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MiningStructurePermission
helpviewer_keywords:
- MiningStructurePermission element
ms.assetid: 4ba2bfd2-9003-4eed-8049-a74d452894ea
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 22713569509019e9d0aac30f82c898c73a034fda
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="miningstructurepermission-element-assl"></a>MiningStructurePermission 元素 (ASSL)
  定义的权限的成员[角色](../../../analysis-services/scripting/objects/role-element-assl.md)元素具有对单个[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)元素。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|[权限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[添加](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.MiningStructurePermission>。  
  
 在[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，权限**AllowDrillthrough**已扩展为适用于挖掘结构。 当向角色分配此权限时，任何作为该角色成员的用户均可使用以下语法直接查询挖掘结构：  
  
```  
SELECT <structure column list> FROM <structure>.CASES  
```  
  
 此外，如果**AllowDrillthrough**启用在挖掘结构和挖掘模型中，用户可以查询通过使用以下语法未包含在挖掘模型的结构列：  
  
```  
SELECT StructureColumn('<structure column name>' FROM <model>.CASES  
```  
  
 例如，创建使用客户键客户收入，只有列的模型和客户购买。 通过使用钻取，用户可返回未包含在挖掘模型中的其他结构列，如客户联系信息等。  
  
 因此，为了保护敏感数据或个人信息，你应该构建你的数据源视图来屏蔽个人信息，并授予**AllowDrillthrough**权限仅在必要时的结构。  
  
 有关详细信息，请参阅[钻取查询（数据挖掘）](../../../analysis-services/data-mining/drillthrough-queries-data-mining.md)。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.AnalysisServices.MiningModel.AllowDrillThrough%2A>   
 <xref:Microsoft.AnalysisServices.AdomdClient.MiningModel.AllowDrillThrough%2A>   
 [对象 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

