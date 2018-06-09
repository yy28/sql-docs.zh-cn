---
title: ADO MD 对象 |Microsoft 文档
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
helpviewer_keywords:
- ADO MD, objects
- objects [ADO MD]
ms.assetid: 2a32e873-3282-4520-a7ed-89493f1da80e
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ae297d189b03af51c73a98e6f273601e805b25c
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "32807130"
---
# <a name="ado-md-objects"></a>ADO MD 对象
|||  
|-|-|  
|[Axis](../../../ado/reference/ado-md-api/axis-object-ado-md.md)|表示一个位置或筛选器轴的单元集，包含所选的成员的一个或多个维度。|  
|[目录](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|包含特定于多维数据提供程序 (MDP) 的多维架构信息 （即，多维数据集和基础维度、 层次结构、 级别和成员）。|  
|[单元格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)|表示包含在单元集中的轴坐标的交叉点处的数据。|  
|[Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|表示多维查询的结果。 它是从多维数据集或其他单元集中选定单元格的集合。|  
|[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|从包含一组相关的维度的多维架构表示多维数据集。|  
|[Dimension](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|表示多维数据集中，包含一个或多个层次结构的成员的维度之一。|  
|[Hierarchy](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|表示一种方式在其中一个维度的成员可以为聚集的或"汇总。" 可以在一个或多个层次结构上聚合的维度。|  
|[Level](../../../ado/reference/ado-md-api/level-object-ado-md.md)|包含一组的成员，其中每个具有相同的排名层次结构中。|  
|[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)|表示多维数据集中，某一级别的成员级别的成员或沿 x 轴的单元集的位置的成员的子级。|  
|[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)|表示一组定义的点沿 x 轴的不同维度的一个或多个成员。|  
  
 此外，**目录**对象连接到 ADO**连接**对象，它又包括在标准的 ADO 库：  
  
|Object|Description|  
|------------|-----------------|  
|[连接](../../../ado/reference/ado-api/connection-object-ado.md)|表示与数据源的开放连接。|  
  
 这些对象之间的关系所示[ADO MD 对象模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)。  
  
 相应集合中可包含多个 ADO MD 对象。 例如， [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)对象可以包含在[CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)集合**目录**。 有关详细信息，请参阅[ADO MD 集合](../../../ado/reference/ado-md-api/ado-md-collections.md)。  
  
## <a name="see-also"></a>请参阅  
 [ADO MD API 参考](../../../ado/reference/ado-md-api/ado-md-api-reference.md)   
 [ADO MD 代码示例](../../../ado/reference/ado-md-api/ado-md-code-examples.md)   
 [ADO MD 集合](../../../ado/reference/ado-md-api/ado-md-collections.md)   
 [ADO MD 枚举常量](../../../ado/reference/ado-md-api/ado-md-enumerated-constants.md)   
 [ADO MD 方法](../../../ado/reference/ado-md-api/ado-md-methods.md)   
 [ADO MD 对象模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO MD 属性](../../../ado/reference/ado-md-api/ado-md-properties.md)
