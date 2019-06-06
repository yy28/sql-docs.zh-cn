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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c06214d23441782cbe5e14433b16928224d5d48c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66709851"
---
# <a name="ado-md-objects"></a>ADO MD 对象

|||  
|-|-|  
|[Axis](../../../ado/reference/ado-md-api/axis-object-ado-md.md)|表示一个位置或单元，其中包含所选的一个或多个维度成员集的筛选轴。|  
|[目录](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|包含特定于多维数据提供程序 (MDP) 的多维架构信息 （即多维数据集和基础维度、 层次结构、 级别和成员）。|  
|[Cell](../../../ado/reference/ado-md-api/cell-object-ado-md.md)|表示单元集内包含的轴坐标相交处的数据。|  
|[Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|表示多维查询的结果。 它是从多维数据集或其他单元集中选择的单元的集合。|  
|[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|表示从多维架构，其中包含一组相关的维度的多维数据集。|  
|[Dimension](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|表示多维数据集，其中包含一个或多个层次结构的成员的维度之一。|  
|[Hierarchy](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|表示一种方式中的维度的成员可以为聚集的或"累加起来。" 维度可以针对一个或多个层次结构进行聚合。|  
|[Level](../../../ado/reference/ado-md-api/level-object-ado-md.md)|包含一组的成员，其中每个层次结构中相同的排名。|  
|[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)|表示在多维数据集，一个级别的成员的成员的级别或沿某个轴的单元集的位置的成员的子级。|  
|[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)|表示一组不同维度的一个或多个成员，用于定义沿某个轴的点。|  
  
 此外，**目录**对象连接到 ADO**连接**对象，它是包含在标准的 ADO 库：  
  
|Object|Description|  
|------------|-----------------|  
|[“连接”](../../../ado/reference/ado-api/connection-object-ado.md)|表示与数据源的开放连接。|  
  
 这些对象之间的关系中所示[ADO MD 对象模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)。  
  
 许多 ADO MD 对象可包含在相应的集合中。 例如， [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)对象可以包含在[CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)的集合**目录**。 有关详细信息，请参阅[ADO MD 集合](../../../ado/reference/ado-md-api/ado-md-collections.md)。  
  
## <a name="see-also"></a>请参阅  
 [ADO MD API 参考](../../../ado/reference/ado-md-api/ado-md-api-reference.md)   
 [ADO MD 代码示例](../../../ado/reference/ado-md-api/ado-md-code-examples.md)   
 [ADO MD 集合](../../../ado/reference/ado-md-api/ado-md-collections.md)   
 [ADO MD 枚举常量](../../../ado/reference/ado-md-api/ado-md-enumerated-constants.md)   
 [ADO MD 方法](../../../ado/reference/ado-md-api/ado-md-methods.md)   
 [ADO MD 对象模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO MD 属性](../../../ado/reference/ado-md-api/ado-md-properties.md)
