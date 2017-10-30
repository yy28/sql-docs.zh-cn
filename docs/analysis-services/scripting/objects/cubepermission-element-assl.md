---
title: "CubePermission 元素 (ASSL) |Microsoft 文档"
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
- CubePermission Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- CubePermission
helpviewer_keywords:
- CubePermission element
ms.assetid: b144b623-ff20-4ead-91ad-4c718f3b140b
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6db733a91b405ef5eed6a6dd5a5a7f977aa33266
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="cubepermission-element-assl"></a>CubePermission 元素 (ASSL)
  定义的特定成员的权限[角色](../../../analysis-services/scripting/objects/role-element-assl.md)中特定元素[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CubePermissions>  
   <CubePermission>  
      <!-- The following elements extend Permission -->  
      <ReadSourceData>...</ReadSourceData>  
            <DimensionPermissions>...</DimensionPermissions>  
            <CellPermissions>...</CellPermissions>  
   </CubePermission>  
</CubePermissions>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|[权限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|默认值|无|  
|基数|0-n：可出现一次或多次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CubePermissions](../../../analysis-services/scripting/collections/cubepermissions-element-assl.md)|  
|子元素|[CellPermissions](../../../analysis-services/scripting/collections/cellpermissions-element-assl.md)， [DimensionPermissions](../../../analysis-services/scripting/collections/dimensionpermissions-element-assl.md)， [ReadSourceData](../../../analysis-services/scripting/properties/readsourcedata-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.CubePermission>。  
  
## <a name="see-also"></a>另请参阅  
 [多维数据集元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [对象 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

