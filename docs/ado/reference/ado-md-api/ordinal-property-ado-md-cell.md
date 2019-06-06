---
title: Ordinal 属性 （ADO MD 单元格） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cell::Ordinal
- Ordinal
helpviewer_keywords:
- Ordinal property [ADO MD]
ms.assetid: a6001168-b954-47f0-ba0d-c05c4cc40c58
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c4a40c59ad222c943cefe089ffaddd53f2cec25a
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66708812"
---
# <a name="ordinal-property-ado-md-cell"></a>Ordinal 属性（ADO MD 单元）
唯一标识[单元格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)按其单元集内的位置。  
  
## <a name="return-values"></a>返回值  
 返回**长**整数和是只读的。  
  
## <a name="remarks"></a>备注  
 单元格的序号值唯一地标识单元集内的单元格。 从概念上讲，单元格，像在单元集中进行编号在单元集中*p*-维数组，其中*p*是数[轴](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)。 从零行优先顺序开始编号的单元格。 下面是用于计算单元格的序号的公式：  
  
 单元格的序号值可用于[项](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)的属性[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)对象，以快速检索[单元格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)。  
  
## <a name="applies-to"></a>适用范围  
 [单元对象 (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)  
  
## <a name="see-also"></a>请参阅  
 [轴示例 (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [单元集对象 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [Item 属性 （ADO MD 单元集）](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)   
 [Ordinal 属性（ADO MD 位置）](../../../ado/reference/ado-md-api/ordinal-property-ado-md-position.md)
