---
title: 添加元素 (ASSL) |Microsoft 文档
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
- MiningStructurePermissions Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningStructurePermissions
helpviewer_keywords:
- MiningStructurePermissions element
ms.assetid: 4db9a9b2-8525-441f-a202-fd253282f540
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: a4771102a81dfae1e4a0e62ea1527a5ad6d19199
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025812"
---
# <a name="miningstructurepermissions-element-assl"></a>MiningStructurePermissions 元素 (ASSL)
  包含的权限的集合上[MiningStructure](../objects/miningstructure-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningStructure>  
   ...  
   <MiningStructurePermissions>  
      <MiningStructurePermission xsi:type="Permission">...</MiningStructurePermission>  
   </MiningStructurePermissions>  
   ...  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningStructure](../objects/miningstructure-element-assl.md)|  
|子元素|[MiningStructurePermission](../objects/miningstructurepermission-element-assl.md)类型的[权限](../data-type/permission-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.MiningStructurePermissionCollection>。  
  
## <a name="see-also"></a>请参阅  
 [权限数据类型&#40;ASSL&#41;](../data-type/permission-data-type-assl.md)   
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  