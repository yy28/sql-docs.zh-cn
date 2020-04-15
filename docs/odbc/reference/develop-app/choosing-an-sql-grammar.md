---
title: 选择 SQL 语法 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299157"
---
# <a name="choosing-an-sql-grammar"></a>选择 SQL 语法
构造 SQL 语句时要做出的第一个决定是使用哪个语法。 除了开放组、ANSI 和 ISO 等各种标准机构提供的语法外，几乎每个 DBMS 供应商都定义自己的语法，每个语法与标准略有不同。  
  
 [附录 C：SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)，描述了所有 ODBC 驱动程序必须支持的最小 SQL 语法。 此语法是 SQL-92 条目级别的子集。 驱动程序可能支持其他语法，以符合 SQL-92 定义的中间、完整或 FIPS 127-2 过渡级别。 有关详细信息，请参阅附录 C 中的[SQL 最小语法](../../../odbc/reference/appendixes/sql-minimum-grammar.md)：SQL 语法和 SQL-92。  
  
 附录 C 还定义了包含 SQL-92 语法未涵盖的常用语言功能（如外部联接）的标准语法的*转义序列*。 有关详细信息，请参阅附录 C 中的[ODBC 转义序列](../../../odbc/reference/appendixes/odbc-escape-sequences.md)：SQL 语法和[转义序列](../../../odbc/reference/develop-app/escape-sequences.md)，请参阅本节后面的。  
  
 所选语法会影响驱动程序处理语句的方式。 驱动程序必须修改 SQL-92 SQL 和 ODBC 定义的转义序列到特定于 DBMS 的 SQL。 由于大多数 SQL 语法基于一个或多个各种标准，因此大多数驱动程序很少或根本没有工作来满足此要求。 它通常只包括搜索由 ODBC 定义的转义序列，并用特定于 DBMS 的语法替换它们。 当驱动程序遇到它无法识别的语法时，它假定该语法特定于 DBMS，并且在不修改数据源的情况下传递 SQL 语句以执行。  
  
 因此，实际上有两种语法可供选择：SQL-92语法（和 ODBC 转义序列）和特定于 DBMS 的语法。 在两者中，只有 SQL-92 语法是可互操作的，因此所有可互操作的应用程序都应该使用它。 不可互操作的应用程序可以使用 SQL-92 语法或特定于 DBMS 的语法。 特定于 DBMS 的语法有两个优点：它们可以利用 SQL-92 未涵盖的任何功能，并且它们的速度略快，因为驱动程序不必修改它们。 后一个功能可以通过设置SQL_ATTR_NOSCAN语句属性部分强制执行，该属性阻止驱动程序搜索和替换转义序列。  
  
 如果使用 SQL-92 语法，应用程序可以通过调用**SQLNativeSql**来发现驱动程序如何修改它。 这在调试应用程序时通常很有用。 **SQLNativeSql**接受 SQL 语句，并在驱动程序修改后返回它。 由于此函数处于 Core 接口一致性级别，因此所有驱动程序都支持此功能。
