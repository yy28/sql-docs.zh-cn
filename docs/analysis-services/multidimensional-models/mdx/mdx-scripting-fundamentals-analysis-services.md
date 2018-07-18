---
title: MDX 脚本编写基础知识 (Analysis Services) |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9ca77b9c10f1dba24127e35e5fe55d7ffcdad3dc
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34021724"
---
# <a name="mdx-scripting-fundamentals-analysis-services"></a>MDX 脚本编写基础知识 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中，多维表达式 (MDX) 脚本由一个或多个 MDX 表达式或语句构成，这些表达式或语句使用计算结果填充多维数据集。  
  
 MDX 脚本定义多维数据集的计算过程。 MDX 脚本也被视为多维数据集的一部分。 因此，更改与多维数据集相关联的 MDX 脚本将会立即更改多维数据集的计算过程。  
  
 要创建 MDX 脚本，您可以使用 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中的“多维数据集设计器”。 有关详细信息，请参阅 [定义赋值和其他脚本命令](../../../analysis-services/multidimensional-models/define-assignments-and-other-script-commands.md) 和 [Microsoft SQL Server 2005 中的 MDX 脚本简介](http://go.microsoft.com/fwlink/?LinkId=81892)。  
  
 有关与 MDX 查询和计算相关的性能问题，请参阅 [SQL Server Analysis Services 性能指南](http://go.microsoft.com/fwlink/p/?LinkId=399050)的“MDX 优化”部分。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[基本 MDX 脚本 & #40;MDX & #41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md)|详细介绍了基本 MDX 脚本（包括每个多维数据集中提供的默认 MDX 脚本），以及 MDX 脚本通常如何在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中的多维数据集内运行。|  
|[管理作用域和上下文 & #40;MDX & #41;](../../../analysis-services/multidimensional-models/mdx/managing-scope-and-context-mdx.md)|介绍如何使用 [CALCULATE](../../../mdx/mdx-scripting-calculate.md) 语句、 [SCOPE](../../../mdx/mdx-scripting-scope.md) 语句以及 [This](../../../mdx/this-mdx.md) 函数管理 MDX 脚本中的上下文和作用域。|  
|[使用变量和参数 & #40;MDX & #41;](../../../analysis-services/multidimensional-models/mdx/using-variables-and-parameters-mdx.md)|介绍如何在 MDX 脚本中使用变量和参数。|  
|[错误处理 & #40;MDX & #41;](../../../analysis-services/multidimensional-models/mdx/error-handling-mdx.md)|介绍 MDX 脚本中的错误处理。|  
|[支持的 MDX & #40;MDX & #41;](../../../analysis-services/multidimensional-models/mdx/supported-mdx-mdx.md)|提供 MDX 脚本中支持的 MDX 运算符、语句和函数的列表。|  
  
## <a name="see-also"></a>另请参阅  
 [MDX 语言参考 & #40;MDX & #41;](../../../mdx/mdx-language-reference-mdx.md)  
  
  
