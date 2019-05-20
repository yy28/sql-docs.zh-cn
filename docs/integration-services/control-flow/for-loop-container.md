---
title: For 循环容器 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.forloopcontainerdetails.f1
- sql13.dts.designer.forloopcontainer.f1
helpviewer_keywords:
- repeating control flow
- containers [Integration Services], For Loop
- For Loop containers
ms.assetid: 44cf7355-992b-4bbf-a28c-bfb012de06f6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 683d3bcee8450a62a040663dacf30d337556529d
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65727677"
---
# <a name="for-loop-container"></a>For 循环容器

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  For 循环容器定义包中的重复控制流。 此循环实现类似于编程语言中的 **For** 循环结构。 循环每次重复时，For 循环容器都计算一个表达式并重复运行其工作流，直到表达式计算结果为 **False**。  
  
 For 循环容器使用下列元素定义循环：  
  
-   为循环计数器赋值的可选初始化表达式。  
  
-   包含用于测试循环应停止还是继续的表达式的求值表达式。  
  
-   递增或递减循环计数器的可选迭代表达式。  
  
 下图显示了一个具有发送邮件任务的 For 循环容器。 如果初始化表达式为 `@Counter = 0`，求值表达式为 `@Counter < 4`，迭代表达式为 `@Counter = @Counter + 1`，则该循环将重复运行四次并发送四封电子邮件。  
  
 ![For 循环容器重复执行任务四次](../../integration-services/control-flow/media/ssis-forloop.gif "A For Loop container repeats a task four times")  
  
 表达式必须是有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 表达式。  
  
 若要创建初始化和赋值表达式，可以使用赋值运算符 (=)。 此运算符在其他方面不为 Integration Services 表达式语法所支持，只能供 For 循环容器中的初始化和赋值表达式类型使用。 使用赋值运算符的任何表达式都必须使用语法 `@Var = <expression>`，其中 Var 是运行时变量，\<expression> 是遵循 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 表达式语法规则的表达式。 表达式可以包含 SSIS 表达式语法支持的变量、文字以及任何运算符和函数。 表达式的计算结果的数据类型必须能够转换为变量的数据类型。  
  
 一个 For 循环容器只能有一个求值表达式。 这意味着 For 循环容器对所有其控制流元素运行相同次数。 因为 For 循环容器可以包含其他 For 循环容器，所以可以在包中构建嵌套循环和实现复杂循环。  
  
 可以为 For 循环容器设置一个事务属性，为包控制流的子集定义一个事务。 采用这种方法，可以更详细地管理事务。 例如，如果 For 循环容器多次重复一个更新表中数据的控制流，则可以配置 For 循环及其控制流，让它们使用一个事务来确保数据只有在全部数据都成功更新后才更新。 有关详细信息，请参阅 [Integration Services 事务](../../integration-services/integration-services-transactions.md)。  
  
## <a name="add-iteration-to-a-control-flow-with-the-for-loop-container"></a>使用 For 循环容器将迭代添加到控制流
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含 For 循环容器，此控制流元素使得可以更简便地包含按条件重复包中控制流的循环。 有关详细信息，请参阅 [For 循环容器](../../integration-services/control-flow/for-loop-container.md)。  
  
 For 循环容器计算每次循环迭代的条件，并在该条件的计算结果为 false 时停止。 For 循环容器含有用于对循环进行初始化的表达式，并指定停止执行重复控制流的求值条件，以及为表达式（其更新与求值条件进行比较的值）赋值。 必须提供求值条件，但初始化表达式和赋值表达式为可选。  
  
 For 循环容器不提供功能，只提供用来生成可重复的控制流的结构。 若要提供容器功能，则 For 循环容器中必须至少包含一个任务。 有关详细信息，请参阅 [Integration Services Tasks](../../integration-services/control-flow/integration-services-tasks.md)。  
  
 For 循环容器可包含具有多个任务的控制流，还可包含其他容器。 将任务和容器添加到 For 循环容器的过程与将它们添加到包的过程相似，不同的是将任务和容器拖动到 For 循环容器而不是拖动到包。 如果 For 循环容器包含多个任务或容器，可以使用优先约束连接它们，就像在包中操作一样。 有关详细信息，请参阅 [优先约束](../../integration-services/control-flow/precedence-constraints.md)。  
  
## <a name="add-a-for-loop-container-in-a-control-flow"></a>在控制流中添加 For 循环容器  
  
1.  将 For 循环容器添加到包。 有关详细信息，请参阅[在控制流中添加或删除任务或容器](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)。  
  
