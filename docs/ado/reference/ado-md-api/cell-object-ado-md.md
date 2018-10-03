---
title: 单元对象 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cell
helpviewer_keywords:
- Cell object [ADO MD]
ms.assetid: dcc2f044-b785-4a29-9bc5-b673f66eedf9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: df7b93e00ddff15c320152e3fa2bc1f104caa3a4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47612512"
---
# <a name="cell-object-ado-md"></a>单元对象 (ADO MD)
表示单元集内包含的轴坐标相交处的数据。  
  
## <a name="remarks"></a>备注  
 一个**单元格**对象返回的[项](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)属性[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)对象。  
  
 使用集合和属性的**单元格**对象，您可以执行以下操作：  
  
-   返回中的数据**单元格**与[值](../../../ado/reference/ado-md-api/value-property-ado-md.md)属性。  
  
-   返回表示格式化的显示的字符串**值**具有属性[FormattedValue](../../../ado/reference/ado-md-api/formattedvalue-property-ado-md.md)属性。  
  
-   返回的序数值**单元格**内**单元集**与[序号](../../../ado/reference/ado-md-api/ordinal-property-ado-md-cell.md)属性。  
  
-   确定的位置**单元格**内[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)与[位置](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)集合。  
  
-   有关检索其他信息**单元格**与标准的 ADO[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
 **属性**集合包含提供程序提供的属性。 下表列出了可能可用的属性。 实际的属性列表可能不同的提供程序实现根据。 请参阅可用属性的更完整的列表为提供程序的文档。  
  
|“属性”|Description|  
|----------|-----------------|  
|BackColor|显示该单元格时使用的背景色。|  
|FontFlags|位掩码细节效果字体。|  
|FontName|用于显示单元格的值的字体。|  
|FontSize|用于显示单元格的值的字体大小。|  
|ForeColor|显示该单元格时使用前景色。|  
|FormatString|带格式字符串中的值。|  
  
 本部分包含以下主题。  
  
-   [属性、 方法和事件](../../../ado/reference/ado-md-api/cell-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [轴示例 (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [单元集对象 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [Positions 集合 (ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
