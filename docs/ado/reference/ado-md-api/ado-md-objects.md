---
title: ADO MD 对象 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO MD, objects
- objects [ADO MD]
ms.assetid: 2a32e873-3282-4520-a7ed-89493f1da80e
author: rothja
ms.author: jroth
ms.openlocfilehash: 3e655647e7f485a27764280faba1adac091f0b7b
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242547"
---
# <a name="ado-md-objects"></a>ADO MD 对象

|对象|说明|  
|-|-|  
|[轴](../../../ado/reference/ado-md-api/axis-object-ado-md.md)|表示单元集的位置或筛选轴，其中包含一个或多个维度的选定成员。|  
|[目录](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|包含特定于多维数据访问接口（MDP）的多维架构信息（即多维数据集和基础维度、层次结构、级别和成员）。|  
|[芯](../../../ado/reference/ado-md-api/cell-object-ado-md.md)|表示轴坐标相交处的数据，该数据集包含在单元集中。|  
|[格](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|表示多维查询的结果。 它是从多维数据集或其他单元集选择的单元的集合。|  
|[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|表示多维架构中的一个多维数据集，其中包含一组相关的维度。|  
|[维度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|表示多维数据集的一个维度，其中包含一个或多个成员的层次结构。|  
|[层次结构](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|表示一个维度成员可以聚合或 "汇总" 的方式。 可以在一个或多个层次结构上聚合维度。|  
|[Level](../../../ado/reference/ado-md-api/level-object-ado-md.md)|包含一组成员，其中每个成员在层次结构中具有相同的级别。|  
|[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)|表示多维数据集中某一级别的成员、某一级别的某个成员的子级或沿某个单元集的一个位置的成员。|  
|[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)|表示一个或多个不同维度的成员的集合，这些成员定义沿轴的点。|  
  
 此外，**目录**对象还连接到 ado**连接**对象，该对象包含在标准 ADO 库中：  
  
|对象|说明|  
|------------|-----------------|  
|[Connection](../../../ado/reference/ado-api/connection-object-ado.md)|表示到数据源的连接是打开的。|  
  
 这些对象之间的关系如[ADO MD 对象模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)中所示。  
  
 许多 ADO MD 对象可以包含在相应的集合中。 例如， [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)对象可以包含在**目录**的[CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)集合中。 有关详细信息，请参阅[ADO MD 集合](../../../ado/reference/ado-md-api/ado-md-collections.md)。  
  
## <a name="see-also"></a>另请参阅  
 [ADO MD API 参考](../../../ado/reference/ado-md-api/ado-md-api-reference.md)   
 [ADO MD 代码示例](../../../ado/reference/ado-md-api/ado-md-code-examples.md)   
 [ADO MD 集合](../../../ado/reference/ado-md-api/ado-md-collections.md)   
 [ADO MD 枚举常量](../../../ado/reference/ado-md-api/ado-md-enumerated-constants.md)   
 [ADO MD 方法](../../../ado/reference/ado-md-api/ado-md-methods.md)   
 [ADO MD 对象模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO MD 属性](../../../ado/reference/ado-md-api/ado-md-properties.md)
