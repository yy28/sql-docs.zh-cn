---
title: FilterAxis 属性（ADO MD） |Microsoft Docs
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
ms.openlocfilehash: d44ac908c04338f80c18699319f75a068370c3e0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67938456"
---
# <a name="filteraxis-property-ado-md"></a>FilterAxis 属性 (ADO MD)
指示有关当前[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)的筛选器信息。  
  
## <a name="return-values"></a>返回值  
 返回一个[轴](../../../ado/reference/ado-md-api/axis-object-ado-md.md)对象，它是只读的。  
  
## <a name="remarks"></a>备注  
 使用**FilterAxis**属性可以返回有关用于切分数据的维度的信息。 **轴**的[DimensionCount](../../../ado/reference/ado-md-api/dimensioncount-property-ado-md.md)属性返回切片器维度数。 此轴通常只包含一行。  
  
 [单元格](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)集对象的[轴](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)集合中不包含**FilterAxis**返回的**轴**。  
  
## <a name="applies-to"></a>应用于  
 [单元集对象 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>另请参阅  
 [Axis 对象（ADO MD）](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [Dimension 对象（ADO MD）](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [DimensionCount 属性 (ADO MD)](../../../ado/reference/ado-md-api/dimensioncount-property-ado-md.md)
