---
title: "成员对象 (ADO MD) |Microsoft 文档"
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
f1_keywords: Member
helpviewer_keywords: Member object [ADO MD], members
ms.assetid: 3dedf755-0741-4c3f-8b4e-bff8ff8809c8
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6624e44343ef680c317338ea1fe32ead2aa0d9d0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="member-object-ado-md"></a>成员对象 (ADO MD)
表示多维数据集中，某一级别的成员级别的成员或沿 x 轴的单元集的位置的成员的子级。  
  
## <a name="remarks"></a>Remarks  
 属性**成员**与不同，具体取决于使用它的上下文。 A**成员**的[级别](../../../ado/reference/ado-md-api/level-object-ado-md.md)中[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)具有[子级](../../../ado/reference/ado-md-api/children-property-ado-md.md)返回的属性**成员**上从当前层次结构中的下一步较低级别**成员**。 有关**成员**的[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)、**子级**集合始终为空。 此外，[类型](../../../ado/reference/ado-md-api/type-property-ado-md.md)属性仅适用于**成员**的**级别**。  
  
 A**成员**的**位置**具有两个属性，可显示时[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md): [DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md)和[ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)。 如果上访问这些属性，将出现错误**成员**的**级别**。  
  
 使用集合和属性的**成员**对象**级别**，你可以执行以下操作：  
  
-   标识**成员**与[名称](../../../ado/reference/ado-md-api/name-property-ado-md.md)和[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)属性。  
  
-   返回字符串显示时要使用**成员**与[标题](../../../ado/reference/ado-md-api/caption-property-ado-md.md)属性。  
  
-   返回一个有意义的字符串，描述的度量值或公式**成员**与[说明](../../../ado/reference/ado-md-api/description-property-ado-md.md)属性。  
  
-   确定的性质**成员**与[类型](../../../ado/reference/ado-md-api/type-property-ado-md.md)属性。  
  
-   获取有关的信息**级别**的**成员**与[LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md)和[LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md)属性。  
  
-   获取相关**成员**中[层次结构](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)与[父](../../../ado/reference/ado-md-api/parent-property-ado-md.md)和[子级](../../../ado/reference/ado-md-api/children-property-ado-md.md)属性。  
  
-   计数的子级**成员**与[ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)属性。  
  
-   使用标准的 ADO[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合以获取有关其他信息**级别**对象。  
  
 使用集合和属性的**成员**的**位置**沿[轴](../../../ado/reference/ado-md-api/axis-object-ado-md.md)，你可以执行以下操作：  
  
-   标识**成员**与[名称](../../../ado/reference/ado-md-api/name-property-ado-md.md)和[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)属性。  
  
-   返回字符串显示时要使用**成员**与[标题](../../../ado/reference/ado-md-api/caption-property-ado-md.md)属性。  
  
-   返回一个有意义的字符串，描述的度量值或公式**成员**与[说明](../../../ado/reference/ado-md-api/description-property-ado-md.md)属性。  
  
-   获取有关的信息**级别**的**成员**与[LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md)和[LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md)属性。  
  
-   计数的子级**成员**与[ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)属性。  
  
-   使用[DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md)属性来确定上是否存在至少一个子**轴**紧跟 this**成员**。  
  
-   使用[ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)属性来确定是否此父**成员**立即前面父相同**成员**。  
  
-   使用标准的 ADO[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合以获取有关其他信息**级别**对象。  
  
 **属性**集合包含提供程序提供的属性。 下表列出可能可用的属性。 实际的属性列表可能不同根据提供程序的实现。 请参阅你的提供程序的更完整列表的可用属性的文档。  
  
|“属性”|Description|  
|----------|-----------------|  
|CatalogName|为此多维数据集所属的目录的名称。|  
|ChildrenCardinality|成员具有的子级的个数。|  
|CubeName|多维数据集的名称。|  
|Description|成员有意义的描述。|  
|DimensionUniqueName|明确名称[维度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)。|  
|HierarchyUniqueName|层次结构的明确名称。|  
|LevelNumber|层次结构的根级别之间的距离。|  
|LevelUniqueName|级别的明确的名称。|  
|MemberCaption|与成员相关的标签或标题。|  
|MemberGUID|成员的 GUID。|  
|MemberName|成员的名称。|  
|MemberOrdinal|该成员的序号。|  
|MemberType|成员的类型。|  
|成员的唯一名称|成员的明确名称。|  
|ParentCount|此成员的父级数的计数。|  
|ParentLevel|成员的父代的级别数。|  
|ParentUniqueName|成员的父级明确名称。|  
|SchemaName|此多维数据集所属的架构的名称。|  
  
 本部分包含以下主题。  
  
-   [属性、 方法和事件](../../../ado/reference/ado-md-api/member-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [目录 (VB) 示例](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [Members 集合 (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
