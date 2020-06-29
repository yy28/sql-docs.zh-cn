---
title: 将表达式添加到优先约束 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- precedence executables [Integration Services]
- precedence constraints [Integration Services], adding expressions
- adding expressions
- constrained executables [Integration Services]
- combining constraints
- expressions [Integration Services], constraints
ms.assetid: 5574d89a-a68e-4b84-80ea-da93305e5ca1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3b86869a2b5d2e1ecd93227355509170db2bd5c7
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439664"
---
# <a name="add-expressions-to-precedence-constraints"></a>将表达式添加到优先约束
  优先约束可用表达式定义两个可执行文件之间的约束：优先可执行文件和受约束的可执行文件。 可执行文件可以是任务或容器。 表达式可以单独使用，也可以与优先可执行文件的执行结果结合使用。 可执行文件的执行结果或者为成功，或者为失败。 配置优先约束的执行结果时，可以将执行结果设置为 `Success`、`Failure` 或 `Completion`。 `Success` 要求优先可执行文件成功；`Failure` 要求优先可执行文件失败；而 `Completion` 则指示无论优先任务成功或失败，受约束的可执行文件都应运行。 有关详细信息，请参阅 [优先约束](control-flow/precedence-constraints.md)。  
  
 表达式的值必须为 `True` 或 `False`，并且此表达式必须为有效的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 表达式。 此表达式可以使用文字、系统变量和自定义变量以及 [!INCLUDE[ssIS](../includes/ssis-md.md)] 表达式语法提供的函数和运算符。 例如，表达式 `@Count == SQRT(144) + 10` 使用了变量 `Count`、SQRT 函数以及等号 (==) 和加号 (+) 运算符。 有关详细信息，请参阅 [Integration Services (SSIS) 表达式](expressions/integration-services-ssis-expressions.md)。  
  
 在下图中，使用一个执行结果和一个表达式的优先约束将任务 A 和任务 B 链接在一起。 此约束值设置为 `Success`，表达式为 `@X >== @Z`。 仅当任务 A 成功完成且变量 `X` 的值大于或等于变量 `Z` 的值时，受约束的任务 B 才运行。  
  
 ![两个任务之间的优先约束](media/mw-dts-03.gif "两个任务之间的优先约束")  
  
 也可以用包含不同表达式的多个优先约束来链接可执行文件。 例如，在下图中，使用执行结果和表达式的优先约束将任务 B 和任务 C 链接到任务 A。 两个约束的值都设置为 `Success.`，一个优先约束包含表达式 `@X >== @Z`，而另一个优先约束包含表达式 `@X < @Z`。 变量 `X` 和变量 `Z` 的值决定是任务 C 运行还是任务 B 运行。  
  
 ![优先约束表达式](media/mw-dts-04.gif "优先约束表达式")  
  
 可使用 **设计器中的** “优先约束编辑器” [!INCLUDE[ssIS](../includes/ssis-md.md)] 和 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 提供的“属性”窗口来添加或修改表达式。 但是，“属性”窗口不提供表达式语法验证。  
  
 如果优先约束包含表达式，那么在 **“控制流”** 选项卡的设计图面上会有一个图标出现在该优先约束旁边，图标上的 ToolTip 显示此表达式。  
  
## <a name="combining-execution-values-and-expressions"></a>将执行值和表达式组合起来。  
 下表介绍把执行值约束和表达式组合在优先约束中的效果。  
  
|求值运算|约束的计算结果为|表达式的计算结果为|受约束的可执行文件运行|  
|--------------------------|-----------------------------|-----------------------------|---------------------------------|  
|约束|True|空值|True|  
|约束|False|空值|False|  
|表达式|空值|True|True|  
|表达式|空值|False|False|  
|约束和表达式|True|True|True|  
|约束和表达式|True|False|False|  
|约束和表达式|False|True|False|  
|约束和表达式|False|False|False|  
|约束或表达式|True|True|True|  
|约束或表达式|True|False|True|  
|约束或表达式|False|True|True|  
|约束或表达式|False|False|False|  
  
### <a name="to-add-an-expression-to-a-precedence-constraint"></a>将表达式添加到优先约束  
  
-   [在优先约束中使用表达式](../../2014/integration-services/use-an-expression-in-a-precedence-constraint.md)  
  
-   [设置优先约束的属性](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)  
  
## <a name="external-resources"></a>外部资源  
 social.technet.microsoft.com 上的技术文章 [SSIS 表达式示例](https://go.microsoft.com/fwlink/?LinkId=220761)  
  
## <a name="see-also"></a>另请参阅  
 [多个优先约束](../../2014/integration-services/multiple-precedence-constraints.md)   
 [优先约束](control-flow/precedence-constraints.md)  
  
  
