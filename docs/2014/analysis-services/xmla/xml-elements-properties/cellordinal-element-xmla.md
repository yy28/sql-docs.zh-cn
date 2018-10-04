---
title: CellOrdinal 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CellOrdinal Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.cellordinal
- urn:schemas-microsoft-com:xml-analysis#CellOrdinal
- http://schemas.microsoft.com/analysisservices/2003/engine#CellOrdinal
helpviewer_keywords:
- CellOrdinal element
ms.assetid: 1808c498-e3b4-4e5c-9e22-7f8662d32874
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7c1c46936acfe909f3655b09737bb595bebb6b22
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48133467"
---
# <a name="cellordinal-element-xmla"></a>CellOrdinal 元素 (XMLA)
  包含要更新的单元格的多维数据集中的序号位置[UpdateCells](../xml-elements-commands/updatecells-element-xmla.md)命令。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Cell>  
   ...  
   <CellOrdinal>...</CellOrdinal>  
   ...  
</Cell>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Long|  
|默认值|None|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[单元格](cell-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 `CellOrdinal` 元素标识 `UpdateCells` 命令所要更新的单元。  
  
 有关更新单元的详细信息，请参阅[更新单元 (XMLA)](../../multidimensional-models-scripting-language-assl-xmla/updating-cells-xmla.md)。  
  
## <a name="see-also"></a>请参阅  
 [值元素&#40;XMLA&#41;](value-element-xmla.md)   
 [UpdateCells 元素&#40;XMLA&#41;](../xml-elements-commands/updatecells-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
