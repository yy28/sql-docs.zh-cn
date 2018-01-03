---
title: "Members 集合 (ADO MD) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Level::Members
- Members
- Position::Members
helpviewer_keywords: Members collection [ADO MD]
ms.assetid: 3a647cde-efdc-4394-b1b9-8cbb1b9d689f
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bc86aad4176a2f5bac9e9fd70331109c89aa445c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="members-collection-ado-md"></a>Members 集合 (ADO MD)
包含[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)对象从一个级别或沿 x 轴的位置。  
  
## <a name="remarks"></a>Remarks  
 A**成员**使用集合来包含以下类型的成员：  
  
-   构成多维数据集中的级别成员。 这些批注包含在**成员**集合[级别](../../../ado/reference/ado-md-api/level-object-ado-md.md)对象。 例如，使用从示例[概述多维架构和数据](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)，国家/地区级别的四个成员是加拿大、 美国、 英国，和德国。  
  
-   成员的子级的层次结构中的特定成员。 这些成员返回的[子级](../../../ado/reference/ado-md-api/children-property-ado-md.md)的父属性**成员**对象。 例如，再次使用相同的示例，加拿大成员的两个子级是加拿大东部和加拿大西部。  
  
-   定义坐标轴上的特定位置的成员[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)。 使用从单元集[使用多维数据](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)举一个例子，x 轴上的第一个位置的两个成员是情人和西雅图。 这些成员包含通过**成员**集合[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)对象。  
  
 **成员**是一个标准的 ADO 集合。 属性和方法的集合，您可以执行以下操作：  
  
-   获取集合中具有的对象数[计数](../../../ado/reference/ado-api/count-property-ado.md)属性。  
  
-   返回从具有默认值的集合的对象[项](../../../ado/reference/ado-api/item-property-ado.md)属性。  
  
-   更新的提供程序从集合中的对象[刷新](../../../ado/reference/ado-api/refresh-method-ado.md)方法。  
  
 本部分包含以下主题。  
  
-   [属性、 方法和事件](../../../ado/reference/ado-md-api/members-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [成员示例 (VBScript)](../../../ado/reference/ado-md-api/members-example-vbscript.md)   
 [成员对象 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)
