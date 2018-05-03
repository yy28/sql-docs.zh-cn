---
title: FilterAxis 属性 (ADO MD) |Microsoft 文档
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
- Cellset::FilterAxis
- FilterAxis
helpviewer_keywords:
- FilterAxis property [ADO MD]
ms.assetid: 9c656963-531e-4cd1-b698-d5f42a9b7ba3
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 671a56b9117ea77b479d1a0fff78729ca9c3f5ab
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="filteraxis-property-ado-md"></a>FilterAxis 属性 (ADO MD)
指示当前的筛选器信息[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)。  
  
## <a name="return-values"></a>返回值  
 返回[轴](../../../ado/reference/ado-md-api/axis-object-ado-md.md)对象，并且是只读的。  
  
## <a name="remarks"></a>注释  
 使用**FilterAxis**属性以返回使用对数据进行切片的维度的信息。 [DimensionCount](../../../ado/reference/ado-md-api/dimensioncount-property-ado-md.md)属性**轴**返回切片器维度数。 此轴通常具有只在一行。  
  
 **轴**返回**FilterAxis**未包含在[轴](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)集合[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)对象。  
  
## <a name="applies-to"></a>适用范围  
 [单元集对象 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>另请参阅  
 [轴对象 (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [维度对象 (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [DimensionCount 属性 (ADO MD)](../../../ado/reference/ado-md-api/dimensioncount-property-ado-md.md)
