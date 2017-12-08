---
title: "MDX 脚本编写基础知识 (Analysis Services) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cubes [Analysis Services], scripts
- calculations [Analysis Services], scripts
- MDX [Analysis Services], scripts
- scripts [MDX]
- cubes [Analysis Services], calculations
- Multidimensional Expressions [Analysis Services], scripts
ms.assetid: fdecb3ce-7c87-4bab-8000-532ba7a29f96
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bf34d952a7a52b3993a3ddaec02caf34e93fb76d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="mdx-scripting-fundamentals-analysis-services"></a>MDX 脚本编写基础知识 (Analysis Services)
  在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中，多维表达式 (MDX) 脚本由一个或多个 MDX 表达式或语句构成，这些表达式或语句使用计算结果填充多维数据集。  
  
 MDX 脚本定义多维数据集的计算过程。 MDX 脚本也被视为多维数据集的一部分。 因此，更改与多维数据集相关联的 MDX 脚本将会立即更改多维数据集的计算过程。  
  
 要创建 MDX 脚本，您可以使用 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中的“多维数据集设计器”。 有关详细信息，请参阅 [定义赋值和其他脚本命令](../../../analysis-services/multidimensional-models/define-assignments-and-other-script-commands.md) 和 [Microsoft SQL Server 2005 中的 MDX 脚本简介](http://go.microsoft.com/fwlink/?LinkId=81892)。  
  
 有关与 MDX 查询和计算相关的性能问题，请参阅 [SQL Server Analysis Services 性能指南](http://go.microsoft.com/fwlink/p/?LinkId=399050)的“MDX 优化”部分。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[基本 MDX 脚本 (MDX)](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md)|详细介绍了基本 MDX 脚本（包括每个多维数据集中提供的默认 MDX 脚本），以及 MDX 脚本通常如何在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中的多维数据集内运行。|  
|[管理作用域和上下文 (MDX)](../../../analysis-services/multidimensional-models/mdx/managing-scope-and-context-mdx.md)|介绍如何使用 [CALCULATE](../../../mdx/mdx-scripting-calculate.md) 语句、 [SCOPE](../../../mdx/mdx-scripting-scope.md) 语句以及 [This](../../../mdx/this-mdx.md) 函数管理 MDX 脚本中的上下文和作用域。|  
|[使用变量和参数 (MDX)](../../../analysis-services/multidimensional-models/mdx/using-variables-and-parameters-mdx.md)|介绍如何在 MDX 脚本中使用变量和参数。|  
|[错误处理 (MDX)](../../../analysis-services/multidimensional-models/mdx/error-handling-mdx.md)|介绍 MDX 脚本中的错误处理。|  
|[支持的 MDX (MDX)](../../../analysis-services/multidimensional-models/mdx/supported-mdx-mdx.md)|提供 MDX 脚本中支持的 MDX 运算符、语句和函数的列表。|  
  
## <a name="see-also"></a>另请参阅  
 [MDX 语言参考 (MDX)](../../../mdx/mdx-language-reference-mdx.md)  
  
  
