---
title: 成员集合 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level::Members
- Members
- Position::Members
helpviewer_keywords:
- Members collection [ADO MD]
ms.assetid: 3a647cde-efdc-4394-b1b9-8cbb1b9d689f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 541e1098dfd18210e7c07a0718ecd3add758c8a4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62659560"
---
# <a name="members-collection-ado-md"></a>成员集合 (ADO MD)
包含[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)对象从一个级别或沿某个轴的位置。  
  
## <a name="remarks"></a>备注  
 一个**成员**集合用于包含以下类型的成员：  
  
-   构成了在多维数据集级别的成员。 这些批注包含在**成员**系列[级别](../../../ado/reference/ado-md-api/level-object-ado-md.md)对象。 例如，使用从示例[概述的多维架构和数据](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)，国家/地区级别的四个成员为加拿大、 美国、 英国、 德国。  
  
-   成员的子节点的层次结构中的特定成员。 这些成员返回的[子级](../../../ado/reference/ado-md-api/children-property-ado-md.md)的父对象**成员**对象。 例如，再次使用相同的示例，两个子代的 Canada 成员是加拿大东部和加拿大西部。  
  
-   定义沿某个轴的特定位置的成员[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)。 使用从 cellset[处理多维数据](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)作为示例，在 x 轴上的第一个位置的两个成员是情人节和西雅图。 这些成员所包含的**成员**系列[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)对象。  
  
 **成员**是一个标准 ADO 集合。 使用的属性和方法的集合，可以执行以下操作：  
  
-   获取与集合中的对象数[计数](../../../ado/reference/ado-api/count-property-ado.md)属性。  
  
-   具有默认值的集合中返回的对象[项](../../../ado/reference/ado-api/item-property-ado.md)属性。  
  
-   更新的提供程序从集合中的对象[刷新](../../../ado/reference/ado-api/refresh-method-ado.md)方法。  
  
 本部分包含以下主题。  
  
-   [属性、 方法和事件](../../../ado/reference/ado-md-api/members-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [成员示例 (VBScript)](../../../ado/reference/ado-md-api/members-example-vbscript.md)   
 [成员对象 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)
