---
title: 读取元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 5742e7708158bfb703a5e4de8abcffd52dea67f3
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="read-element-assl"></a>Read 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  确定是否可以为读取数据或元数据给定[CubeDimensionPermission](../../../analysis-services/scripting/data-type/cubedimensionpermission-data-type-assl.md)或[权限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CubeDimensionPermission> <!-- or Permission -->  
   ...  
   <Read>...</Read>  
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
  
## <a name="remarks"></a>備註  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*无*|不允许访问父对象的数据或元数据。|  
|*允许*|允许对父对象的数据和元数据进行读取访问。|  
  
## <a name="remarks"></a>注释  
 对应的父级的元素**读取**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.CubeDimensionPermission>和<xref:Microsoft.AnalysisServices.Permission>。  
  
## <a name="see-also"></a>另请参阅  
 [多维数据集元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [维度元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [CubePermission 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/cubepermission-element-assl.md)   
 [权限数据类型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
