---
title: FilterAxis 属性 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cellset::FilterAxis
- FilterAxis
helpviewer_keywords:
- FilterAxis property [ADO MD]
ms.assetid: 9c656963-531e-4cd1-b698-d5f42a9b7ba3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5015888cfafcce56c97f2369d418ed7be842dd28
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63295373"
---
# <a name="filteraxis-property-ado-md"></a>FilterAxis 属性 (ADO MD)
指示当前的筛选器信息[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)。  
  
## <a name="return-values"></a>返回值  
 返回[轴](../../../ado/reference/ado-md-api/axis-object-ado-md.md)对象，并是只读的。  
  
## <a name="remarks"></a>备注  
 使用**FilterAxis**属性返回用于对数据进行切片维度的信息。 [DimensionCount](../../../ado/reference/ado-md-api/dimensioncount-property-ado-md.md)的属性**轴**返回的切片器维度数。 此轴通常具有一个行。  
  
 **轴**返回的**FilterAxis**未包含在[轴](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)集合[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)对象。  
  
## <a name="applies-to"></a>适用范围  
 [单元集对象 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>请参阅  
 [轴对象 (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [维度对象 (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [DimensionCount 属性 (ADO MD)](../../../ado/reference/ado-md-api/dimensioncount-property-ado-md.md)
