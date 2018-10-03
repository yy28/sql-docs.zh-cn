---
title: 编译嵌入式的 SQL 程序 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc8133241ad0b76579e87164350a5c6fe2a39f2e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47600905"
---
# <a name="compiling-an-embedded-sql-program"></a>编译嵌入式 SQL 程序
嵌入式的 SQL 程序包含多种 SQL 和主机语言语句，因为它不能直接提交到主机语言的编译器。 相反，它是通过一个多步骤过程编译。 尽管此过程不同产品产品，但步骤是大致相同的所有产品。  
  
 此图显示编译嵌入式的 SQL 程序所需的步骤。  
  
 ![编译嵌入式的 SQL 程序的步骤](../../odbc/reference/media/pr02.gif "pr02")  
  
 在编译嵌入式的 SQL 程序包括五个步骤：  
  
1.  嵌入式的 SQL 程序提交到 SQL 使用预编译器，编程的工具。 使用预编译器扫描程序、 查找嵌入的 SQL 语句，并对其进行处理。 需要支持的 DBMS 每种编程语言不同使用预编译器。 DBMS 产品通常会提供一个或多个语言，包括 C、 Pascal、 COBOL、 Fortran、 Ada、 PL precompilers / I，和各种程序集语言。  
  
2.  使用预编译器会生成两个输出文件。 第一个文件是源文件，其嵌入的 SQL 语句中去除。 在其位置，使用预编译器将替换为对提供程序和 DBMS 之间的运行时链接的专用 DBMS 例程的调用。 通常情况下，仅对使用预编译器和 DBMS; 已知的名称和这些例程的调用序列它们不是向 DBMS 的公共接口。 第二个文件是在程序中使用所有嵌入式 SQL 语句的副本。 此文件有时称为数据库请求模块或 DBRM。  
  
3.  使用预编译器的源代码文件输出到标准编译器提交进行编程语言 （例如 C 或 COBOL 编译器） 的主机。 编译器处理源代码并生成作为其输出的对象代码。 请注意，此步骤不执行任何操作与 DBMS 或 SQL。  
  
4.  链接器接受由编译器生成的对象模块中，链接到各种库例程，并生成可执行程序。 链接到可执行程序的库例程包括在步骤 2 中所述的专用 DBMS 例程。  
  
5.  通过使用预编译器生成的数据库请求模块提交到一个特殊的绑定实用程序。 此实用程序将检查 SQL 语句、 分析、 验证和优化它们，然后会生成每个语句的访问计划。 结果是整个程序，它表示嵌入的 SQL 语句的可执行文件版本的合并的访问计划。 绑定实用程序将该计划存储在数据库中，通常将使用它的应用程序的名称。 是否执行此步骤，在编译时或运行的时依赖于 DBMS。  
  
 请注意，将与前面所述的步骤十分紧密地关联用于编译嵌入式的 SQL 程序的步骤[处理 SQL 语句](../../odbc/reference/processing-a-sql-statement.md)。 具体而言，请注意，使用预编译器用于分隔主机语言代码，从 SQL 语句和绑定实用程序分析和验证 SQL 语句并创建访问计划。 Dbms 第 5 步，会发生在编译时中的前四个步骤的处理 SQL 语句发生在编译时，在最后一步 （执行） 时会在运行时。 进行此类非常快的 Dbms 中的查询执行效果。
