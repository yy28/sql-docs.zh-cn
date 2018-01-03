---
title: "维度对象 (ADO MD) |Microsoft 文档"
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
f1_keywords: Dimension
helpviewer_keywords: Dimension object [ADO MD]
ms.assetid: 66adbbd2-23a3-4c19-a91b-84c31309aa1b
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: aeab1d9f91ac80c78bd5c3f546d26ff1c868f3cd
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="dimension-object-ado-md"></a>维度对象 (ADO MD)
表示多维数据集中，包含一个或多个层次结构的成员的维度之一。  
  
## <a name="remarks"></a>Remarks  
 使用集合和属性的**维度**对象，你可以执行以下操作：  
  
-   标识**维度**与[名称](../../../ado/reference/ado-md-api/name-property-ado-md.md)和[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)属性。  
  
-   返回一个有意义的字符串，描述**维度**与[说明](../../../ado/reference/ado-md-api/description-property-ado-md.md)属性。  
  
-   返回[层次结构](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)组成对象**维度**与[层次结构](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)集合。  
  
-   使用标准的 ADO[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合以获取有关其他信息**维度**对象。  
  
 **属性**集合包含提供程序提供的属性。 下表列出可能可用的属性。 实际的属性列表可能不同根据提供程序的实现。 请参阅你的提供程序的更完整列表的可用属性的文档。  
  
|“属性”|Description|  
|----------|-----------------|  
|CatalogName|为此多维数据集所属的目录的名称。|  
|CubeName|多维数据集的名称。|  
|DefaultHierarchy|默认层次结构的唯一名称。|  
|Description|多维数据集有意义的描述。|  
|DimensionCaption|标签或标题与维度相关联。|  
|DimensionCardinality|维度中的成员数。|  
|DimensionGUID|维度的 GUID。|  
|DimensionName|维度的名称。|  
|DimensionOrdinal|在窗体多维数据集的维度的组之间的维度的序号。|  
|DimensionType|维度类型。|  
|DimensionUniqueName|维度的明确名称。|  
|SchemaName|此多维数据集所属的架构的名称。|  
  
 本部分包含以下主题。  
  
-   [属性、 方法和事件](../../../ado/reference/ado-md-api/dimension-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [CubeDef 示例 (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [CubeDef 对象 (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)   
 [维度集合 (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [层次结构集合 (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
