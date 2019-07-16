---
title: 级别对象 (ADO MD) |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949604"
---
# <a name="level-object-ado-md"></a>级别对象 (ADO MD)
包含一组的成员，其中每个层次结构中相同的排名。  
  
## <a name="remarks"></a>备注  
 使用集合和属性的**级别**对象，您可以执行以下操作：  
  
-   识别**级别**与[名称](../../../ado/reference/ado-md-api/name-property-ado-md.md)并[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)属性。  
  
-   返回显示时要使用的字符串**级别**与[标题](../../../ado/reference/ado-md-api/caption-property-ado-md.md)属性。  
  
-   返回一个有意义的字符串，描述**级别**与[说明](../../../ado/reference/ado-md-api/description-property-ado-md.md)属性。  
  
-   返回[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)构成对象**级别**与[成员](../../../ado/reference/ado-md-api/members-collection-ado-md.md)集合。  
  
-   返回的根级别的数量**级别**与[深度](../../../ado/reference/ado-md-api/depth-property-ado-md.md)属性。  
  
-   使用标准的 ADO[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，以获取有关其他信息**级别**对象。  
  
 **属性**集合包含提供程序提供的属性。 下表列出了可能可用的属性。 实际的属性列表可能不同的提供程序实现根据。 请参阅可用属性的更完整的列表为提供程序的文档。  
  
|名称|描述|  
|----------|-----------------|  
|CatalogName|此多维数据集所属的目录的名称。|  
|CubeName|多维数据集的名称。|  
|描述|级别的有意义说明。|  
|DimensionUniqueName|明确的名称[维度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)。|  
|HierarchyUniqueName|明确的层次结构的名称。|  
|LevelCaption|标签或标题与级别关联。|  
|LevelCardinality|级别中的成员数。|  
|LevelGUID|级别的 GUID。|  
|LevelName|级别的名称。|  
|LevelNumber|层次结构的根级别之间的距离。|  
|LevelType|级别的类型。|  
|LevelUniqueName|明确的级别名称。|  
|SchemaName|此多维数据集所属的架构的名称。|  
  
 本部分包含以下主题。  
  
-   [属性、 方法和事件](../../../ado/reference/ado-md-api/level-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [CubeDef 示例 (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [层次结构对象 (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)   
 [级别集合 (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [成员集合 (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
