---
title: 多维模型中的多维数据集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- OLAP objects [Analysis Services], cubes
- cubes [Analysis Services], about cubes
- cubes [Analysis Services]
- OLAP [Analysis Services], cubes
ms.assetid: e0f7acf3-4b07-41fc-a5fc-ac30b4a56c54
caps.latest.revision: 32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ca5da5ea8dfb22adc6e038f9dc54740e5102aad0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37237727"
---
# <a name="cubes-in-multidimensional-models"></a>多维模型中的多维数据集
  多维数据集是包含用于分析的信息的多维结构；多维数据集主要由维度和度量值构成。 维度定义您用来对其执行切片操作的多维数据集的结构，而度量值提供最终用户感兴趣的聚合数值。 作为逻辑结构，多维数据集允许客户端应用程序检索度量值的值，就像它们包含在多维数据集的单元中一样；将为每个可能的摘要值都定义单元。 多维数据集中的单元通过维度成员的交集定义，并且包含该特定交集处的度量值的聚合值。  
  
## <a name="benefits-of-using-cubes"></a>使用多维数据集的好处  
 多维数据集提供存储所有相关数据以便进行分析的单一位置。  
  
## <a name="components-of-cubes"></a>多维数据集的组件  
 一个多维数据集由以下组件构成：  
  
|元素|Description|  
|-------------|-----------------|  
|维度|[多维模型中的维度](dimensions-in-multidimensional-models.md)|  
|度量值和度量值组|[在多维模型中创建度量值和度量值组](create-measures-and-measure-groups-in-multidimensional-models.md)|  
|“度量值组”|[多维模型中的分区](partitions-in-multidimensional-models.md)|  
|透视|[多维模型中的透视](perspectives-in-multidimensional-models.md)|  
|层次结构|[创建用户定义的层次结构](user-defined-hierarchies-create.md)|  
|操作|[多维模型中的操作](actions-in-multidimensional-models.md)|  
|关键绩效指标 (KPI)|[关键绩效指标&#40;Kpi&#41;多维模型中](key-performance-indicators-kpis-in-multidimensional-models.md)|  
|“新建命名集”|[多维模型中的计算](calculations-in-multidimensional-models.md)|  
|翻译|[多维模型中的翻译](translations-in-multidimensional-models-analysis-services.md)|  
  
## <a name="related-tasks"></a>Related Tasks  
  
|主题|Description|  
|-----------|-----------------|  
|[使用多维数据集向导创建多维数据集](create-a-cube-using-the-cube-wizard.md)|说明如何使用多维数据集向导定义多维数据集、维度、维度属性以及用户定义层次结构。|  
|[在多维模型中创建度量值和度量值组](create-measures-and-measure-groups-in-multidimensional-models.md)|介绍如何定义度量值组。|  
|[多维模型中的计算](calculations-in-multidimensional-models.md)|说明如何在 MDX 脚本中定义和配置计算。|  
|[多维模型中的操作](actions-in-multidimensional-models.md)|说明如何定义和配置操作。|  
|[多维模型中的透视](perspectives-in-multidimensional-models.md)|说明如何定义和配置透视。|  
|[定义存储过程](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)|说明如何使用存储过程。|  
  
  
