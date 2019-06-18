---
title: 层次结构对象 (ADO MD) |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 5915102164afccd8e2055e14d0ef9d63b2cf5937
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66709145"
---
# <a name="hierarchy-object-ado-md"></a>层次结构对象 (ADO MD)
表示在其中的一种方法的成员[维度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)可以聚合或"累加起来。" 维度可以针对一个或多个层次结构进行聚合。  
  
## <a name="remarks"></a>备注  
 使用集合和属性的**层次结构**对象，您可以执行以下操作：  
  
-   识别**层次结构**与[名称](../../../ado/reference/ado-md-api/name-property-ado-md.md)并[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)属性。  
  
-   返回一个有意义的字符串，描述**层次结构**与[说明](../../../ado/reference/ado-md-api/description-property-ado-md.md)属性。  
  
-   返回[级别](../../../ado/reference/ado-md-api/level-object-ado-md.md)构成对象**层次结构**与[级别](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)集合。  
  
-   使用标准的 ADO[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，以获取有关其他信息**层次结构**对象。  
  
 **属性**集合包含提供程序提供的属性。 下表列出了可能可用的属性。 实际的属性列表可能不同的提供程序实现根据。 请参阅可用属性的更完整的列表为提供程序的文档。  
  
|“属性”|Description|  
|----------|-----------------|  
|AllMember|在层次结构中汇总的最高级别成员。|  
|CatalogName|此多维数据集所属的目录的名称。|  
|CubeName|多维数据集的名称。|  
|DefaultMember|此层次结构的默认成员唯一名称。|  
|Description|在层次结构有意义的说明。|  
|DimensionType|此层次结构所属的维度的类型。|  
|DimensionUniqueName|明确的维度的名称。|  
|HierarchyCaption|与层次结构关联的标签或标题。|  
|HierarchyCardinality|层次结构中的成员数。|  
|HierarchyGUID|层次结构的 GUID。|  
|HierarchyName|层次结构的名称。|  
|HierarchyUniqueName|明确的层次结构的名称。|  
|SchemaName|此多维数据集所属的架构的名称。|  
  
 本部分包含以下主题。  
  
-   [属性、 方法和事件](../../../ado/reference/ado-md-api/hierarchy-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [CubeDef 示例 (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [维度对象 (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [层次结构集合 (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [级别集合 (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
