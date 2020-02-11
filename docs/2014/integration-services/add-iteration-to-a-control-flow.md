---
title: 向控制流添加迭代 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- repeating workflows
- adding iterations
- control flow [Integration Services], iterations
- expressions [Integration Services], control flow
- iterations [Integration Services]
- For Loop containers
ms.assetid: eb3a7494-88ae-4165-9d0f-58715eb1734a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b96f5f900e8c1a3adf136c7bdaf1b89f297e4921
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66061974"
---
# <a name="add-iteration-to-a-control-flow"></a>将迭代添加到控制流
  
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包含 For 循环容器，此控制流元素使得可以更简便地包含按条件重复包中控制流的循环。 有关详细信息，请参阅 [For Loop Container](control-flow/for-loop-container.md)。  
  
 For 循环容器计算每次循环迭代的条件，并在该条件的计算结果为 false 时停止。 For 循环容器含有用于对循环进行初始化的表达式，并指定停止执行重复控制流的求值条件，以及为表达式（其更新与求值条件进行比较的值）赋值。 必须提供求值条件，但初始化表达式和赋值表达式为可选。  
  
 For 循环容器不提供功能，只提供用来生成可重复的控制流的结构。 若要提供容器功能，则 For 循环容器中必须至少包含一个任务。 有关详细信息，请参阅 [Integration Services Tasks](control-flow/integration-services-tasks.md)。  
  
 For 循环容器可包含具有多个任务的控制流，还可包含其他容器。 将任务和容器添加到 For 循环容器的过程与将它们添加到包的过程相似，不同的是将任务和容器拖动到 For 循环容器而不是拖动到包。 如果 For 循环容器包含多个任务或容器，可以使用优先约束连接它们，就像在包中操作一样。 有关详细信息，请参阅 [优先约束](control-flow/precedence-constraints.md)。  
  
## <a name="using-expressions-in-for-loop-configuration"></a>在 For 循环配置中使用表达式  
 用指定求值条件、初始化值或赋值值的方法配置 For 循环容器时，可以使用文字或表达式。  
  
 表达式中可以包含变量。 使用变量的优点是变量可在运行时更新，使得包管理起来更灵活、更容易。 表达式的最大长度为 4000 个字符。  
  
 在表达式中指定变量时，必须在其前面加符号 @。 例如，对于名`Counter`为的变量，请@Counter在 for 循环容器使用的表达式中输入。 如果变量上包含了命名空间属性，则您必须用方括号将变量和命名空间括起来。 例如，对于`Counter` `MyNamespace`命名空间中的变量，请键入 [@MyNamespace::Counter]。  
  
 For 循环容器使用的变量必须在 For 循环容器的范围内定义，或者在包容器层次结构中较高层次容器的范围内定义。 例如，For 循环容器可使用在其范围内定义的变量，也可使用在包范围内定义的变量。 有关详细信息，请参阅[Integration Services &#40;SSIS&#41; 变量](integration-services-ssis-variables.md)和[在包中使用变量](../../2014/integration-services/use-variables-in-packages.md)。  
  
 
  [!INCLUDE[ssIS](../includes/ssis-md.md)] 表达式语法提供了一整套运算符和函数，可以用于实现计算、初始化或赋值所用的复杂表达式。 有关详细信息，请参阅 [Integration Services (SSIS) 表达式](expressions/integration-services-ssis-expressions.md)。  
  
### <a name="to-implement-a-for-loop-container-in-a-control-flow"></a>在控制流中实现 For 循环容器  
  
1.  将 For 循环容器添加到包。 有关详细信息，请参阅[在控制流中添加或删除任务或容器](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
2.  将任务和容器添加到 For 循环容器。 有关详细信息，请参阅[在控制流中添加或删除任务或容器](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
3.  使用优先约束连接 For 循环容器中的任务和容器。 有关详细信息，请参阅 [使用默认优先约束来连接任务和容器](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)。  
  
4.  配置 For 循环容器。 有关详细信息，请参阅 [配置 For 循环容器](../../2014/integration-services/configure-a-for-loop-container.md)。  
  
## <a name="see-also"></a>另请参阅  
 [在控制流中添加或删除任务或容器](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)   
 [对组件进行分组或取消分组](group-or-ungroup-components.md)   
 [使用默认优先约束来连接任务和容器](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)   
 [向控制流添加枚举](../../2014/integration-services/add-enumeration-to-a-control-flow.md)   
 [控制流](control-flow/control-flow.md)  
  
  
