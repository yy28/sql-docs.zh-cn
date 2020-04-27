---
title: MDX 脚本编写基础知识（Analysis Services） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- cubes [Analysis Services], scripts
- calculations [Analysis Services], scripts
- MDX [Analysis Services], scripts
- scripts [MDX]
- cubes [Analysis Services], calculations
- Multidimensional Expressions [Analysis Services], scripts
ms.assetid: fdecb3ce-7c87-4bab-8000-532ba7a29f96
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 17cb2b326ed510a952249da6a73693b6be6ab252
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66073856"
---
# <a name="mdx-scripting-fundamentals-analysis-services"></a>MDX 脚本编写基础知识 (Analysis Services)
  在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中，多维表达式 (MDX) 脚本由一个或多个 MDX 表达式或语句构成，这些表达式或语句使用计算结果填充多维数据集。  
  
 MDX 脚本定义多维数据集的计算过程。 MDX 脚本也被视为多维数据集的一部分。 因此，更改与多维数据集相关联的 MDX 脚本将会立即更改多维数据集的计算过程。  
  
 要创建 MDX 脚本，您可以使用 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中的“多维数据集设计器”。 有关详细信息，请参阅 [定义赋值和其他脚本命令](../define-assignments-and-other-script-commands.md) 和 [Microsoft SQL Server 2005 中的 MDX 脚本简介](https://go.microsoft.com/fwlink/?LinkId=81892)。  
  
 有关与 MDX 查询和计算相关的性能问题，请参阅 [SQL Server Analysis Services 性能指南](https://go.microsoft.com/fwlink/p/?LinkId=399050)的“MDX 优化”部分。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|说明|  
|-----------|-----------------|  
|[基本 MDX 脚本 (MDX)](the-basic-mdx-script-mdx.md)|详细介绍了基本 MDX 脚本（包括每个多维数据集中提供的默认 MDX 脚本），以及 MDX 脚本通常如何在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中的多维数据集内运行。|  
|[管理作用域和上下文 (MDX)](managing-scope-and-context-mdx.md)|介绍如何使用 [CALCULATE](/sql/mdx/mdx-scripting-calculate) 语句、 [SCOPE](/sql/mdx/mdx-scripting-scope) 语句以及 [This](/sql/mdx/this-mdx) 函数管理 MDX 脚本中的上下文和作用域。|  
|[使用变量和参数 (MDX)](using-variables-and-parameters-mdx.md)|介绍如何在 MDX 脚本中使用变量和参数。|  
|[错误处理 (MDX)](error-handling-mdx.md)|介绍 MDX 脚本中的错误处理。|  
|[支持的 MDX (MDX)](supported-mdx-mdx.md)|提供 MDX 脚本中支持的 MDX 运算符、语句和函数的列表。|  
  
## <a name="see-also"></a>另请参阅  
 [MDX 语言参考 (MDX)](/sql/mdx/mdx-language-reference-mdx)  
  
  
