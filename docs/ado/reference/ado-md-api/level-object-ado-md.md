---
title: Level 对象（ADO MD） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level
helpviewer_keywords:
- Level object [ADO MD]
ms.assetid: 37815869-ed30-45fd-9aea-0a986c1b305c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4a44060ae4ffd9399c34d4cd8133f5ad7404ed5a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67949604"
---
# <a name="level-object-ado-md"></a>级别对象 (ADO MD)
包含一组成员，其中每个成员在层次结构中具有相同的级别。  
  
## <a name="remarks"></a>备注  
 使用**Level**对象的集合和属性，可以执行以下操作：  
  
-   标识具有[Name](../../../ado/reference/ado-md-api/name-property-ado-md.md)和[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)属性的**级别**。  
  
-   返回在用[Caption](../../../ado/reference/ado-md-api/caption-property-ado-md.md)属性显示**级别**时要使用的字符串。  
  
-   返回一个有意义的字符串，该字符串描述具有[Description](../../../ado/reference/ado-md-api/description-property-ado-md.md)属性的**级别**。  
  
-   返回组成[成员](../../../ado/reference/ado-md-api/members-collection-ado-md.md)集合的**级别**的[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)对象。  
  
-   从**级别**的根返回[深度](../../../ado/reference/ado-md-api/depth-property-ado-md.md)属性的级别数。  
  
-   使用标准 ADO [Properties](../../../ado/reference/ado-api/properties-collection-ado.md)集合获取有关**Level**对象的其他信息。  
  
 **Properties**集合包含提供程序提供的属性。 下表列出了可用的属性。 实际属性列表可能有所不同，具体取决于提供程序的实现。 有关可用属性的更完整列表，请参阅提供程序的文档。  
  
|名称|说明|  
|----------|-----------------|  
|CatalogName|此多维数据集所属的目录的名称。|  
|CubeName|多维数据集的名称。|  
|说明|级别的有意义的说明。|  
|DimensionUniqueName|[维度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)的明确名称。|  
|HierarchyUniqueName|层次结构的明确名称。|  
|LevelCaption|与级别关联的标签或标题。|  
|LevelCardinality|级别中的成员数。|  
|LevelGUID|级别的 GUID。|  
|LevelName|级别的名称。|  
|LevelNumber|层次结构的级别与根之间的距离。|  
|LevelType|级别的类型。|  
|LevelUniqueName|级别的明确名称。|  
|SchemaName|此多维数据集所属架构的名称。|  
  
 本部分包含以下主题。  
  
-   [属性、方法和事件](../../../ado/reference/ado-md-api/level-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [CubeDef 示例（VBScript）](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [层次结构对象（ADO MD）](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)   
 [级别集合（ADO MD）](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [成员集合（ADO MD）](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
