---
title: CellData 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 571aa0b0d95ff4b3c9f15acb9808fde4cd78c0a1
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="celldata-element-xmla"></a>CellData 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含表示包含的单元格数据的单元格元素的集合[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)用元素[MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)数据类型。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:mddataset">  
   ...  
   <CellData>  
      <Cell>...</Cell>  
   </CellData>  
</root>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
|子元素|[单元格](../../../analysis-services/xmla/xml-elements-properties/cell-element-mddataset-xmla.md)|  
  
## <a name="remarks"></a>注释  
 在父根元素中，**轴**元素后跟**CellData**元素的一个集合**单元格**包含的每个单元格的单元格属性值的元素返回在多维数据集中。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
