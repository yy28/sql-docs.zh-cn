---
title: "ODBC 程序员 &#39; s 引用 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC], reference
ms.assetid: b33c3c43-ae66-44a3-be17-9cd82624dd96
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3c5440b6cfc25665156986a0aed99a1fa05e16be
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-programmer39s-reference"></a>ODBC 程序员 &#39; s 引用
*ODBC 程序员参考*包含以下各节。  
  
-   [What's New in ODBC 3.8](../../odbc/reference/what-s-new-in-odbc-3-8.md)列出已添加 Windows 8 SDK 中的新 ODBC 功能。  
  
-   [示例 ODBC 程序](../../odbc/reference/sample-odbc-program.md)演示一个示例 ODBC 程序程序。  
  
-   [简介 ODBC](../../odbc/reference/introduction-to-odbc.md)提供简要的历史记录的结构化查询语言和 ODBC 和 ODBC 接口的概念性信息。  
  
-   [开发应用程序](../../odbc/reference/develop-app/developing-applications.md)包含有关开发使用 ODBC 接口和驱动程序实现它的应用程序的信息。  
  
-   [安装和配置 ODBC 软件](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md)提供有关安装和设置 DLL 的函数参考信息。  
  
-   [开发 ODBC 驱动程序](../../odbc/reference/develop-driver/developing-an-odbc-driver.md)包含编写驱动程序的信息。  
  
-   [API 参考](../../odbc/reference/syntax/odbc-reference.md)包含语法和语义信息所有 ODBC 函数。  
  
-   [ODBC 附录](../../odbc/reference/appendixes/odbc-appendixes.md)包含技术详细信息表和引用表 ODBC 错误代码、 数据类型和 SQL 语法。  
  
## <a name="working-with-the-odbc-documentation"></a>使用 ODBC 文档  
 ODBC 接口用于 C 编程语言。 使用 ODBC 接口跨越三个区域： ODBC 的 SQL 语句的函数调用及 C 编程。 本文档假设如下：  
  
-   C 编程语言的应用知识。  
  
-   常规 DBMS 知识和熟悉 SQL。  
  
 将使用以下排字约定。  
  
|格式|用于|  
|------------|--------------|  
|选择 * 从|大写字母指示 SQL 语句、 宏名称和在操作系统命令级别使用的术语。|  
|`RETCODE SQLFetch(hdbc)`|等宽字体用于示例命令行和程序代码。|  
|*自变量*|斜体字表示编程参数，用户或应用程序必须提供，或者 word 强调的信息。|  
|**SQLEndTran**|粗体类型指示必须严格按所示，包括函数名称键入语法。|  
|&#124;|竖线分隔的语法行中的两个互相排斥的选项。|  
|...|省略号表示自变量可以重复多次。|  
|实例时都提供 SQL Server 登录名。 。 实例时都提供 SQL Server 登录名。|三个点的一列指示延续前面的代码行。|  
  
## <a name="about-the-code-examples"></a>有关代码示例  
 本指南中的代码示例旨在仅用于说明目的。 因为它们编写主要是为了演示 ODBC 原则，效率有时在一旁为了清楚起见。 此外，代码的整个部分有时省略了为清楚起见。 其中包括非 ODBC 函数 （其名称不会启动与"SQL"这些函数） 和大多数的错误处理的定义。  
  
 所有的代码示例使用 ANSI 字符串和相同的数据库架构，启动时显示[目录函数](../../odbc/reference/develop-app/catalog-functions.md)。  
  
## <a name="recommended-reading"></a>推荐阅读的主题  
 有关 SQL 的详细信息，以下标准有：  
  
-   使用完整性增强功能，ANSI，1989 ANSI X3.135 1989 数据库语言 — SQL。  
  
-   数据库语言-SQL: ANSI X3H2 和 ISO/IEC JTC1/SC21/WG3 9075:1992 (SQL 92)。  
  
-   打开组、 数据管理： 结构化的查询语言 (SQL) 版本 2 (Open Group，1996年)。  
  
 除了标准和特定于供应商 SQL 指南，很多书描述 SQL，包括：  
  
-   日期、 C.J.，与 Darwen，Hugh: *SQL 标准的指南*(Addison Wesley，1993年)。  
  
-   坚持、 Sandra l。、 Darnovsky、 Marcy 和 Bowman，Judith s。:*实际 SQL 手册*(Addison Wesley，1989年)。  
  
-   Groff，James。 和 Weinberg，Paul N.:*使用 SQL* （Osborne McGraw-峰，1990年）。  
  
-   Gruber，Martin:*了解 SQL* (Sybex，1990年)。  
  
-   Hursch 上, 插座 l。 和菲 J.: *SQL、 结构化的查询语言*（选项卡丛书，1988年）。  
  
-   Melton、 Jim 和人 Simon Alan。:*了解新的 SQL： 完整指南*（Morgan Kaufmann 发布者，1993年）。  
  
-   Pascal、 Fabian: *SQL 和关系的基础知识*(& T 丛书，1990年)。  
  
-   Trimble、 j.Harvey，先生和 Chappell，David: *Visual SQL 简介*(Wiley，1989)。  
  
-   Van der Lan、 Rick F.:*简介 SQL* (Addison Wesley，1988年)。  
  
-   Vang、 Soren: *SQL 和关系数据库*（Microtrend 丛书，1990年）。  
  
-   Viescas，John: *SQL 快速参考指南*(Microsoft Corp.，1989年)。  
  
 有关处理的事务的其他信息，请参阅：  
  
-   灰色，j.n。 和 Reuter、 Andreas:*事务处理： 概念和技术*（Morgan Kaufmann 发布者，1993年）。  
  
-   Hackathorn，Richard D.:*企业数据库连接*(Wiley & 儿子，1993年)。  
  
 有关调用级接口的详细信息，以下标准有：  
  
-   Open Group*数据管理： SQL 调用级别界面 (CLI)，C451* （打开组，1995年）。  
  
-   ISO/IEC 9075-3:1995，调用级接口 (SQL/CLI)。  
  
 有关 ODBC 的其他信息，有多种丛书都是可用，包括：  
  
-   Geiger Kyle:*内 ODBC* (Microsoft Press®，1995年)。  
  
-   Gryphon、 Robert、 Charpentier、 Luc、 Oelschlager、 Jon、 Shoemaker，Andrew，交叉，Jim，和 Lilley、 说 W.:*使用 ODBC 2* （汉阳，1994年）。  
  
-   Johnston、 Tom 和 Osborne，标记： *ODBC 开发人员指南*(Howard W.Sam & 公司，1994年)。  
  
-   北部，Ken: *Windows 多 DBMS 编程： 为 DBMS 项目使用 c + +、 Visual Basic、 ODBC、 OLE 2 和工具*(John Wiley & 儿子，Inc.，1995年)。  
  
-   Stegman、 Michael o。、 Signore、 Robert 和 Creamer，John: *ODBC 解决方案、 开放式数据库连接中的分布式环境*（McGraw 峰，1995年）。  
  
-   图案来工作，Keith:*使用 ODBC 2* （汉阳，1994年）。  
  
-   Whiting，帐单：*自学 ODBC 在 21 天内*(Howard W.Sam & 公司，1994年)。

