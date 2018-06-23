---
title: MiningModelPermissions 元素 (ASSL) |Microsoft 文档
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
- MiningModelPermissions Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningModelPermissions
helpviewer_keywords:
- MiningModelPermissions element
ms.assetid: 6cbcf029-9627-4839-9fc5-15e58e1ba0c3
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 701a5e139f3a5f2f98799be7dfc5f6dec1db3ced
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126178"
---
# <a name="miningmodelpermissions-element-assl"></a>MiningModelPermissions 元素 (ASSL)
  包含的有关权限的集合[MiningModel](../objects/miningmodel-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningModel>  
   ...  
   <MiningModelPermissions>  
      <MiningModelPermission xsi:type="Permission">...</MiningModelPermission>  
   </MiningModelPermissions>  
   ...  
</MiningModel>  
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
|父元素|[MiningModel](../objects/miningmodel-element-assl.md)|  
|子元素|[MiningModelPermission](../objects/miningmodelpermission-element-assl.md)类型的[权限](../data-type/permission-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.MiningModelPermissionCollection>。  
  
## <a name="see-also"></a>请参阅  
 [权限数据类型&#40;ASSL&#41;](../data-type/permission-data-type-assl.md)   
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  