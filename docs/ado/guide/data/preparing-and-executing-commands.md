---
title: "准备和执行命令 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Command object [ADO], preparing and executing commands
ms.assetid: 7448d9ee-7f4b-47e3-be54-2df8c9bbac32
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e9c8bce6735f6fb7db1f0c279514aca3420d3ba1
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="preparing-and-executing-commands"></a>准备和执行命令
命令是颁发给提供程序执行某些操作对基础数据源的说明。 SQL 语句，例如，是到 Microsoft SQL 数据提供程序的命令。 在 ADO 中，命令通常表示由**命令**对象，尽管还可以通过发出简单命令**连接**或**记录集**对象。  
  
 你可以使用**命令**对象从提供程序，前提提供程序可以正确地解释命令字符串请求操作的任何支持的类型。 数据提供程序的常见操作是查询数据库并返回中的记录**记录集**对象，该程序可以被想象成一个容器来保存结果和一个工具，可查看的结果对象。 与许多 ADO 对象一样，某些**命令**对象集合、 方法或属性可能会产生错误在引用后，具体取决于提供程序功能。  
  
 除了使用**命令**对象，可以使用**执行**方法**连接**对象或**打开**方法**记录集**对象发出命令并让它执行。 但是，你应该使用**命令**对象，如果你需要重新使用的命令在代码中，或如果你需要传递与您的命令的详细的参数信息。 本部分中后面的更详细地介绍这些方案。  
  
> [!NOTE]
>  某些**命令**s 可以返回的结果集以二进制流的形式或为单个**记录**而不是**记录集**，如果提供程序支持此功能。 此外，某些**命令**s 并不返回任何结果根本设置 （例如，SQL Update 查询）。 本部分将介绍最典型的方案中，但是： 执行**命令**以形式返回结果的 s**记录集**对象。 有关返回到的结果的详细信息**记录**s 或**流**s，请参阅[记录和流](../../../ado/guide/data/records-and-streams.md)。  
  
 本部分包含以下主题。  
  
-   [命令对象概述](../../../ado/guide/data/command-object-overview.md)  
  
-   [创建和执行简单的命令](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [命令对象参数](../../../ado/guide/data/command-object-parameters.md)  
  
-   [使用命令调用存储过程](../../../ado/guide/data/calling-a-stored-procedure-with-a-command.md)  
  
-   [作为一个连接对象的方法调用存储的过程](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
-   [命名命令](../../../ado/guide/data/named-commands.md)  
  
-   [将参数传递给命名命令](../../../ado/guide/data/passing-parameters-to-a-named-command.md)
