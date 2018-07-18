---
title: 编译嵌入式的 SQL 程序 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- compiling embedded SQL programs [ODBC]
- embedded SQL [ODBC]
ms.assetid: 9e94146a-5b80-4a01-b586-1e03ff05b9ac
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4e4b89a65475b35b50a968b9497c6d90574c6738
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32908932"
---
# <a name="compiling-an-embedded-sql-program"></a>编译嵌入式的 SQL 程序
嵌入式的 SQL 程序包含的 SQL 和主机语言语句混合，因为它不能直接提交到主机语言使用的编译器。 相反，它是通过一个多步骤过程编译。 尽管此过程的不同产品产品，的步骤都大致相同的所有产品。  
  
 此图显示编译嵌入式的 SQL 程序所需的步骤。  
  
 ![若要编译的嵌入式的 SQL 程序的步骤](../../odbc/reference/media/pr02.gif "pr02")  
  
 在编译的嵌入式的 SQL 程序包括五个步骤：  
  
1.  嵌入式的 SQL 程序提交到 SQL 预编译器，编程的工具。 预编译器扫描程序，查找嵌入的 SQL 语句，并处理订单。 需要为每个支持的 DBMS 的编程语言不同预编译器。 DBMS 产品通常提供了一个或多个语言版本，包括 C、 Pascal、 COBOL、 Fortran、 Ada、 PL 的 precompilers / I，和各种程序集语言。  
  
2.  预编译器将生成两个输出文件。 第一个文件是源文件，其嵌入的 SQL 语句中提取出来。 在它们的位置，预编译器替换对提供程序和 DBMS 之间的运行时链接的专有 DBMS 例程的调用。 通常情况下，仅供预编译器和 DBMS; 已知的名称和这些例程的调用序列它们不是 DBMS 的公共接口。 第二个文件是一份在程序中使用所有嵌入式 SQL 语句。 此文件有时称为数据库请求模块或 DBRM。  
  
3.  从预编译器输出的源文件提交给标准编译器进行编程语言 （如 C 或 COBOL 编译器） 的主机。 编译器处理的源代码，并生成作为其输出的对象代码。 请注意，此步骤有执行任何操作以 DBMS 或 SQL 完成。  
  
4.  链接器接受由编译器生成的对象模块、 使用各种库例程，链接它们并生成可执行程序。 链接到可执行程序的库例程包括在步骤 2 中所述的专有 DBMS 例程。  
  
5.  由预编译器生成的数据库请求模块提交到一个特殊绑定实用程序。 此实用程序检查 SQL 语句、 分析、 验证，并优化，然后生成每个语句的访问计划。 结果是针对整个程序，表示嵌入的 SQL 语句的可执行文件版本的组合的访问计划。 绑定实用工具将计划存储在数据库中，通常将其分配将使用它的应用程序的名称。 是否此步骤将在编译时或运行的时依赖于 DBMS。  
  
 请注意，用于编译的嵌入式的 SQL 程序的步骤使用前面部分中所述的步骤非常密切关联[处理 SQL 语句](../../odbc/reference/processing-a-sql-statement.md)。 具体而言，请注意，预编译器分隔的 SQL 语句从主机语言代码，并且绑定实用程序分析并验证 SQL 语句和创建访问计划。 Dbms 其中第 5 步发生在编译时，在处理 SQL 语句的前四个步骤发生在编译时，最后一步 （执行） 发生时在运行时。 在这种 Dbms 非常快速地进行查询执行效果。
