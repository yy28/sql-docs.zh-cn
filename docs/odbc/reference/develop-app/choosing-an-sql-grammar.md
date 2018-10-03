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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 670ed0adbbd5ad993af0942d492ee19f75fa9628
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47848025"
---
# <a name="choosing-an-sql-grammar"></a>选择 SQL 语法
可以在构造 SQL 语句时使用的第一个决定是要使用的语法。 除了可从各种标准主体，例如 Open Group、 ANSI 和 ISO 语法几乎每个 DBMS 供应商定义其自己的语法，其中每个稍有不同标准。  
  
 [附录 C:SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)，介绍了所有 ODBC 驱动程序必须都支持的最小 SQL 语法。 此语法是 SQL-92 的入门级的子集。 驱动程序可能支持其他语法，以符合中间、 完整或通过 SQL-92 FIPS 127-2 过渡级别定义。 有关详细信息，请参阅[SQL 最低语法](../../../odbc/reference/appendixes/sql-minimum-grammar.md)附录 c: SQL 语法和 SQL-92 中。  
  
 此外定义了附录 C*转义序列*包含等外部联接中，通常可用的语言功能的标准语法，不包括在 SQL-92 语法。 有关详细信息，请参阅[ODBC 转义序列](../../../odbc/reference/appendixes/odbc-escape-sequences.md)附录 c: SQL 语法，在和[转义序列](../../../odbc/reference/develop-app/escape-sequences.md)，在本部分中更高版本。  
  
 所选的语法会影响该驱动程序如何处理该语句。 SQL-92 SQL 和到如何使用特定于 SQL 的 ODBC 定义的转义序列，则必须修改驱动程序。 由于大多数 SQL 语法基于一个或多个各种标准，因此大多数驱动程序将执行很少或没有工作，以满足此要求。 它通常仅包含搜索定义的转义序列的 ODBC 和它们替换为特定于 DBMS 的语法。 当驱动程序遇到无法识别的语法时，它假定语法是特定于 DBMS 的并将传递而无需执行的数据源的修改 SQL 语句。  
  
 因此，实际上有两个选项的语法，使用： SQL-92 语法 （和 ODBC 转义序列） 和特定于 DBMS 的语法。 这两种，仅 SQL-92 语法是互操作性，因此可互操作的所有应用程序应使用它。 不是可互操作的应用程序可以使用 SQL-92 语法或特定于 DBMS 的语法。 特定于 DBMS 的语法有两大好处： 他们可以利用任何功能不受 SQL-92 和它们是略微更快，因为该驱动程序不需要对其进行修改。 可以通过设置 SQL_ATTR_NOSCAN 语句属性，它将停止搜索并替换转义序列中的驱动程序部分强制执行后一种功能。  
  
 如果使用 SQL-92 语法，则该应用程序可以发现如何修改驱动程序通过调用**SQLNativeSql**。 调试应用程序时，这是通常很有用。 **SQLNativeSql**接受 SQL 语句并将其返回后，驱动程序进行了修改。 由于此函数在核心接口一致性级别，它被支持的所有驱动程序。
