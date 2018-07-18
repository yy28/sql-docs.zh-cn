---
title: 级别对象 (ADO MD) |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level
helpviewer_keywords:
- Level object [ADO MD]
ms.assetid: 37815869-ed30-45fd-9aea-0a986c1b305c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 35263c640b1446397776a4365349afdd522d78f4
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35283986"
---
# <a name="level-object-ado-md"></a>级别对象 (ADO MD)
包含一组的成员，其中每个具有相同的排名层次结构中。  
  
## <a name="remarks"></a>Remarks  
 使用集合和属性的**级别**对象，你可以执行以下操作：  
  
-   标识**级别**与[名称](../../../ado/reference/ado-md-api/name-property-ado-md.md)和[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)属性。  
  
-   返回字符串显示时要使用**级别**与[标题](../../../ado/reference/ado-md-api/caption-property-ado-md.md)属性。  
  
-   返回一个有意义的字符串，描述**级别**与[说明](../../../ado/reference/ado-md-api/description-property-ado-md.md)属性。  
  
-   返回[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)组成对象**级别**与[成员](../../../ado/reference/ado-md-api/members-collection-ado-md.md)集合。  
  
-   返回从的根级别数**级别**与[深度](../../../ado/reference/ado-md-api/depth-property-ado-md.md)属性。  
  
-   使用标准的 ADO[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合以获取有关其他信息**级别**对象。  
  
 **属性**集合包含提供程序提供的属性。 下表列出可能可用的属性。 实际的属性列表可能不同根据提供程序的实现。 请参阅你的提供程序的更完整列表的可用属性的文档。  
  
|“属性”|Description|  
|----------|-----------------|  
|CatalogName|为此多维数据集所属的目录的名称。|  
|CubeName|多维数据集的名称。|  
|Description|级别的有意义的描述。|  
|DimensionUniqueName|明确名称[维度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)。|  
|HierarchyUniqueName|层次结构的明确名称。|  
|LevelCaption|标签或与级别关联的标题。|  
|LevelCardinality|级别中的成员数。|  
|LevelGUID|级别的 GUID。|  
|LevelName|级别的名称。|  
|LevelNumber|层次结构的根级别之间的距离。|  
|LevelType|级别的类型。|  
|LevelUniqueName|级别的明确的名称。|  
|SchemaName|此多维数据集所属的架构的名称。|  
  
 本部分包含以下主题。  
  
-   [属性、 方法和事件](../../../ado/reference/ado-md-api/level-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [CubeDef 示例 (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [层次结构对象 (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)   
 [级别集合 (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [Members 集合 (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
