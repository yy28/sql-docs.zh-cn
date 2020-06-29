---
title: 优先约束 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- tasks [Integration Services], precedence constraints
- control flow [Integration Services], precedence constraints
- precedence constraints [Integration Services]
- constraints [Integration Services]
- sequence execution options [Integration Services]
- containers [Integration Services], precedence constraints
ms.assetid: c5ce5435-fd89-4156-a11f-68470a69aa9f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 14fd00565c011b04c28345faca8ee5db5ae821f9
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85438194"
---
# <a name="precedence-constraints"></a>优先约束
  优先约束在控制流中链接包中的可执行文件、容器和任务，并指定决定可执行文件是否运行的条件。 可执行文件可以是 For 循环容器、Foreach 循环容器、序列容器、任务或事件处理程序。 事件处理程序也使用优先约束将其可执行文件链接为控制流。

 优先约束链接两个可执行文件：优先可执行文件和受约束的可执行文件。 优先可执行文件先于受约束的可执行文件运行，而优先可执行文件的执行结果可能决定受约束的可执行文件是否运行。 下列关系图显示由优先约束链接的两个可执行文件。

 ![由优先约束连接的可执行文件](../media/ssis-pcsimple.gif "由优先约束连接的可执行文件")

 在线性控制流（即不分支的控制流）中，优先约束独自控制任务运行的顺序。 如果控制流有分支，则由 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 运行时引擎决定紧随分支之后的任务和容器的执行顺序。 运行时引擎还决定着控制流中未连接的工作流的执行顺序。

 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 的嵌套容器体系结构使得所有容器（除仅封装单个任务的任务宿主容器之外）均可包含其他容器，且每个容器都有自己的控制流。 For 循环容器、Foreach 循环容器和序列容器可以包含多个任务和其他容器，而这些任务和容器又可以包含多个任务和容器，如此逐层嵌套。 例如，带有脚本任务和序列容器的包具有链接该脚本任务和序列容器的优先约束。 序列容器包含三个脚本任务，且容器的优先约束将此三个脚本任务链接为控制流。 下列关系图显示包中带有两级嵌套的优先约束。

 ![包中的优先约束](../media/mw-dts-12.gif "包中的优先约束")

 由于包位于 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 容器层次结构的顶部，因此优先约束不能链接多个包；但是可以向包添加执行包任务并间接地将其他包链接到控制流中。

 可以使用下列方式配置优先约束：

-   指定求值运算。 优先约束同时使用约束值和表达式，或者使用其中任一个来决定受约束的可执行文件是否运行。

-   如果优先约束使用执行结果，则您可以指定执行结果成功、失败或完成。

-   如果优先约束使用计算结果，则您可以提供计算结果为布尔值的表达式。

-   指定优先约束是单独计算还是与应用于受约束可执行文件的其他约束一起计算。

## <a name="evaluation-operations"></a>求值运算
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 提供下列求值运算：

-   仅使用优先可执行文件的执行结果来决定受约束的可执行文件是否运行的约束。 优先可执行文件的执行结果可以为完成、成功或失败。 这是默认操作。

-   求值以决定受约束的可执行文件是否运行的表达式。 如果表达式计算结果为 true，则受约束的可执行文件运行。

-   组合了对优先可执行文件执行结果以及对计算表达式返回结果的要求的表达式和约束。

-   使用优先可执行文件执行结果或使用计算表达式返回结果的表达式或约束。

 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器用颜色标识优先约束的类型。 “成功”约束为绿色，“失败”约束为红色，而“完成”约束为蓝色。 若要在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器中显示表明约束类型的文本标签，则必须配置 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器的可访问性功能。

 表达式必须是有效的 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 表达式，且可以包含函数、运算符以及系统和自定义变量。 有关详细信息，请参阅 [Integration Services (SSIS) 表达式](../expressions/integration-services-ssis-expressions.md)和 [Integration Services (SSIS) 变量](../integration-services-ssis-variables.md)。

## <a name="execution-results"></a>执行结果
 优先约束可以单独使用下列执行结果或将这些结果与表达式结合使用。

-   完成仅要求优先可执行文件完成而不考虑结果，受约束的执行文件便可运行。

-   成功要求优先可执行文件必须成功完成，受约束的可执行文件才能运行。

-   失败要求优先可执行文件失败，受约束的可执行文件便可运行。

> [!NOTE]
>  优先约束必须为相同 `Precedence Constraint` 集合的成员，才能组成逻辑与条件。 例如，不能组合来自两个 Foreach 循环容器的优先约束。

## <a name="configuration-of-the-precedence-constraint"></a>优先约束的配置
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。

 有关可以在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器中设置的属性的信息，请参阅 [优先约束编辑器](../precedence-constraint-editor.md)。

 有关如何以编程方式设置这些属性的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint>。

## <a name="related-tasks"></a>Related Tasks
 有关如何在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击以下主题之一：

-   [设置优先约束的属性](../set-the-properties-of-a-precedence-constraint.md)

-   [使用快捷菜单设置优先约束的值](../set-the-value-of-a-precedence-constraint-by-using-the-shortcut-menu.md)

-   [使用默认优先约束来连接任务和容器](../connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)

     本主题提供有关如何设置优先约束的默认行为以及如何用默认优先约束来连接可执行文件的信息，请参阅：

## <a name="related-content"></a>相关内容
 social.technet.microsoft.com 上的技术文章 [SSIS 表达式示例](https://go.microsoft.com/fwlink/?LinkId=220761)

## <a name="see-also"></a>另请参阅
 [将表达式添加到优先约束](../add-expressions-to-precedence-constraints.md)[多个优先约束](../multiple-precedence-constraints.md)


