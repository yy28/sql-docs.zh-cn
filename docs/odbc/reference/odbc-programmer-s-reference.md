---
title: ODBC 程序员&#39;参考 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280507"
---
# <a name="odbc-programmer39s-reference"></a>ODBC 程序员&#39;参考
*ODBC 程序员的参考*包含以下部分。  
  
-   [ODBC 3.8 中的新增](../../odbc/reference/what-s-new-in-odbc-3-8.md)功能列出了 Windows 8 SDK 中添加的新 ODBC 功能。  
  
-   [示例 ODBC 计划](../../odbc/reference/sample-odbc-program.md)提供了 ODBC 计划示例。  
  
-   [ODBC 简介](../../odbc/reference/introduction-to-odbc.md)提供了结构化查询语言和 ODBC 的简要历史记录，以及有关 ODBC 接口的概念信息。  
  
-   [开发应用程序](../../odbc/reference/develop-app/developing-applications.md)包含有关开发使用 ODBC 接口的应用程序的信息以及实现该应用程序的驱动程序。  
  
-   [安装和配置 ODBC 软件](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md)提供有关安装的信息和设置 DLL 功能参考。  
  
-   [开发 ODBC 驱动程序](../../odbc/reference/develop-driver/developing-an-odbc-driver.md)包含有关编写驱动程序的信息。  
  
-   [API 参考](../../odbc/reference/syntax/odbc-reference.md)包含所有 ODBC 函数的语法和语义信息。  
  
-   [ODBC 附录](../../odbc/reference/appendixes/odbc-appendixes.md)包含 ODBC 错误代码、数据类型和 SQL 语法的技术详细信息和参考表。  
  
## <a name="working-with-the-odbc-documentation"></a>使用 ODBC 文档  
 ODBC 接口用于与 C 编程语言一起使用。 ODBC 接口的使用涉及三大块：SQL 语句、ODBC 函数调用，以及 C 编程。 本文档假定以下内容：  
  
-   C编程语言的工作知识。  
  
-   一般 DBMS 知识和对 SQL 的熟悉程度。  
  
 使用以下排版约定。  
  
|格式|用于|  
|------------|--------------|  
|选择 = 从|大写字母表示 SQL 语句、宏名称和在操作系统命令级别使用的术语。|  
|`RETCODE SQLFetch(hdbc)`|单一空间字体用于示例命令行和程序代码。|  
|argument**|斜体字表示编程参数、用户或应用程序必须提供的信息或单词强调。|  
|**SQLEndTran**|粗体类型表示语法必须完全按照所示类型进行键入，包括函数名称。|  
|&#124;|垂直条分隔语法行中的两个互斥选项。|  
|...|省略号表示参数可以重复多次。|  
|. . .|三个点的列表示前几行代码的延续。|  
  
## <a name="about-the-code-examples"></a>关于代码示例  
 本指南中的代码示例仅用于说明目的。 因为它们主要是为了展示 ODBC 原则，因此有时为了明确起见，效率被搁置一边。 此外，为了清楚起见，有时省略了代码的整个部分。 其中包括非 ODBC 函数（名称不以"SQL"开头的函数）和大多数错误处理的定义。  
  
 所有代码示例都使用 ANSI 字符串和相同的数据库架构，这在[目录函数](../../odbc/reference/develop-app/catalog-functions.md)的开头显示。  
  
## <a name="recommended-reading"></a>推荐阅读的主题  
 有关 SQL 的详细信息，可以使用以下标准：  
  
-   数据库语言 - 具有完整性增强的 SQL，ANSI，1989 ANSI X3.135-1989。  
  
-   数据库语言 - SQL：ANSI X3H2 和 ISO/IEC JTC1/SC21/WG3 9075：1992 （SQL-92）。  
  
-   开放组，数据管理：结构化查询语言（SQL），版本 2（开放组，1996 年）。  
  
 除了标准和特定于供应商的 SQL 指南外，许多书籍还描述了 SQL，包括：  
  
-   日期，C.J.，达文，休 *：SQL标准指南*（艾迪森-韦斯利，1993年）。  
  
-   艾默生、桑德拉·L、达诺夫斯基、马西和鲍曼，朱迪思：*实用SQL手册*（艾迪森-韦斯利，1989年）。  
  
-   格罗夫，詹姆斯R.和文伯格，保罗N.：*使用SQL（* 奥斯本麦格劳希尔，1990年）。  
  
-   格鲁伯，马丁：*理解*SQL（Sybex，1990年）。  
  
-   赫尔施，杰克L.和卡罗琳*J.：SQL，结构化查询语言*（TAB书籍，1988年）。  
  
-   梅尔顿、吉姆和西蒙，艾伦：*了解新的SQL：一个完整的指南*（摩根考夫曼出版社，1993年）。  
  
-   帕斯卡尔，法比安 *：SQL和关系基础知识*（M&T书籍，1990年）。  
  
-   特林布尔，小J.哈维和查佩尔，大卫 *：SQL的视觉介绍*（威利，1989年）。  
  
-   范德兰斯，里克*F.：SQL简介*（艾迪森-韦斯利，1988年）。  
  
-   Vang， 索伦 *：SQL 和关系数据库*（微趋势书籍，1990 年）。  
  
-   约翰·维斯卡斯 *：SQL 快速参考指南*（微软公司，1989 年）。  
  
 有关事务处理的其他信息，请参阅：  
  
-   格雷，J.N. 和Reuter，Andreas：*交易处理：概念和技术*（摩根·考夫曼出版社，1993年）。  
  
-   哈克索恩，理查德D.：*企业数据库连接*（威利&儿子，1993年）。  
  
 有关呼叫级接口的详细信息，请提供以下标准：  
  
-   打开组，*数据管理：SQL 呼叫级别接口 （CLI），C451（* 开放组，1995 年）。  
  
-   ISO/IEC 9075-3：1995，呼叫级接口（SQL/CLI）。  
  
 有关 ODBC 的更多信息，可查阅多本书，包括：  
  
-   盖格，凯尔 *：ODBC内部*（微软出版社®，1995年）。  
  
-   格里芬，罗伯特，查彭蒂埃，吕克，欧尔施拉格，乔恩，鞋匠，安德鲁，克罗斯，吉姆和利利，阿尔伯特W.：*使用ODBC* 2（Que，1994年）。  
  
-   约翰斯顿，汤姆和奥斯本，马克 *：ODBC开发者指南*（霍华德·萨姆斯&公司，1994年）。  
  
-   北，肯 *：Windows多DBMS编程：使用C++、视觉基础、ODBC、OLE 2 和 DBMS 项目工具*（John Wiley & Sons， Inc.，1995 年）。  
  
-   斯特格曼、迈克尔·奥、索多洛、罗伯特和梅勒，约翰 *：ODBC 解决方案，分布式环境中的开放数据库连接*（McGraw-Hill，1995 年）。  
  
-   韦尔奇，基思：*使用ODBC* 2（Que，1994年）。  
  
-   惠廷，比尔：*在二十一天内自学ODBC（* 霍华德·萨姆斯&公司，1994年）。
