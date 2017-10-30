---
title: "AttributePermissions 元素 (ASSL) |Microsoft 文档"
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
- AttributePermissions Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AttributePermissions
helpviewer_keywords:
- AttributePermissions element
ms.assetid: ac703177-5936-440e-b1a5-a254a89258bc
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ee64c8c31e07d7e210285ff956ed984a09dc124c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="attributepermissions-element-assl"></a>AttributePermissions 元素 (ASSL)
  包含单个属性权限的集合[角色](../../../analysis-services/scripting/objects/role-element-assl.md)元素上的特定维度[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CubeDimensionPermission> <!-- or DimensionPermission -->  
   <AttributePermissions>  
      <AttributePermission>...</AttributePermission>  
      </AttributePermissions>  
</CubeDimensionPermission>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CubeDimensionPermission](../../../analysis-services/scripting/data-type/cubedimensionpermission-data-type-assl.md)， [DimensionPermission](../../../analysis-services/scripting/objects/dimensionpermission-element-assl.md)|  
|子元素|[AttributePermission](../../../analysis-services/scripting/objects/attributepermission-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 有关**DimensionPermission**，此集合只能包含一个**AttributePermission**每个属性。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.AttributePermissionCollection>。  
  
## <a name="see-also"></a>另请参阅  
 [权限数据类型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)   
 [集合 & #40;ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  

