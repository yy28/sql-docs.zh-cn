---
title: ODBC 程序员&#39;的参考 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c83a7de609d200da2957a65b9325d031eda49780
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63273042"
---
# <a name="odbc-programmer39s-reference"></a>ODBC 程序员&#39;的参考
*ODBC 程序员参考*包含以下各节。  
  
-   [What's New in ODBC 3.8](../../odbc/reference/what-s-new-in-odbc-3-8.md)列出已添加 Windows 8 SDK 中的新 ODBC 功能。  
  
-   [示例 ODBC 程序](../../odbc/reference/sample-odbc-program.md)显示示例 ODBC 程序。  
  
-   [ODBC 简介](../../odbc/reference/introduction-to-odbc.md)提供简要的历史记录的结构化查询语言和 ODBC 和 ODBC 接口的概念信息。  
  
-   [开发应用程序](../../odbc/reference/develop-app/developing-applications.md)包含有关开发使用 ODBC 接口和实现它的驱动程序的应用程序的信息。  
  
-   [安装和配置 ODBC 软件](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md)提供有关安装和设置 DLL 函数引用的信息。  
  
-   [开发 ODBC 驱动程序](../../odbc/reference/develop-driver/developing-an-odbc-driver.md)包含编写驱动程序的信息。  
  
-   [API 参考](../../odbc/reference/syntax/odbc-reference.md)包含的语法和语义信息的所有 ODBC 函数。  
  
-   [ODBC 附录](../../odbc/reference/appendixes/odbc-appendixes.md)包含技术详细信息和引用表的 ODBC 错误代码、 数据类型和 SQL 语法。  
  
## <a name="working-with-the-odbc-documentation"></a>使用 ODBC 文档  
 ODBC 接口用于与 C 编程语言一起使用。 ODBC 接口的使用涉及三大块：SQL 语句，ODBC 函数调用，以及 C 编程。 本文档的假设条件如下：  
  
-   C 编程语言的应用知识。  
  
-   常规 DBMS 知识和熟悉 SQL。  
  
 使用以下排字约定。  
  
|格式|用于|  
|------------|--------------|  
|SELECT * FROM|大写的字母指示 SQL 语句、 宏名称和操作系统命令级别使用的术语。|  
|`RETCODE SQLFetch(hdbc)`|Monospace 字体用于示例命令行和程序代码。|  
|argument|斜体字表明以编程方式参数，用户或应用程序必须提供，或 word 强调的信息。|  
|**SQLEndTran**|粗体表示必须按所示，其中包括函数名称的原样键入的语法。|  
|&#124;|竖线用于分隔两个互斥选项的语法行中。|  
|...|省略号表示自变量可以重复多次。|  
|. . .|三个点的列指示延续前面的代码行。|  
  
## <a name="about-the-code-examples"></a>有关代码示例  
 本指南中的代码示例旨在仅用于说明目的。 因为它们编写主要是为了演示 ODBC 原则，效率有时会在一旁为了清楚起见。 此外，代码的整个部分有时省略了为清楚起见。 其中包括非 ODBC 函数 （其名称不以"SQL"开头的那些函数） 和大多数的错误处理的定义。  
  
 所有代码示例都使用 ANSI 字符串和相同的数据库架构，而会显示在开头[目录函数](../../odbc/reference/develop-app/catalog-functions.md)。  
  
## <a name="recommended-reading"></a>推荐阅读的主题  
 有关 SQL 的详细信息，以下标准有：  
  
-   数据库语言-SQL 完整性增强功能，ANSI，1989 ANSI X3.135 1989 与。  
  
-   数据库语言-SQL:ANSI X3H2 和 ISO/IEC JTC1/SC21/WG3 9075:1992 (SQL-92)。  
  
-   Open Group 数据管理：结构化的查询语言 (SQL)，版本 2 (Open Group，1996年)。  
  
 除了标准和特定于供应商 SQL 参考线，很多书描述 SQL，包括：  
  
-   日期，C.J.，与 Darwen，Hugh:*SQL 标准的指南*(Addison Wesley，1993年)。  
  
-   Emerson、 Sandra L.、 Darnovsky、 Marcy 和 Bowman，Judith s。:*实际 SQL 手册*(Addison Wesley，1989年)。  
  
-   Groff，James R.和 Weinberg，Paul N.:*使用 SQL* (Osborne Mcgraw-hill，1990年)。  
  
-   Gruber，Martin:*了解 SQL* (Sybex，1990年)。  
  
-   Hursch，Jack L.和菲 j.:*SQL、 结构化的查询语言*(选项卡 Books，1988年)。  
  
-   Melton、 Jim 和 Simon，Alan R.:*了解新的 SQL:完整指南*（Morgan Kaufmann 出版社，1993年）。  
  
-   Pascal，卡尔蔡司工业：*SQL 和关系的基础知识*（M 和 T 书籍，1990年）。  
  
-   Trimble、 J.Harvey，Jr.和 Chappell，David:*SQL 的视频介绍*(Wiley，1989)。  
  
-   Van der Lan，Rick F.:*简介 SQL* (Addison Wesley，1988年)。  
  
-   Vang，Soren:*SQL 和关系数据库*(Microtrend Books，1990年)。  
  
-   Viescas，John:*SQL 快速参考指南*(Microsoft Corp.，1989年)。  
  
 有关事务处理的其他信息，请参阅：  
  
-   Gray, J. N. 和 Reuter，Andreas:*事务处理：概念和技术*（Morgan Kaufmann 出版社，1993年）。  
  
-   Hackathorn，Richard D.:*企业数据库连接*(Wiley & 儿子，1993年)。  
  
 有关调用级别接口的详细信息，以下标准有：  
  
-   打开组*数据管理：SQL 调用级别接口 (CLI) C451* (Open Group，1995年)。  
  
-   ISO/IEC 9075-3:1995，调用级别接口 (SQL/CLI)。  
  
 有关 ODBC 的其他信息，大量书籍可供使用，包括：  
  
-   Geiger Kyle:*在 ODBC* (Microsoft Press®，1995年)。  
  
-   Gryphon、 Robert、 Charpentier、 l u c、 Oelschlager、 Jon、 Shoemaker，Andrew，交叉，Jim，和 Lilley、 Albert W.:*使用 ODBC 2* (Que，1994年)。  
  
-   约翰斯顿、 Tom 和 Osborne，标记：*ODBC 开发人员指南*（Howard W.Sam 和公司，1994年）。  
  
-   北部，Ken:*Windows 多 DBMS 编程：使用C++，Visual Basic、 ODBC、 OLE 2 和 Tools for DBMS 项目*（John Wiley 和儿子，Inc.，1995年）。  
  
-   Stegman、 Michael O.、 Signore、 Robert 和 Creamer，John:*ODBC 解决方案、 开放式数据库连接中的分布式环境*(2.0》(mcgraw-Hill，1995年)。  
  
-   Welch，Keith:*使用 ODBC 2* (Que，1994年)。  
  
-   Whiting，帐单：*自学 ODBC 二十一个天内*（Howard W.Sam 和公司，1994年）。
