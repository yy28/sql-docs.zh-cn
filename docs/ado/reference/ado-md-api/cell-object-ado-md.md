---
title: Cell Object （ADO MD） |Microsoft Docs
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
ms.openlocfilehash: bbf97a4095f2295b8851f87ba20ab083938e70ed
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67947748"
---
# <a name="cell-object-ado-md"></a>单元对象 (ADO MD)
表示单元集内包含的轴坐标相交处的数据。  
  
## <a name="remarks"></a>备注  
 单元[集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)对象的[Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)属性返回**Cell**对象。  
  
 使用**Cell**对象的集合和属性，可以执行以下操作：  
  
-   返回具有[值](../../../ado/reference/ado-md-api/value-property-ado-md.md)属性的**单元**中的数据。  
  
-   返回一个字符串，该字符串表示带有[FormattedValue](../../../ado/reference/ado-md-api/formattedvalue-property-ado-md.md)属性的**Value**属性的格式显示。  
  
-   返回单元**集**内具有[Ordinal](../../../ado/reference/ado-md-api/ordinal-property-ado-md-cell.md)属性的**单元**的序号值。  
  
-   确定[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)中**单元格**在[位置](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)集合中的位置。  
  
-   检索有关具有标准 ADO[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合的**单元**的其他信息。  
  
 **Properties**集合包含提供程序提供的属性。 下表列出了可用的属性。 实际属性列表可能有所不同，具体取决于提供程序的实现。 有关可用属性的更完整列表，请参阅提供程序的文档。  
  
|名称|说明|  
|----------|-----------------|  
|BackColor|显示单元格时使用的背景色。|  
|FontFlags|字体上的位掩码细节效果。|  
|FontName|用于显示单元值的字体。|  
|FontSize|用于显示单元值的字号。|  
|ForeColor|显示单元格时使用的前景色。|  
|FormatString|带格式的字符串中的值。|  
  
 本部分包含以下主题。  
  
-   [属性、方法和事件](../../../ado/reference/ado-md-api/cell-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [轴示例（VBScript）](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [单元集对象（ADO MD）](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [位置集合（ADO MD）](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
