---
title: 编译嵌入式 SQL 程序 |微软文档
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
ms.openlocfilehash: eb801dc532009410055b67031b3e036cc6b9c3d0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306528"
---
# <a name="compiling-an-embedded-sql-program"></a>编译嵌入式 SQL 程序
由于嵌入式 SQL 程序包含 SQL 和宿主语言语句的组合，因此无法直接将其提交到主机语言的编译器。 相反，它是通过多步骤过程编译的。 尽管此过程因产品而异，但所有产品的步骤大致相同。  
  
 此图显示了编译嵌入式 SQL 程序所需的步骤。  
  
 ![用于编译嵌入式 SQL 程序的步骤](../../odbc/reference/media/pr02.gif "pr02")  
  
 编译嵌入式 SQL 程序涉及五个步骤：  
  
1.  嵌入的 SQL 程序将提交到 SQL 预编译器，一个编程工具。 预编译器扫描程序，查找嵌入的 SQL 语句，并处理它们。 DBMS 支持的每个编程语言都需要不同的预编译器。 DBMS 产品通常为一种或多种语言提供预编译器，包括 C、Pascal、COBOL、Fortran、Ada、PL/I 和各种汇编语言。  
  
2.  预编译器生成两个输出文件。 第一个文件是源文件，它删除了嵌入的 SQL 语句。 就其位置，预编译器将替换对专有 DBMS 例程的调用，这些例程提供程序和 DBMS 之间的运行时链接。 通常，这些例程的名称和调用序列仅由预编译器和 DBMS 知道;它们不是 DBMS 的公共接口。 第二个文件是程序中使用的所有嵌入式 SQL 语句的副本。 此文件有时称为数据库请求模块或 DBRM。  
  
3.  预编译器的源文件输出将提交到主机编程语言（如 C 或 COBOL 编译器）的标准编译器。 编译器处理源代码并生成对象代码作为其输出。 请注意，此步骤与 DBMS 或 SQL 无关。  
  
4.  链接器接受编译器生成的对象模块，将它们与各种库例程链接，并生成可执行程序。 链接到可执行程序的库例程包括步骤 2 中描述的专有 DBMS 例程。  
  
5.  预编译器生成的数据库请求模块将提交到特殊的绑定实用程序。 此实用程序检查 SQL 语句、分析、验证和优化它们，然后为每个语句生成访问计划。 结果是整个程序的组合访问计划，表示嵌入式 SQL 语句的可执行版本。 绑定实用程序将计划存储在数据库中，通常为其分配将用于使用它的应用程序的名称。 此步骤是在编译时还是运行时执行取决于 DBMS。  
  
 请注意，用于编译嵌入式 SQL 程序的步骤与[处理 SQL 语句](../../odbc/reference/processing-a-sql-statement.md)前面描述的步骤密切相关。 特别是，请注意，预编译器将 SQL 语句与宿主语言代码分开，绑定实用程序解析和验证 SQL 语句并创建访问计划。 在步骤 5 在编译时发生的 DBMS 中，处理 SQL 语句的前四个步骤发生在编译时，而最后一个步骤（执行）发生在运行时。 这具有使查询在此类 DBMS 中执行速度非常快的效果。