2.  将任务和容器添加到 For 循环容器。 有关详细信息，请参阅 [在控制流中添加或删除任务或容器](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)。  
  
3.  使用优先约束连接 For 循环容器中的任务和容器。 有关详细信息，请参阅[使用默认优先约束来连接任务和容器](https://msdn.microsoft.com/library/8f31f15f-98ff-4c35-b41f-8b8cfd148d75)。  
  
4.  配置 For 循环容器。 有关详细信息，请参阅 [配置 For 循环容器](https://msdn.microsoft.com/library/b9cd7ea7-b198-4a35-8b16-6acf09611ca5)。  

##  <a name="configure-the-for-loop-container"></a>配置 For 循环容器
此过程介绍如何使用 **“For 循环编辑器”** 对话框配置 For 循环容器。  
  
 有关 For 循环容器的示例，请参阅 bimonkey.com 上的 [不失败的 SSIS 循环](https://go.microsoft.com/fwlink/?LinkId=240295) 。  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，双击 For 循环容器，打开“For 循环编辑器”。  
  
2.  根据需要，修改 For 循环容器的名称和说明。  
  
3.  根据需要，在 **InitExpression** 文本框中键入初始化表达式。  
  
4.  在 **EvalExpression** 文本框中键入求值表达式。  
  
    > [!NOTE]  
    >  表达式的计算结果必须为布尔值。 当表达式的计算结果为 **false**时，循环停止运行。  
  
5.  根据需要，在 **AssignExpression** 文本框中键入赋值表达式。  
  
6.  根据需要，单击 **“表达式”** ，并在 **“表达式”** 页上为 For 循环容器的属性创建属性表达式。 有关详细信息，请参阅 [添加或更改属性表达式](../../integration-services/expressions/add-or-change-a-property-expression.md)。  
  
7.  单击 **“确定”** ，关闭 **“For 循环编辑器”**。  

## <a name="for-loop-editor-dialog-box"></a>“For 循环编辑器”对话框
可以使用 **“For 循环编辑器”** 对话框的 **“For 循环”** 页，配置只有在指定条件的计算结果为 False 时才会停止重复执行工作流的循环。  
  
 若要了解有关 For 循环容器以及如何在包中使用它的信息，请参阅 [For Loop Container](../../integration-services/control-flow/for-loop-container.md)。  
  
### <a name="options"></a>选项  
 **InitExpression**  
 提供初始化该循环所用值的表达式（可选）。  
  
 **EvalExpression**  
 提供用于计算循环应停止还是继续的表达式。  
  
 **AssignExpression**  
 提供在每次循环重复时更改条件的表达式（可选）。  
  
 **名称**  
 为 For 循环容器提供唯一的名称。 此名称用作任务图标中的标签。  
  
> [!NOTE]  
>  对象名称在一个包内必须是唯一的。  
  
 **Description**  
 提供 For 循环容器的说明。  
 
## <a name="use-expressions-with-the-for-loop-container"></a>将表达式与 For 循环容器配合使用  
 用指定求值条件、初始化值或赋值值的方法配置 For 循环容器时，可以使用文字或表达式。  
  
 表达式中可以包含变量。 使用变量的优点是变量可在运行时更新，使得包管理起来更灵活、更容易。 表达式的最大长度为 4000 个字符。  
  
 在表达式中指定变量时，必须在其前面加符号 @。 例如，对于名为 Counter 的变量，请在 For 循环容器使用的表达式中输入 @Counter。 如果变量上包含了命名空间属性，则您必须用方括号将变量和命名空间括起来。 例如，对于 MyNamespace 命名空间中的 Counter 变量，请键入 [@MyNamespace::Counter]。  
  
 For 循环容器使用的变量必须在 For 循环容器的范围内定义，或者在包容器层次结构中较高层次容器的范围内定义。 例如，For 循环容器可使用在其范围内定义的变量，也可使用在包范围内定义的变量。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)和[在包中使用变量](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 表达式语法提供了一整套运算符和函数，可以用于实现计算、初始化或赋值所用的复杂表达式。 有关详细信息，请参阅 [Integration Services (SSIS) 表达式](../../integration-services/expressions/integration-services-ssis-expressions.md)。  
  
  
## <a name="see-also"></a>另请参阅  
 [控制流](../../integration-services/control-flow/control-flow.md)   
 [Integration Services (SSIS) 表达式](../../integration-services/expressions/integration-services-ssis-expressions.md)  
  
  
