---
title: For 循环容器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.forloopcontainerdetails.f1
helpviewer_keywords:
- repeating control flow
- containers [Integration Services], For Loop
- For Loop containers
ms.assetid: 44cf7355-992b-4bbf-a28c-bfb012de06f6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ec872407dbec3885f72c4300b90cb3e11d1bcf92
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85433034"
---
# <a name="for-loop-container"></a>For 循环容器
  For 循环容器定义包中的重复控制流。 此循环实现类似于编程语言中的 **For** 循环结构。 循环每次重复时，For 循环容器都计算一个表达式并重复运行其工作流，直到表达式计算结果为 `False`。  
  
 For 循环容器使用下列元素定义循环：  
  
-   为循环计数器赋值的可选初始化表达式。  
  
-   包含用于测试循环应停止还是继续的表达式的求值表达式。  
  
-   递增或递减循环计数器的可选迭代表达式。  
  
 下图显示了一个具有发送邮件任务的 For 循环容器。 如果初始化表达式为 `@Counter = 0`，求值表达式为 `@Counter < 4`，迭代表达式为 `@Counter = @Counter + 1`，则该循环将重复运行四次并发送四封电子邮件。  
  
 ![For 循环容器重复执行任务四次](../media/ssis-forloop.gif "For 循环容器重复执行任务四次")  
  
 表达式必须是有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 表达式。  
  
 若要创建初始化和赋值表达式，可以使用赋值运算符 (=)。 此运算符在其他方面不为 Integration Services 表达式语法所支持，只能供 For 循环容器中的初始化和赋值表达式类型使用。 使用赋值运算符的任何表达式都必须具有语法 `@Var = <expression>` ，其中**Var**是运行时变量， \<expression> 是遵循表达式语法规则的表达式 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 。 表达式可以包含 SSIS 表达式语法支持的变量、文字以及任何运算符和函数。 表达式的计算结果的数据类型必须能够转换为变量的数据类型。  
  
 一个 For 循环容器只能有一个求值表达式。 这意味着 For 循环容器对所有其控制流元素运行相同次数。 因为 For 循环容器可以包含其他 For 循环容器，所以可以在包中构建嵌套循环和实现复杂循环。  
  
 可以为 For 循环容器设置一个事务属性，为包控制流的子集定义一个事务。 采用这种方法，可以更详细地管理事务。 例如，如果 For 循环容器多次重复一个更新表中数据的控制流，则可以配置 For 循环及其控制流，让它们使用一个事务来确保数据只有在全部数据都成功更新后才更新。 有关详细信息，请参阅 [Integration Services 事务](../integration-services-transactions.md)。  
  
## <a name="configuration-of-the-for-loop-container"></a>For 循环容器的配置  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击下列主题之一：  
  
-   [For 循环编辑器](../for-loop-editor.md)  
  
-   [“表达式”页](../expressions/expressions-page.md)  
  
 有关以编程方式设置这些属性的详细信息，请参阅开发人员指南中针对 **T:Microsoft.SqlServer.Dts.Runtime.ForLoop** 类的文档。  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何配置 For 循环容器的信息，请参阅以下主题。  
  
-   [配置 For 循环容器](for-loop-container.md)  
  
-   [设置任务或容器的属性](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>另请参阅  
 [控制流](control-flow.md)   
 [Integration Services (SSIS) 表达式](../expressions/integration-services-ssis-expressions.md)  
  
  
