---
title: 层次结构对象 (ADO MD) |Microsoft 文档
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
- Hierarchy
helpviewer_keywords:
- Hierarchy object [ADO MD]
ms.assetid: 034af340-ac79-494e-ba5e-2b57da1cb9de
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1904398172f9a7b1eaad57e3c4cda11a00fad22e
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="hierarchy-object-ado-md"></a>层次结构对象 (ADO MD)
表示在其中的一种方式的成员[维度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)可以聚合或"汇总。" 可以在一个或多个层次结构上聚合的维度。  
  
## <a name="remarks"></a>注释  
 使用集合和属性的**层次结构**对象，你可以执行以下操作：  
  
-   标识**层次结构**与[名称](../../../ado/reference/ado-md-api/name-property-ado-md.md)和[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)属性。  
  
-   返回一个有意义的字符串，描述**层次结构**与[说明](../../../ado/reference/ado-md-api/description-property-ado-md.md)属性。  
  
-   返回[级别](../../../ado/reference/ado-md-api/level-object-ado-md.md)组成对象**层次结构**与[级别](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)集合。  
  
-   使用标准的 ADO[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合以获取有关其他信息**层次结构**对象。  
  
 **属性**集合包含提供程序提供的属性。 下表列出可能可用的属性。 实际的属性列表可能不同根据提供程序的实现。 请参阅你的提供程序的更完整列表的可用属性的文档。  
  
|名称|Description|  
|----------|-----------------|  
|AllMember|在层次结构中的汇总最高级别成员。|  
|CatalogName|为此多维数据集所属的目录的名称。|  
|CubeName|多维数据集的名称。|  
|DefaultMember|此层次结构的默认成员唯一名称。|  
|Description|层次结构的有意义的描述。|  
|DimensionType|为此层次结构所属的维度的类型。|  
|DimensionUniqueName|维度的明确名称。|  
|HierarchyCaption|与层次结构关联的标签或标题。|  
|HierarchyCardinality|层次结构中的成员数。|  
|HierarchyGUID|层次结构的 GUID。|  
|HierarchyName|层次结构的名称。|  
|HierarchyUniqueName|层次结构的明确名称。|  
|SchemaName|此多维数据集所属的架构的名称。|  
  
 本部分包含以下主题。  
  
-   [属性、 方法和事件](../../../ado/reference/ado-md-api/hierarchy-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [CubeDef 示例 (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [维度对象 (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [层次结构集合 (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [级别集合 (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
