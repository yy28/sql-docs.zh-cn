---
title: 形状的命令通常 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], shape commands
ms.assetid: 1fac7831-a187-4b15-9b43-aad380c5556c
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c56148f0c94455ac96b926de050518d412098bab
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35272586"
---
# <a name="shape-commands-in-general"></a>在常规的形状命令
数据成型定义的列的形状**记录集**，由列中和在其中的方式表示实体之间的关系**记录集**用数据填充。  
  
 形状**记录集**可以包含以下类型的列。  
  
|列类型|Description|  
|-----------------|-----------------|  
|data|字段从**记录集**查询命令返回到数据提供程序，表，或以前调整**记录集**。|  
|章|对另一个引用**记录集**、 调用*章*。 章节列使其可以定义*父-子*关系其中*父*是**记录集**，其中包含的章节列和*子*是**记录集**由章。|  
|聚合|列的值的推导方式为执行*聚合函数*上的所有行或列的子级的所有行**记录集**。 (请参阅以下主题中的聚合函数[聚合函数、 CALC 函数和新关键字](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)。)|  
|计算的表达式|列的值的推导方式为计算 Visual Basic 应用程序上的同一行中的列的表达式**记录集**。 表达式是 CALC 函数的参数。 (请参阅以下主题中的计算表达式[聚合函数、 CALC 函数和新关键字](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)并在[应用程序函数的 Visual Basic](../../../ado/guide/data/visual-basic-for-applications-functions.md)。)|  
|新|在更高版本时可以用数据填充的空，虚构字段。 使用新的关键字定义列。 (请参阅以下主题中中的新关键字[聚合函数、 CALC 函数和新关键字](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)。)|  
  
 形状命令可以包含一个子句，它指定到基础数据提供程序将返回的查询命令**记录集**对象。 查询的语法取决于基础数据提供程序的要求。 通常，这是 SQL 中，尽管 ADO 不需要任何特定的查询语言的使用。  
  
 可以通过发出形状命令**记录集**对象或设置[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)属性[命令](../../../ado/reference/ado-api/command-object-ado.md)对象，然后再调用[执行](../../../ado/reference/ado-api/execute-method-ado-command.md)方法。  
  
 你可以使用的 SQL JOIN 子句将两个表; 关联起来但是，一种分层**记录集**可以更有效地表示的信息。 每一行**记录集**创建的不必要地从表中的一个联接重复一次信息。 一种分层**记录集**只有一个父**记录集**为每个多个子**记录集**对象。  
  
 形状命令可以嵌套。 也就是说，*父命令*或*子命令*本身也可能是另一个形状命令。  
  
 Shape 提供程序始终返回客户端游标，即使用户指定光标所在的位置**adUseServer**。  
  
 你可以访问**记录集**组件的形状**记录集**以编程方式或通过适当的可视化控件。  
  
 Microsoft 提供了一种可视化工具生成形状命令 (请参阅[数据环境设计器](http://go.microsoft.com/fwlink/?LinkId=5689)Visual Basic 6 文档中)，另一个显示分层光标 （请参阅"使用 Microsoft 层次结构Flexgrid 控件"中的 Visual Basic 6 文档）。  
  
 有关导航分层结构信息**记录集**，请参阅[访问分层记录集中的行](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)。  
  
 有关语法正确的形状命令的精确信息，请参阅[正式形状语法](../../../ado/guide/data/formal-shape-grammar.md)。  
  
 本部分包含以下主题。  
  
-   [聚合函数、CALC 函数和 NEW 关键字](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)  
  
-   [向基础数据提供程序发出命令](../../../ado/guide/data/issuing-commands-to-the-underlying-data-provider.md)
