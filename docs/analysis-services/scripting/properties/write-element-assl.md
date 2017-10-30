---
title: "写入元素 (ASSL) |Microsoft 文档"
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
- Write Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Write element
ms.assetid: d8f7a367-d7bf-4b40-acb4-19c8bc8c6c20
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d5f72e90c9975f0cf0dd1d16eeaabdb6eb378781
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="write-element-assl"></a>Write 元素 (ASSL)
  确定是否可以为编写数据或元数据给定[CubeDimensionPermission](../../../analysis-services/scripting/data-type/cubedimensionpermission-data-type-assl.md)或[权限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CubeDimensionPermission> <!-- or Permission -->  
   ...  
   <Write>...</Write>  
   ...  
</CubeDimensionPermission>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*无*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CubeDimensionPermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md)，[权限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*无*|不允许访问父对象的数据或元数据。|  
|*允许*|允许对父对象的数据和元数据进行写访问。|  
  
## <a name="remarks"></a>注释  
 对应的父级的元素**编写**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.CubeDimensionPermission>和<xref:Microsoft.AnalysisServices.Permission>。  
  
## <a name="see-also"></a>另请参阅  
 [多维数据集元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [维度元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

