---
title: CellData 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CellData Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CellData
- http://schemas.microsoft.com/analysisservices/2003/engine#CellData
- urn:schemas-microsoft-com:xml-analysis#CellData
- microsoft.xml.analysis.celldata
helpviewer_keywords:
- CellData element
ms.assetid: 0ebfb5e1-a674-4b9b-bd8c-c529da105f61
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4ca9810ece8670c2072674b16e58d996973913a1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079867"
---
# <a name="celldata-element-xmla"></a>CellData 元素 (XMLA)
  包含一系列表示包含的单元格数据的单元格元素[根](root-element-xmla.md)使用的元素[MDDataSet](../xml-data-types/mddataset-data-type-xmla.md)数据类型。  
  
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
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[根](root-element-xmla.md)|  
|子元素|[单元格](cell-element-mddataset-xmla.md)|  
  
## <a name="remarks"></a>备注  
 在父级 root 元素中，`Axes` 元素后跟 `CellData` 元素，后者是 `Cell` 元素的集合，这些 Cell 元素包含了多维数据集中返回的每个单元的单元属性值。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
