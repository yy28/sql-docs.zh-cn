---
title: 形状的命令通常 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], shape commands
ms.assetid: 1fac7831-a187-4b15-9b43-aad380c5556c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f44063e4f1994e01f3685fdb2c7c47a5c41d4998
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704894"
---
# <a name="shape-commands-in-general"></a>常用 Shape 命令
数据整理定义的形状的列**记录集**，所列的方式表示的实体之间的关系**记录集**用数据填充。  
  
 形状**记录集**可以包含以下类型的列。  
  
|列类型|Description|  
|-----------------|-----------------|  
|data|字段从**记录集**查询命令返回到数据提供程序，表或以前形状**记录集**。|  
|一章|对另一个引用**记录集**称为*章*。 章节列使其可以定义*父-子*关系其中*父*是**记录集**的包含章节列和*子*是**记录集**由一章。|  
|聚合|通过执行派生列的值*聚合函数*上的所有行或子级的所有行的列**记录集**。 (请参阅以下主题中的聚合函数[聚合函数、 CALC 函数和 NEW 关键字](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)。)|  
|计算的表达式|通过 Visual Basic 应用程序中的同一行的列的表达式计算派生列的值**记录集**。 表达式是 CALC 函数的参数。 (请参阅以下主题中的计算表达式[聚合函数、 CALC 函数和 NEW 关键字](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)并在[Visual Basic for Applications 函数](../../../ado/guide/data/visual-basic-for-applications-functions.md)。)|  
|新|在更高版本时可以使用数据填充的空的虚构字段。 使用 NEW 关键字定义该列。 (请参阅以下主题中的新关键字[聚合函数、 CALC 函数和 NEW 关键字](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)。)|  
  
 形状命令可以包含指定的查询命令来将返回基础数据提供程序的子句**记录集**对象。 查询的语法取决于基础数据提供程序的要求。 通常，这是 SQL，虽然 ADO 不需要任何特定的查询语言使用。  
  
 可以通过发出形状命令**记录集**对象或设置[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)属性[命令](../../../ado/reference/ado-api/command-object-ado.md)对象，然后再调用[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)方法。  
  
 可以使用 SQL JOIN 子句来关联两个表;但是，一种分层**记录集**可以更高效地表示的信息。 每一行**记录集**创建由冗余地从一个表联接重复信息。 一种分层**记录集**只有一个父**记录集**为每个多个子**记录集**对象。  
  
 可以嵌套形状命令。 即*父命令*或*子命令*本身可能是另一个形状命令。  
  
 Shape 提供程序始终返回客户端游标，即使用户指定光标所在的位置**adUseServer**。  
  
 您可以访问**记录集**组件的形状**记录集**以编程方式或通过相应的可视化控件。  
  
 Microsoft 提供了一种可视化工具生成形状命令 (请参阅[数据环境设计器](https://go.microsoft.com/fwlink/?LinkId=5689)Visual Basic 6 文档中)，另一个显示分层光标 （请参阅"使用 Microsoft 层次结构Flexgrid 控件"中的 Visual Basic 6 文档）。  
  
 了解如何浏览的分层**记录集**，请参阅[访问分层记录集的行](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)。  
  
 有关语法正确的形状命令的精确信息，请参阅[正式 Shape 语法](../../../ado/guide/data/formal-shape-grammar.md)。  
  
 本部分包含以下主题。  
  
-   [聚合函数、CALC 函数和 NEW 关键字](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)  
  
-   [向基础数据提供程序发出命令](../../../ado/guide/data/issuing-commands-to-the-underlying-data-provider.md)
