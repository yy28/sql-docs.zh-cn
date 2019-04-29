---
title: 准备和执行命令 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Command object [ADO], preparing and executing commands
ms.assetid: 7448d9ee-7f4b-47e3-be54-2df8c9bbac32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f3de2bb729e2096e1b30aab12c402803036914b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62911356"
---
# <a name="preparing-and-executing-commands"></a>准备和执行命令
命令是颁发给提供程序执行某些操作对基础数据源的说明。 SQL 语句，例如，是 Microsoft SQL 数据提供程序的命令。 在 ADO 中，命令通常表示由**命令**对象，尽管也可以通过发出简单命令**连接**或**记录集**对象。  
  
 可以使用**命令**对象从提供程序，假定该提供程序可以正确地解释命令字符串中请求任何受支持的类型的操作。 数据提供程序的常见操作是查询数据库并返回中的记录**记录集**，可以认为的用于保存结果并使用工具来查看结果的容器的对象。 与许多 ADO 对象一样，某些**命令**对象集合、 方法或属性可能会产生错误时引用，具体取决于提供程序的功能。  
  
 除了使用之外**命令**对象，可以使用**Execute**方法**连接**对象或**打开**方法**记录集**对象发出命令，并使其执行。 但是，应使用**命令**对象，如果您需要重复使用在代码中，命令或如果需要传递详细的参数信息与你的命令。 本部分后面的更详细地介绍这些方案。  
  
> [!NOTE]
>  某些**命令**s 可以返回的结果集作为二进制流或作为单个**记录**而不是**记录集**，如果这提供程序支持。 此外，某些**命令**s 并不返回任何结果集，在所有 （例如，SQL 更新查询）。 本部分将介绍最典型的方案中，但是： 执行**命令**的返回结果作为**记录集**对象。 有关返回到结果的详细信息**记录**s 或**Stream**s，请参阅[记录和流](../../../ado/guide/data/records-and-streams.md)。  
  
 本部分包含以下主题。  
  
-   [命令对象概述](../../../ado/guide/data/command-object-overview.md)  
  
-   [创建和执行简单的命令](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [命令对象参数](../../../ado/guide/data/command-object-parameters.md)  
  
-   [使用命令调用存储过程](../../../ado/guide/data/calling-a-stored-procedure-with-a-command.md)  
  
-   [作为一个连接对象的方法调用存储的过程](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
-   [命名命令](../../../ado/guide/data/named-commands.md)  
  
-   [将参数传递给命名命令](../../../ado/guide/data/passing-parameters-to-a-named-command.md)
