---
title: 层次结构对象（ADO MD） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Hierarchy
helpviewer_keywords:
- Hierarchy object [ADO MD]
ms.assetid: 034af340-ac79-494e-ba5e-2b57da1cb9de
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 35e02e4823d0a3abf245e1885b95176d6350d712
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67949696"
---
# <a name="hierarchy-object-ado-md"></a>层次结构对象 (ADO MD)
表示一个[维度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)成员可以聚合或 "汇总" 的方式。 可以在一个或多个层次结构上聚合维度。  
  
## <a name="remarks"></a>备注  
 使用**层次结构**对象的集合和属性，可以执行以下操作：  
  
-   标识具有[Name](../../../ado/reference/ado-md-api/name-property-ado-md.md)和[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)属性的**层次结构**。  
  
-   返回一个有意义的字符串，该字符串描述具有[Description](../../../ado/reference/ado-md-api/description-property-ado-md.md)属性的**层次结构**。  
  
-   返回与[Level](../../../ado/reference/ado-md-api/level-object-ado-md.md) [集合构成](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)**层次结构**的级别对象。  
  
-   使用标准 ADO [Properties](../../../ado/reference/ado-api/properties-collection-ado.md)集合获取有关**层次结构**对象的其他信息。  
  
 **Properties**集合包含提供程序提供的属性。 下表列出了可用的属性。 实际属性列表可能有所不同，具体取决于提供程序的实现。 有关可用属性的更完整列表，请参阅提供程序的文档。  
  
|名称|说明|  
|----------|-----------------|  
|AllMember|层次结构中最高级别的汇总的成员。|  
|CatalogName|此多维数据集所属的目录的名称。|  
|CubeName|多维数据集的名称。|  
|DefaultMember|此层次结构的默认成员的唯一名称。|  
|说明|层次结构的有意义的说明。|  
|DimensionType|此层次结构所属的维度的类型。|  
|DimensionUniqueName|维度的明确名称。|  
|HierarchyCaption|与层次结构关联的标签或标题。|  
|HierarchyCardinality|层次结构中的成员数。|  
|HierarchyGUID|层次结构的 GUID。|  
|HierarchyName|层次结构的名称。|  
|HierarchyUniqueName|层次结构的明确名称。|  
|SchemaName|此多维数据集所属架构的名称。|  
  
 本部分包含以下主题。  
  
-   [属性、方法和事件](../../../ado/reference/ado-md-api/hierarchy-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [CubeDef 示例（VBScript）](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Dimension 对象（ADO MD）](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [层次结构集合（ADO MD）](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [级别集合（ADO MD）](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
