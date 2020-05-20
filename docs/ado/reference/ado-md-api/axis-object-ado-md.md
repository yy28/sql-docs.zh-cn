---
title: Axis 对象（ADO MD） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Axis
helpviewer_keywords:
- Axis object [ADO MD]
ms.assetid: 5f498c9a-b1e7-4e6e-9ae6-71eadaf9aada
author: rothja
ms.author: jroth
ms.openlocfilehash: c251355637c5d57729a7d4aa737f2face1c9ace2
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82765178"
---
# <a name="axis-object-ado-md"></a>轴对象 (ADO MD)
表示单元集的位置或筛选轴，其中包含一个或多个维度的选定成员。  
  
## <a name="remarks"></a>备注  
 Axis 对象可以包含**Axis** [集合，](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)或由[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)的[FilterAxis](../../../ado/reference/ado-md-api/filteraxis-property-ado-md.md)属性返回。  
  
 使用**Axis**对象的集合和属性，可以执行以下操作：  
  
-   标识具有[Name](../../../ado/reference/ado-md-api/name-property-ado-md.md)属性的**轴**。  
  
-   使用[position](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)集合循环访问**轴**上的每个位置。  
  
-   通过[DimensionCount](../../../ado/reference/ado-md-api/dimensioncount-property-ado-md.md)属性获取**轴**上的维度数。  
  
-   获取具有标准 ADO[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合的**轴**特定于提供程序的属性。  
  
 本部分包含以下主题。  
  
-   [属性、方法和事件](../../../ado/reference/ado-md-api/axis-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [轴示例（VBScript）](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [轴集合（ADO MD）](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)   
 [位置集合（ADO MD）](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
