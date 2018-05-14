---
title: CellOrdinal 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ba1734e3df9689f6aeb06db9b26df032483c57a5
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="cellordinal-element-xmla"></a>CellOrdinal 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含要更新的单元格多维数据集中的序号位置[UpdateCells](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)命令。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Cell>  
   ...  
   <CellOrdinal>...</CellOrdinal>  
   ...  
</Cell>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Long|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[单元格](../../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **CellOrdinal**元素标识要更新的单元格**UpdateCells**命令。  
  
 有关更新单元的详细信息，请参阅[更新单元 (XMLA)](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/updating-cells-xmla.md)。  
  
## <a name="see-also"></a>另请参阅  
 [值元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/value-element-xmla.md)   
 [UpdateCells 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)   
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
