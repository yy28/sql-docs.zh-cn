---
title: "处理元素 (ASSL) |Microsoft 文档"
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
- Process Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Process
helpviewer_keywords:
- Process element
ms.assetid: 4aa08718-be44-4781-92cf-7b32b20f862c
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e208dcbd564db186af596132f0974e4e42789dd6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="process-element-assl"></a>Process 元素 (ASSL)
  确定用户是否可以处理父元素的所有者。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Permission> <-- or one of the other elements contained in the Element Relationships table -->  
   ...  
   <Process>...</Process>  
   ...  
</Permission>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|False|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md)， [DatabasePermission](../../../analysis-services/scripting/objects/databasepermission-element-assl.md)， [DimensionPermission](../../../analysis-services/scripting/objects/dimensionpermission-element-assl.md)， [MiningModelPermission](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md)， [MiningStructurePermission](../../../analysis-services/scripting/objects/miningstructurepermission-element-assl.md)，[权限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对应的父级的元素**过程**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.CubePermission>， <xref:Microsoft.AnalysisServices.DatabasePermission>， <xref:Microsoft.AnalysisServices.DimensionPermission>， <xref:Microsoft.AnalysisServices.MiningModelPermission>， <xref:Microsoft.AnalysisServices.MiningStructurePermission>，和<xref:Microsoft.AnalysisServices.Permission>。  
  
## <a name="see-also"></a>另请参阅  
 [Role 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
