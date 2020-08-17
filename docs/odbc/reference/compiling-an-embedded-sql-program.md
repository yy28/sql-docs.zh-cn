---
description: 编译嵌入式 SQL 程序
title: 编译嵌入式 SQL 程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- compiling embedded SQL programs [ODBC]
- embedded SQL [ODBC]
ms.assetid: 9e94146a-5b80-4a01-b586-1e03ff05b9ac
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5065d50bd9ae23cc7db8a2310b13792b461da2a5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386073"
---
# <a name="compiling-an-embedded-sql-program"></a>编译嵌入式 SQL 程序
由于嵌入的 SQL 程序包含 SQL 和宿主语言语句的混合，因此无法将其直接提交给主机语言的编译器。 相反，它是通过多步骤进程进行编译的。 尽管此过程与产品不同，但对于所有产品，步骤大致相同。  
  
 下图显示编译嵌入式 SQL 程序所需的步骤。  
  
 ![用于编译嵌入式 SQL 程序的步骤](../../odbc/reference/media/pr02.gif "pr02")  
  
 编译嵌入式 SQL 程序涉及五个步骤：  
  
1.  将嵌入式 SQL 程序提交到 SQL 预编译器，这是一个编程工具。 预编译器扫描程序，查找嵌入式 SQL 语句并对其进行处理。 DBMS 支持的每种编程语言都需要不同的预编译器。 DBMS 产品通常为一种或多种语言（包括 C、Pascal、COBOL、Fortran、Ada、PL/I 和各种汇编语言）提供 precompilers。  
  
2.  预编译器会生成两个输出文件。 第一个文件是源文件，即去除其嵌入式 SQL 语句。 在其位置，预编译器将调用专用 DBMS 例程，这些例程提供程序和 DBMS 之间的运行时链接。 通常，这些例程的名称和调用序列只对预编译器和 DBMS 知道：它们不是 DBMS 的公共接口。 第二个文件是程序中使用的所有嵌入式 SQL 语句的副本。 此文件有时称为数据库请求模块，或 DBRM。  
  
3.  预编译器的源文件输出将提交给主机编程语言 (标准编译器，如 C 或 COBOL 编译器) 。 编译器将处理源代码并生成对象代码作为其输出。 请注意，此步骤与 DBMS 或 SQL 不执行任何操作。  
  
4.  链接器接受编译器生成的对象模块，将它们链接到各种库例程，并生成一个可执行程序。 链接到可执行程序中的库例程包括步骤2中所述的专有 DBMS 例程。  
  
5.  预编译器生成的数据库请求模块将提交到特殊的绑定实用工具。 此实用程序检查 SQL 语句、分析、验证和优化它们，然后为每个语句生成一个访问计划。 结果是整个程序的组合访问计划，表示嵌入式 SQL 语句的可执行版本。 绑定实用工具将计划存储在数据库中，通常将其分配给将使用它的应用程序的名称。 在编译时或运行时是否发生此步骤取决于 DBMS。  
  
 请注意，用于编译嵌入式 SQL 程序的步骤与前面介绍的 [处理 SQL 语句](../../odbc/reference/processing-a-sql-statement.md)的步骤密切相关。 特别要注意的是，预编译器将 SQL 语句与宿主语言代码分隔开来，并且绑定实用工具分析和验证 SQL 语句并创建访问计划。 在执行步骤5的 Dbms 中，在编译时，处理 SQL 语句的前四个步骤发生在编译时，而最后一个步骤 (执行) 在运行时执行。 这会使此类 Dbms 中的查询执行速度非常快。
