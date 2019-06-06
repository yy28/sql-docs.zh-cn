---
title: CubeDef 对象 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CubeDef
helpviewer_keywords:
- CubeDef object [ADO MD]
ms.assetid: feb2581c-fc41-471c-bb69-29f8a55fda70
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 3831c78380d8ae34e1dab74e92514c7d84136988
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66709385"
---
# <a name="cubedef-object-ado-md"></a>CubeDef 对象 (ADO MD)
表示从多维架构，其中包含一组相关的维度的多维数据集。  
  
## <a name="remarks"></a>备注  
 使用集合和属性的**CubeDef**对象，您可以执行以下操作：  
  
-   识别**CubeDef**与[名称](../../../ado/reference/ado-md-api/name-property-ado-md.md)属性。  
  
-   返回一个字符串，描述与多维数据集[说明](../../../ado/reference/ado-md-api/description-property-ado-md.md)属性。  
  
-   返回构成了与多维数据集的维度[维度](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)集合。  
  
-   获取有关其他信息**CubeDef**与标准的 ADO[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
 **属性**集合包含提供程序提供的属性。 下表列出了可能可用的属性。 实际的属性列表可能不同的提供程序实现根据。 请参阅可用属性的更完整的列表为提供程序的文档。  
  
|“属性”|Description|  
|----------|-----------------|  
|CatalogName|此多维数据集所属的目录的名称。|  
|CreatedOn|日期和时间的多维数据集创建。|  
|CubeGUID|多维数据集的 GUID。|  
|CubeName|多维数据集的名称。|  
|CubeType|多维数据集的类型。|  
|DataUpdatedBy|执行的最后一个数据更新的人员的用户 ID。|  
|Description|多维数据集的贴切描述。|  
|LastSchemaUpdate|日期和时间的上次架构更新。|  
|SchemaName|此多维数据集所属的架构的名称。|  
|SchemaUpdatedBy|执行上次架构更新的人员的用户 ID。|  
  
 本部分包含以下主题。  
  
-   [属性、 方法和事件](../../../ado/reference/ado-md-api/cubedef-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [CubeDef 示例 (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [目录对象 (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)   
 [CubeDefs 集合 (ADO MD)](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)   
 [维度集合 (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
