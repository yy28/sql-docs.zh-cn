---
title: 管理作用域和上下文 (MDX) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- scripts [MDX], context
- scope [MDX]
- CALCULATE statement
- This function [MDX]
- SCOPE statement
- scripts [MDX], scope
ms.assetid: 631e7c20-8be9-4c35-8609-76516aef19d1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5bcaff42dd71f1c278c390d06240657f5f80f112
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62725668"
---
# <a name="managing-scope-and-context-mdx"></a>管理作用域和上下文 (MDX)
  在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中，多维表达式 (MDX) 脚本可以在脚本执行中的特定点应用于整个多维数据集或多维数据集的特定部分。 MDX 脚本可以通过使用计算传递采取分层方法在多维数据集内进行计算。  
  
> [!NOTE]  
>  有关计算传递如何影响计算的详细信息，请参阅[理解传递次序和求解次序 (MDX)](mdx-data-manipulation-understanding-pass-order-and-solve-order.md)。  
  
 若要控制 MDX 脚本中的计算传递、作用域以及上下文，可以明确使用 CACULATE 语句、`This` 函数以及 SCOPE 语句。  
  
## <a name="using-the-calculate-statement"></a>使用 CALCULATE 语句  
 CALCULATE 语句用聚合数据填充多维数据集中的每个单元。 例如，默认 MDX 脚本在脚本的开始处有一个 CALCULATE 语句。  
  
 有关 CALCULATE 语句的语法详细信息，请参阅 [CALCULATE 语句 (MDX)](/sql/mdx/mdx-scripting-calculate)。  
  
> [!NOTE]  
>  如果脚本包含含有 CALCULATE 语句的 SCOPE 语句，MDX 将在由 SCOPE 语句定义的子多维数据集的上下文内计算 CALCULATE 语句，而不是针对整个多维数据集进行计算。  
  
## <a name="using-the-this-function"></a>使用 This 函数  
 `This` 函数使您可以在 MDX 脚本内检索当前的子多维数据集。 您可以使用 `This` 函数快速将当前子多维数据集内的单元的值设置为 MDX 表达式。 在特定计算传递过程中，通常将 `This` 函数和 SCOPE 语句一起使用，以更改特定子多维数据集的内容。  
  
> [!NOTE]  
>  如果脚本包含含有 `This` 函数的 SCOPE 语句，MDX 将在由 SCOPE 语句定义的子多维数据集的上下文内计算 `This` 函数，而不是针对整个多维数据集进行计算。  
  
### <a name="this-function-example"></a>This 函数的示例  
 在 [!INCLUDE[ssAWDWsp](../../../includes/ssawdwsp-md.md)] 示例多维数据集的 Finance 度量值组中，以下 MDX 脚本命令示例使用 `This` 函数将 Customer 维度中 Redmond 成员的子级的 Amount 度量值增加 10%：  
  
```  
/* This SCOPE statement defines the current subcube */  
SCOPE([Customer].&[Redmond].MEMBERS,   
    [Measures].[Amount], *);  
        /* This expression sets the value of the Amount measure */  
        THIS = [Measures].[Amount] * 1.1;  
END SCOPE;  
```  
  
 有关详细信息的语法`This`函数中，请参阅[此&#40;MDX&#41;](/sql/mdx/this-mdx)。  
  
## <a name="using-the-scope-statement"></a>使用 SCOPE 语句  
 SCOPE 语句定义包含 MDX 脚本内其他 MDX 表达式和语句并指定这些表达式和语句的作用域的当前子多维数据集。 MDX 在该子多维数据集的上下文内计算其他 MDX 表达式和语句，包括 `This` 函数和 CALCULATE 语句。  
  
 SCOPE 语句本质上是动态的，但不是迭代的。 SCOPE 语句中包含的语句运行一次，但子多维数据集本身可以动态确定。 例如，有一个名为 SampleCube 的多维数据集。 对 SampleCube 多维数据集应用以下 SCOPE 语句以定义一个子多维数据集，将上下文定义为 Measures 维度内的 ALLMEMBERS：  
  
 `SCOPE([Measures].ALLMEMBERS);`  
  
 `THIS = [Measures].ALLMEMBERS.COUNT;`  
  
 `END SCOPE;`  
  
 此 SCOPE 语句中包含的语句和表达式运行一次。  
  
 现在，商业用户对 SampleCube 多维数据集运行以下 MDX 查询，该查询包含一个名为 ExistingMeasure 的度量值：  
  
 `WITH MEMBER [Measures].[NewMeasure] AS '1'`  
  
 `SELECT`  
  
 `[Measures].ALLMEMBERS ON COLUMNS,`  
  
 `[Customer].DEFAULTMEMBER ON ROWS`  
  
 `FROM`  
  
 `[SampleCube]`  
  
 查询所返回的单元集与下表中显示的输出相似。  
  
||[ExistingMeasure]|[NewMeasure]|  
|-|-------------------------|--------------------|  
|[Customer].[All]|2|2|  
  
 查看返回的单元集时，请注意定义度量值 NewMeasure 后，MDX 脚本中的 SCOPE 语句包含的 ExistingMeasure 值是如何动态更新的。  
  
 一个 SCOPE 语句可以嵌套在另一个 SCOPE 语句内。 但是，由于 SCOPE 语句不是迭代的，因此嵌套 SCOPE 语句的主要目的是进一步细分子多维数据集，以进行特殊的处理。  
  
### <a name="scope-statement-example"></a>SCOPE 语句的示例  
 在 [!INCLUDE[ssAWDWsp](../../../includes/ssawdwsp-md.md)] 示例多维数据集的 Finance 度量值组中，以下 MDX 脚本示例使用 SCOPE 语句将 Customer 维度中 Redmond 成员的子级的 Amount 度量值的值设置为比原来增加 10%。 但是，另一个 SCOPE 语句将子多维数据集更改为包含 2002 日历年子级的 Amount 度量值。 最后，仅为该子多维数据集聚合 Amount 度量值，其他日历年中 Amount 度量值的聚合值则保持不变。  
  
```  
/* Calculate the entire cube first. */  
CALCULATE;  
/* This SCOPE statement defines the current subcube */  
SCOPE([Customer].&[Redmond].MEMBERS,   
    [Measures].[Amount], *);  
        /* This expression sets the value of the Amount measure */  
        THIS = [Measures].[Amount] * 1.1;  
END SCOPE;  
```  
  
 有关 SCOPE 语句的语法详细信息，请参阅 [SCOPE 语句 (MDX)](/sql/mdx/mdx-scripting-scope)。  
  
## <a name="see-also"></a>请参阅  
 [MDX 语言参考 (MDX)](/sql/mdx/mdx-language-reference-mdx)   
 [基本 MDX 脚本 (MDX)](the-basic-mdx-script-mdx.md)   
 [MDX 查询基础知识 (Analysis Services)](mdx-query-fundamentals-analysis-services.md)  
  
  
