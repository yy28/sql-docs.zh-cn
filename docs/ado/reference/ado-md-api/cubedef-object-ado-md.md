---
title: CubeDef 对象 (ADO MD) |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CubeDef
helpviewer_keywords:
- CubeDef object [ADO MD]
ms.assetid: feb2581c-fc41-471c-bb69-29f8a55fda70
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 31e2bf587c19ab8088b0ab702be60fde54247aec
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="cubedef-object-ado-md"></a>CubeDef 对象 (ADO MD)
从包含一组相关的维度的多维架构表示多维数据集。  
  
## <a name="remarks"></a>注释  
 使用集合和属性的**CubeDef**对象，你可以执行以下操作：  
  
-   标识**CubeDef**与[名称](../../../ado/reference/ado-md-api/name-property-ado-md.md)属性。  
  
-   返回一个字符串，描述与多维数据集[说明](../../../ado/reference/ado-md-api/description-property-ado-md.md)属性。  
  
-   返回构成具有多维数据集维度[维度](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)集合。  
  
-   获取有关其他信息**CubeDef**用标准 ADO[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
 **属性**集合包含提供程序提供的属性。 下表列出可能可用的属性。 实际的属性列表可能不同根据提供程序的实现。 请参阅你的提供程序的更完整列表的可用属性的文档。  
  
|名称|Description|  
|----------|-----------------|  
|CatalogName|为此多维数据集所属的目录的名称。|  
|CreatedOn|日期和时间的多维数据集创建。|  
|CubeGUID|多维数据集 GUID。|  
|CubeName|多维数据集的名称。|  
|CubeType|多维数据集的类型。|  
|DataUpdatedBy|用户 ID 进行的最后一个的数据更新的人员。|  
|Description|多维数据集有意义的描述。|  
|LastSchemaUpdate|日期和时间的最后一个架构更新。|  
|SchemaName|此多维数据集所属的架构的名称。|  
|SchemaUpdatedBy|上次架构更新的人员的用户 ID。|  
  
 本部分包含以下主题。  
  
-   [属性、 方法和事件](../../../ado/reference/ado-md-api/cubedef-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [CubeDef 示例 (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [目录对象 (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)   
 [CubeDefs 集合 (ADO MD)](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)   
 [维度集合 (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
