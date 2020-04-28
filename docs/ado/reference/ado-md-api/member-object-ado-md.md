---
title: 成员对象（ADO MD） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member
helpviewer_keywords:
- Member object [ADO MD], members
ms.assetid: 3dedf755-0741-4c3f-8b4e-bff8ff8809c8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 44d6b5f06bffb1cea786ba34d3d2aa8a3efb45ee
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67949495"
---
# <a name="member-object-ado-md"></a>成员对象 (ADO MD)
表示多维数据集中某一级别的成员、某一级别的某个成员的子级或沿某个单元集的一个位置的成员。  
  
## <a name="remarks"></a>备注  
 **成员**的属性因使用它的上下文而异。 [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)中某一[级别](../../../ado/reference/ado-md-api/level-object-ado-md.md)的**成员**具有一个[子](../../../ado/reference/ado-md-api/children-property-ado-md.md)属性，该属性返回当前**成员**在层次结构中的下一个较低级别上的**成员**。 对于[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)的**成员**，**子**集合始终为空。 此外， [Type](../../../ado/reference/ado-md-api/type-property-ado-md.md)属性仅适用于**级别**的**成员**。  
  
 **位置**的**成员**具有两个属性，这些属性在显示[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)： [DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md)和[ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)时非常有用。 如果在某一**级别**的**成员**上访问这些属性，则会发生错误。  
  
 使用某一**级别**的**成员**对象的集合和属性，您可以执行以下操作：  
  
-   标识具有[Name](../../../ado/reference/ado-md-api/name-property-ado-md.md)和[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)属性的**成员**。  
  
-   返回一个字符串，该字符串在显示具有[Caption](../../../ado/reference/ado-md-api/caption-property-ado-md.md)属性的**成员**时使用。  
  
-   返回一个有意义的字符串，该字符串描述具有[Description](../../../ado/reference/ado-md-api/description-property-ado-md.md)属性的度量值或公式**成员**。  
  
-   确定具有[类型](../../../ado/reference/ado-md-api/type-property-ado-md.md)属性的**成员**的性质。  
  
-   获取有关具有[LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md)和[LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md)属性的**成员**的**级别**的信息。  
  
-   使用[父](../../../ado/reference/ado-md-api/parent-property-ado-md.md)属性和[子](../../../ado/reference/ado-md-api/children-property-ado-md.md)属性获取[层次结构](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)中的相关**成员**。  
  
-   使用[ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)属性计算**成员**的子级。  
  
-   使用标准 ADO [Properties](../../../ado/reference/ado-api/properties-collection-ado.md)集合获取有关**Level**对象的其他信息。  
  
 通过在[轴](../../../ado/reference/ado-md-api/axis-object-ado-md.md)上**放置某个位置**的**成员**的集合和属性，您可以执行以下操作：  
  
-   标识具有[Name](../../../ado/reference/ado-md-api/name-property-ado-md.md)和[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)属性的**成员**。  
  
-   返回一个字符串，该字符串在显示具有[Caption](../../../ado/reference/ado-md-api/caption-property-ado-md.md)属性的**成员**时使用。  
  
-   返回一个有意义的字符串，该字符串描述具有[Description](../../../ado/reference/ado-md-api/description-property-ado-md.md)属性的度量值或公式**成员**。  
  
-   获取有关具有[LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md)和[LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md)属性的**成员**的**级别**的信息。  
  
-   使用[ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)属性计算**成员**的子级。  
  
-   使用[DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md)属性可确定在此**成员**之后的**轴**上是否至少有一个子元素。  
  
-   使用[ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)属性来确定此**成员**的父级是否与紧前面的**成员**的父级相同。  
  
-   使用标准 ADO [Properties](../../../ado/reference/ado-api/properties-collection-ado.md)集合获取有关**Level**对象的其他信息。  
  
 **Properties**集合包含提供程序提供的属性。 下表列出了可用的属性。 实际属性列表可能有所不同，具体取决于提供程序的实现。 有关可用属性的更完整列表，请参阅提供程序的文档。  
  
|名称|说明|  
|----------|-----------------|  
|CatalogName|此多维数据集所属的目录的名称。|  
|ChildrenCardinality|成员具有的子级的个数。|  
|CubeName|多维数据集的名称。|  
|说明|成员的有意义的说明。|  
|DimensionUniqueName|[维度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)的明确名称。|  
|HierarchyUniqueName|层次结构的明确名称。|  
|LevelNumber|层次结构的级别与根之间的距离。|  
|LevelUniqueName|级别的明确名称。|  
|MemberCaption|与成员相关的标签或标题。|  
|MemberGUID|成员的 GUID。|  
|MemberName|成员的名称。|  
|MemberOrdinal|成员的序号。|  
|MemberType|成员的类型。|  
|MemberUniqueName|成员的明确名称。|  
|ParentCount|此成员具有的父级的计数。|  
|ParentLevel|成员的父级的级别号。|  
|ParentUniqueName|成员的父级的明确名称。|  
|SchemaName|此多维数据集所属架构的名称。|  
  
 本部分包含以下主题。  
  
-   [属性、方法和事件](../../../ado/reference/ado-md-api/member-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [目录示例（VB）](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [成员集合（ADO MD）](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
