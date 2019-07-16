---
title: 成员对象 (ADO MD) |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949495"
---
# <a name="member-object-ado-md"></a>成员对象 (ADO MD)
表示在多维数据集，一个级别的成员的成员的级别或沿某个轴的单元集的位置的成员的子级。  
  
## <a name="remarks"></a>备注  
 属性**成员**使用它的上下文而异。 一个**成员**的[级别](../../../ado/reference/ado-md-api/level-object-ado-md.md)中[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)具有[子级](../../../ado/reference/ado-md-api/children-property-ado-md.md)返回的属性**成员**上从当前层次结构中的下一个较低级别**成员**。 有关**成员**的[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)，则**子级**集合始终为空。 此外，[类型](../../../ado/reference/ado-md-api/type-property-ado-md.md)属性仅适用于**成员**的**级别**。  
  
 一个**成员**的**位置**具有两个属性显示时的有用[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md):[DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md)并[ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)。 如果在访问这些属性将会出错**成员**的**级别**。  
  
 使用集合和属性的**成员**对象的**级别**，您可以执行以下操作：  
  
-   识别**成员**与[名称](../../../ado/reference/ado-md-api/name-property-ado-md.md)并[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)属性。  
  
-   返回显示时要使用的字符串**成员**与[标题](../../../ado/reference/ado-md-api/caption-property-ado-md.md)属性。  
  
-   返回一个有意义的字符串，描述将度量值或公式**成员**与[说明](../../../ado/reference/ado-md-api/description-property-ado-md.md)属性。  
  
-   确定的性质**成员**与[类型](../../../ado/reference/ado-md-api/type-property-ado-md.md)属性。  
  
-   获取有关的信息**级别**的**成员**与[LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md)并[LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md)属性。  
  
-   获取相关**成员**中[层次结构](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)与[父](../../../ado/reference/ado-md-api/parent-property-ado-md.md)并[子级](../../../ado/reference/ado-md-api/children-property-ado-md.md)属性。  
  
-   计数的子级**成员**与[ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)属性。  
  
-   使用标准的 ADO[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，以获取有关其他信息**级别**对象。  
  
 使用集合和属性的**成员**的**位置**沿[轴](../../../ado/reference/ado-md-api/axis-object-ado-md.md)，您可以执行以下操作：  
  
-   识别**成员**与[名称](../../../ado/reference/ado-md-api/name-property-ado-md.md)并[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)属性。  
  
-   返回显示时要使用的字符串**成员**与[标题](../../../ado/reference/ado-md-api/caption-property-ado-md.md)属性。  
  
-   返回一个有意义的字符串，描述将度量值或公式**成员**与[说明](../../../ado/reference/ado-md-api/description-property-ado-md.md)属性。  
  
-   获取有关的信息**级别**的**成员**与[LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md)并[LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md)属性。  
  
-   计数的子级**成员**与[ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)属性。  
  
-   使用[DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md)属性来确定是否存在至少一个子**轴**紧跟此**成员**。  
  
-   使用[ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)属性来确定是否此父**成员**前面紧邻的父级相同**成员**。  
  
-   使用标准的 ADO[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，以获取有关其他信息**级别**对象。  
  
 **属性**集合包含提供程序提供的属性。 下表列出了可能可用的属性。 实际的属性列表可能不同的提供程序实现根据。 请参阅可用属性的更完整的列表为提供程序的文档。  
  
|“属性”|描述|  
|----------|-----------------|  
|CatalogName|此多维数据集所属的目录的名称。|  
|ChildrenCardinality|成员具有的子级的个数。|  
|CubeName|多维数据集的名称。|  
|描述|成员的有意义说明。|  
|DimensionUniqueName|明确的名称[维度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)。|  
|HierarchyUniqueName|明确的层次结构的名称。|  
|LevelNumber|层次结构的根级别之间的距离。|  
|LevelUniqueName|明确的级别名称。|  
|MemberCaption|与成员相关的标签或标题。|  
|MemberGUID|成员的 GUID。|  
|MemberName|成员的名称。|  
|MemberOrdinal|成员的序号。|  
|MemberType|成员的类型。|  
|MemberUniqueName|明确的成员的名称。|  
|ParentCount|此成员的父项的数目的计数。|  
|ParentLevel|成员的父代的级别数。|  
|ParentUniqueName|明确成员的父级的名称。|  
|SchemaName|此多维数据集所属的架构的名称。|  
  
 本部分包含以下主题。  
  
-   [属性、 方法和事件](../../../ado/reference/ado-md-api/member-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [目录示例 (VB)](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [成员集合 (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
