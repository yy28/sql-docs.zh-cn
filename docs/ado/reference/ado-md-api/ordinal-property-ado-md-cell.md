---
title: "序号属性 （ADO MD 单元格） |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Cell::Ordinal
- Ordinal
helpviewer_keywords:
- Ordinal property [ADO MD]
ms.assetid: a6001168-b954-47f0-ba0d-c05c4cc40c58
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b6928eeeb7450b2edbd244d70d3c6a8aa999343a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="ordinal-property-ado-md-cell"></a>序号属性 （ADO MD 单元格）
唯一标识[单元格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)按集中的单元格其位置。  
  
## <a name="return-values"></a>返回值  
 返回**长**整数并且是只读的。  
  
## <a name="remarks"></a>注释  
 该单元格的序号值唯一标识集中的单元格的单元格。 从概念上讲，单元格，好像单元集进行编号在单元集中*p*-维数组，其中*p*是数[轴](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)。 从零行优先顺序从开始编号单元格。 下面是用于计算的单元格序号的公式：  
  
 该单元格的序号值可与[项](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)属性[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)对象快速检索[单元格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)。  
  
## <a name="applies-to"></a>适用范围  
 [单元格对象 (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)  
  
## <a name="see-also"></a>另请参阅  
 [轴示例 (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [单元集对象 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [Item 属性 （ADO MD 单元集）](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)   
 [序号属性 （ADO MD 位置）](../../../ado/reference/ado-md-api/ordinal-property-ado-md-position.md)

