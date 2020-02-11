---
title: 轴集合（ADO MD） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Axes
- Cellset::Axes
helpviewer_keywords:
- Axes collection [ADO MD]
ms.assetid: 072fb21a-ec0f-4b02-9022-1cef3ad4bfff
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6c06faf6327d60be823ce9d99215655b5badf5e3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67947408"
---
# <a name="axes-collection-ado-md"></a>轴集合 (ADO MD)
包含定义单元集的[轴](../../../ado/reference/ado-md-api/axis-object-ado-md.md)对象。  
  
## <a name="remarks"></a>备注  
 [单元格集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)对象包含一个**轴**集合。 打开**单元集**后，此集合将至少包含一个**轴**。 有关如何使用**轴**对象的更详细说明，请参阅[axis](../../../ado/reference/ado-md-api/axis-object-ado-md.md)对象。  
  
> [!NOTE]
>  **单元集**的筛选轴不包含在**轴**集合中。 有关详细信息，请参阅[FilterAxis](../../../ado/reference/ado-md-api/filteraxis-property-ado-md.md)属性。  
  
 **轴**是标准 ADO 集合。 通过集合的属性和方法，你可以执行以下操作：  
  
-   获取集合中具有[Count](../../../ado/reference/ado-api/count-property-ado.md)属性的对象的数目。  
  
-   返回集合中具有默认[项](../../../ado/reference/ado-api/item-property-ado.md)属性的对象。  
  
-   用[Refresh](../../../ado/reference/ado-api/refresh-method-ado.md)方法更新集合中的对象。  
  
 本部分包含以下主题。  
  
-   [属性、方法和事件](../../../ado/reference/ado-md-api/axes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [单元集示例（VB）](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [轴对象 (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)
