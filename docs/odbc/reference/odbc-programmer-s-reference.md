---
title: ODBC 程序员&#39;s 参考 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], reference
ms.assetid: b33c3c43-ae66-44a3-be17-9cd82624dd96
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6a9ca32627b9703465dcfca554fdc32ae01442e7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280507"
---
# <a name="odbc-programmer39s-reference"></a>ODBC 程序员&#39;s 参考
*ODBC 程序员参考*包含以下各节。  
  
-   [ODBC 3.8 中的新增](../../odbc/reference/what-s-new-in-odbc-3-8.md)功能列出了在 WINDOWS 8 SDK 中添加的新 ODBC 功能。  
  
-   [示例 Odbc 程序](../../odbc/reference/sample-odbc-program.md)提供了一个示例 odbc 程序。  
  
-   [Odbc 简介](../../odbc/reference/introduction-to-odbc.md)提供了结构化查询语言和 odbc 的简短历史记录，以及有关 ODBC 接口的概念信息。  
  
-   [开发应用程序](../../odbc/reference/develop-app/developing-applications.md)包含有关开发使用 ODBC 接口的应用程序和实现它的驱动程序的信息。  
  
-   [安装和配置 ODBC 软件](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md)会提供有关安装和设置 DLL 函数引用的信息。  
  
-   [开发 ODBC 驱动程序](../../odbc/reference/develop-driver/developing-an-odbc-driver.md)包含有关编写驱动程序的信息。  
  
-   [API 参考](../../odbc/reference/syntax/odbc-reference.md)包含所有 ODBC 函数的语法和语义信息。  
  
-   [Odbc 附录](../../odbc/reference/appendixes/odbc-appendixes.md)包含有关 odbc 错误代码、数据类型和 SQL 语法的技术详细信息和参考表。  
  
## <a name="working-with-the-odbc-documentation"></a>使用 ODBC 文档  
 ODBC 接口用于与 C 编程语言一起使用。 ODBC 接口的使用涉及三大块：SQL 语句、ODBC 函数调用，以及 C 编程。 本文档假定以下内容：  
  
-   C 编程语言的工作知识。  
  
-   一般的 DBMS 知识和熟悉 SQL 的知识。  
  
 使用以下版式约定。  
  
|格式|用于|  
|------------|--------------|  
|SELECT * FROM|大写字母表示在操作系统命令级别使用的 SQL 语句、宏名称和术语。|  
|`RETCODE SQLFetch(hdbc)`|等宽字体用于示例命令行和程序代码。|  
|argument |斜体词语指示编程参数、用户或应用程序必须提供的信息或字词强调。|  
|**SQLEndTran**|粗体表示必须严格按所示方式键入语法，包括函数名称。|  
|&#124;|一个竖线用于分隔语法行中的两个互斥选项。|  
|...|省略号指示参数可以重复多次。|  
|. . .|三个点的列指示之前的代码行的继续符。|  
  
## <a name="about-the-code-examples"></a>关于代码示例  
 本指南中的代码示例仅供说明之用。 由于它们主要是为了演示 ODBC 原则而编写的，因此，在清晰的兴趣情况下，可能会保留效率。 此外，为清楚起见，有时省略了代码的整个部分。 其中包括非 ODBC 函数（其名称不以 "SQL" 开头的函数）的定义和大多数错误处理。  
  
 所有代码示例都使用 ANSI 字符串和相同的数据库架构，这会显示在[目录函数](../../odbc/reference/develop-app/catalog-functions.md)的开头。  
  
## <a name="recommended-reading"></a>推荐阅读的主题  
 有关 SQL 的详细信息，请访问以下标准：  
  
-   数据库语言-包含完整性增强功能的 SQL、ANSI、1989 ANSI X 3.135-1989 年。  
  
-   数据库语言-SQL： ANSI X3H2 and ISO/IEC JTC1/SC21/WG3 9075:1992 （SQL-92）。  
  
-   打开组，数据管理：结构化查询语言（SQL），版本2（开放组，1996）。  
  
 除了标准和特定于供应商的 SQL 指南之外，许多书籍介绍了 SQL，其中包括：  
  
-   日期，c. J，with Darwen，Hugh： *SQL 标准指南*（Addison-Wesley，1993）。  
  
-   Emerson，Sandra，Darnovsky，Marcy，and Bowman，Judith S：*切实可行的 SQL 手册*（Addison-Wesley，1989）。  
  
-   Groff、James R 和 Weinberg，Paul n.：*使用 SQL* （Osborne McGraw-峰，1990）。  
  
-   Gruber，圣马丁：*了解 SQL* （Sybex，1990）。  
  
-   Hursch、插孔 L. 和 Carolyn J.： *SQL，结构化查询语言*（选项卡书籍，1988）。  
  
-   Melton、Jim 和 Simon、Alan R。：*了解新的 SQL：完整的指南*（Morgan Kaufmann publisher，1993）。  
  
-   Pascal、Fabian： *SQL 和关系基础知识*（M & 手册，1990）。  
  
-   Trimble、Harvey、Jr 和 Chappell，David： *SQL 的直观介绍*（Wiley，1989）。  
  
-   Van der Lan，Rick F。： *SQL 简介*（Addison-Wesley，1988）。  
  
-   Vang、Soren： *SQL 和关系数据库*（Microtrend 书籍，1990）。  
  
-   Viescas，John： *SQL 快速参考指南*（Microsoft Corp.，1989）。  
  
 有关事务处理的其他信息，请参阅：  
  
-   灰色，J N。 和 Reuter，Andreas：*事务处理：概念和技术*（Morgan Kaufmann 发布者，1993）。  
  
-   Hackathorn，Richard d.*企业数据库连接*（Wiley & 专家，1993）。  
  
 有关调用级别接口的详细信息，请使用以下标准：  
  
-   打开组，*数据管理： SQL 调用级别接口（CLI），C451* （打开组，1995）。  
  
-   ISO/IEC 9075-3:1995、调用级别接口（SQL/CLI）。  
  
 有关 ODBC 的其他信息，可以使用多个书籍，包括：  
  
-   Geiger，Kyle： *ODBC 内*（微软出版社®，1995）。  
  
-   Gryphon、Robert、Charpentier、Jean-luc、Oelschlager、Jon、Shoemaker、Andrew、叉、Jim 和 Lilley，Albert W：*使用 ODBC 2* （查询，1994）。  
  
-   约翰约翰，Tom 和 Osborne，Mark： *ODBC 开发人员指南*（Howard & 公司，1994）。  
  
-   北部，Ken： *Windows 多 DBMS 编程：使用 c + +、Visual Basic、ODBC、OLE 2 和用于 DBMS 项目的工具*（John Wiley & 专家，inc.，1995）。  
  
-   Stegman、迈克尔 Signore、Robert 和 Creamer，John： *ODBC 解决方案，开放分布式环境中的数据库连接*（McGraw-峰，1995）。  
  
-   Welch，Keith：*使用 ODBC 2* （查询，1994）。  
  
-   Whiting，比尔· *Teach Yourself ODBC in Twenty-One Days*比尔··· Howard & 公司，1994）。
