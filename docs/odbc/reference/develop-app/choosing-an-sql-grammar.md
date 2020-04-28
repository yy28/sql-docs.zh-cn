---
title: 选择 SQL 语法 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], SQL grammar
- SQL grammar [ODBC], selecting
ms.assetid: 4e0d189b-e407-47e0-92a9-f9982230dd0e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2ca9911d3c88f2f540ff1332d77a2e1ebc6a4942
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299157"
---
# <a name="choosing-an-sql-grammar"></a>选择 SQL 语法
构造 SQL 语句时要作出的第一决定是使用哪种语法。 除了来自各种标准主体的语法（如开放组、ANSI 和 ISO），几乎每个 DBMS 供应商都定义自己的语法，其中每个都与标准略有不同。  
  
 [附录 C： Sql 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)介绍了所有 ODBC 驱动程序必须支持的最低 SQL 语法。 此语法是 SQL-92 的条目级别的子集。 驱动程序可能支持其他语法，以符合 SQL-92 定义的中间、完整或 FIPS 127-2 转换级别。 有关详细信息，请参阅附录 C： SQL 语法和 SQL-92 中的[SQL 最低语法](../../../odbc/reference/appendixes/sql-minimum-grammar.md)。  
  
 附录 C 还定义了包含 SQL-92 语法未涵盖的常用语言功能（例如外部联接）的标准语法的*转义序列*。 有关详细信息，请参阅本部分后面的附录 C： SQL 语法和[转义序列](../../../odbc/reference/develop-app/escape-sequences.md)中的[ODBC 转义序列](../../../odbc/reference/appendixes/odbc-escape-sequences.md)。  
  
 所选择的语法将影响驱动程序处理该语句的方式。 驱动程序必须将 SQL-92 SQL 和 ODBC 定义的转义序列修改为 DBMS 特定的 SQL。 由于大多数 SQL 语法基于一个或多个不同的标准，因此大多数驱动程序很少或没有工作来满足此要求。 它通常只包含搜索由 ODBC 定义的转义序列，并将其替换为 DBMS 特定的语法。 当驱动程序遇到无法识别的语法时，它假定语法是 DBMS 特定的，并传递 SQL 语句而不修改数据源以进行执行。  
  
 因此，实际上有两种选择要使用的语法： SQL-92 语法（和 ODBC 转义序列）和 DBMS 特定的语法。 对于这两种方法，只有 SQL 92 语法可互操作，因此所有互操作应用程序都应使用它。 不可互操作的应用程序可以使用 SQL-92 语法或 DBMS 特定的语法。 DBMS 特定的语法有两个优点：它们可以利用 SQL-92 未涵盖的任何功能，并且它们的速度更快，因为驱动程序不必修改它们。 可以通过设置 SQL_ATTR_NOSCAN 语句特性来部分强制执行后一项功能，这会阻止驱动程序搜索和替换转义序列。  
  
 如果使用的是 SQL-92 语法，则应用程序可以通过调用**SQLNativeSql**来发现它被驱动程序修改的方式。 调试应用程序时，这通常很有用。 **SQLNativeSql**接受 SQL 语句，并在驱动程序修改后返回该语句。 由于此函数位于核心接口一致性级别，因此它受所有驱动程序的支持。
