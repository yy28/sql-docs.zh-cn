---
title: 单元格对象 (ADO MD) |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cell
helpviewer_keywords:
- Cell object [ADO MD]
ms.assetid: dcc2f044-b785-4a29-9bc5-b673f66eedf9
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1442261dbde0e6fa5acd2ffcfe702596688f0c0c
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="cell-object-ado-md"></a>单元格对象 (ADO MD)
表示包含在单元集中的轴坐标的交叉点处的数据。  
  
## <a name="remarks"></a>注释  
 A**单元格**会返回对象[项](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)属性[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)对象。  
  
 使用集合和属性的**单元格**对象，你可以执行以下操作：  
  
-   返回中的数据**单元格**与[值](../../../ado/reference/ado-md-api/value-property-ado-md.md)属性。  
  
-   返回表示的格式化的显示的字符串**值**具有属性[FormattedValue](../../../ado/reference/ado-md-api/formattedvalue-property-ado-md.md)属性。  
  
-   返回的序数值**单元格**内**单元集**与[序号](../../../ado/reference/ado-md-api/ordinal-property-ado-md-cell.md)属性。  
  
-   确定的位置**单元格**内[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)与[位置](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)集合。  
  
-   检索有关其他信息**单元格**用标准 ADO[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
 **属性**集合包含提供程序提供的属性。 下表列出可能可用的属性。 实际的属性列表可能不同根据提供程序的实现。 请参阅你的提供程序的更完整列表的可用属性的文档。  
  
|名称|Description|  
|----------|-----------------|  
|BackColor|显示该单元格时使用的背景色。|  
|FontFlags|位掩码细节效果字体。|  
|FontName|用于显示单元格的值的字体。|  
|FontSize|用于显示单元格的值的字体大小。|  
|ForeColor|显示该单元格时使用前景色。|  
|FormatString|格式化字符串中的值。|  
  
 本部分包含以下主题。  
  
-   [属性、 方法和事件](../../../ado/reference/ado-md-api/cell-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [轴示例 (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [单元集对象 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [位置集合 (ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
