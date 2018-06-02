---
title: 多维数据集元素 (OlapInfo) (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 579d36c96efcc4084f725d39c2af3cdddecd98d1
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34574889"
---
# <a name="cube-element-olapinfo-xmla"></a>Cube 元素 (OlapInfo) (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含父级的多维数据集信息[CubeInfo](../../../analysis-services/xmla/xml-elements-properties/cubeinfo-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CubeInfo>  
   <Cube>  
      <CubeName>...</CubeName>  
      <LastDataUpdate>...</LastDataUpdate>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
   </Cube>  
   ...  
</CubeInfo>  
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
|父元素|[CubeInfo](../../../analysis-services/xmla/xml-elements-properties/cubeinfo-element-xmla.md)|  
|子元素|[多维数据集名称](../../../analysis-services/xmla/xml-elements-properties/cubename-element-xmla.md)， [LastDataUpdate](../../../analysis-services/xmla/xml-elements-properties/lastdataupdate-element-xmla.md)， [LastSchemaUpdate](../../../analysis-services/xmla/xml-elements-properties/lastschemaupdate-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>另请参阅
 [属性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
