---
title: OlapInfo 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e8c0cc23eb76d3da97aadbb9a1738580ebdbc62f
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34576779"
---
# <a name="olapinfo-element-xmla"></a>OlapInfo 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含所包含的轴和单元格元数据[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)用元素[MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)数据类型。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:mddataset">  
   ...  
   <OlapInfo>  
      <CubeInfo>...</CubeInfo>  
      <AxesInfo>...</AxesInfo>  
      <CellInfo>...</CellInfo>  
   </OlapInfo>  
   ...  
</root>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
|子元素|[AxesInfo](../../../analysis-services/xmla/xml-elements-properties/axesinfo-element-xmla.md)， [CellInfo](../../../analysis-services/xmla/xml-elements-properties/cellinfo-element-xmla.md)， [CubeInfo](../../../analysis-services/xmla/xml-elements-properties/cubeinfo-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 **OLAPInfo**部分**根**元素使用**MDDataSet**数据类型提供了有关多维数据集的元数据、 多维结果，和的属性的轴单元格包含结果。  
  
## <a name="see-also"></a>另请参阅
 [属性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
