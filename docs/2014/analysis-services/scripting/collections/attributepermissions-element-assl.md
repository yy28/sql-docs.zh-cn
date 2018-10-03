---
title: AttributePermissions 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AttributePermissions Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AttributePermissions
helpviewer_keywords:
- AttributePermissions element
ms.assetid: ac703177-5936-440e-b1a5-a254a89258bc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 00abbc7be0b8efa045074773ee6e2a3526192694
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227957"
---
# <a name="attributepermissions-element-assl"></a>AttributePermissions 元素 (ASSL)
  包含的属性权限的个人的集合[角色](../objects/role-element-assl.md)上的特定维度的元素[多维数据集](../objects/cube-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CubeDimensionPermission> <!-- or DimensionPermission -->  
   <AttributePermissions>  
      <AttributePermission>...</AttributePermission>  
      </AttributePermissions>  
</CubeDimensionPermission>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CubeDimensionPermission](../data-type/permission-data-type-assl.md)， [DimensionPermission](../objects/dimensionpermission-element-assl.md)|  
|子元素|[AttributePermission](../objects/attributepermission-element-assl.md)|  
  
## <a name="remarks"></a>备注  
 对于 `DimensionPermission`，此集合只可包含每个属性的一个 `AttributePermission`。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.AttributePermissionCollection>。  
  
## <a name="see-also"></a>请参阅  
 [Permission 数据类型&#40;ASSL&#41;](../data-type/permission-data-type-assl.md)   
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  
