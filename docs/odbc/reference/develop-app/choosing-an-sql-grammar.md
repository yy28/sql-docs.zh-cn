---
title: 选择的 SQL 语法 |Microsoft 文档
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
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], SQL grammar
- SQL grammar [ODBC], selecting
ms.assetid: 4e0d189b-e407-47e0-92a9-f9982230dd0e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f571ee10abc26d5de0fb0ff35fc0c931b759f2b4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32911482"
---
# <a name="choosing-an-sql-grammar"></a>选择的 SQL 语法
可以在构造 SQL 语句时使用的第一个决定是要使用的语法。 除了可从各种标准的正文，如 Open Group、 ANSI 和 ISO，语法几乎每个 DBMS 供应商定义其自己的语法，其中每个会稍有不同于标准。  
  
 [附录 c: SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)，描述的最小的 SQL 语法，必须支持所有 ODBC 驱动程序。 此语法是 SQL 92 入门级的子集。 驱动程序可能支持其他语法以符合中间、 完整、 或通过 SQL 92 FIPS 127 2 过渡级别定义。 有关详细信息，请参阅[SQL 最小值语法](../../../odbc/reference/appendixes/sql-minimum-grammar.md)附录 c: SQL 语法和 SQL 92 中。  
  
 附录 C 还定义*转义序列*包含通常可用的语言功能，如外部联接中，标准语法，未涵盖的 SQL 92 语法。 有关详细信息，请参阅[ODBC 转义序列](../../../odbc/reference/appendixes/odbc-escape-sequences.md)附录 c: SQL 语法中, 和[转义序列](../../../odbc/reference/develop-app/escape-sequences.md)，本部分中更高版本。  
  
 为所选的语法会影响该驱动程序如何处理该语句。 驱动程序必须修改 SQL 92 SQL 和到特定于 DBMS 的 SQL 的 ODBC 定义转义序列。 由于大多数 SQL 语法基于一个或多个各种标准，大多数驱动程序将执行很少或没有工作，以满足此要求。 它通常仅包含定义的转义序列搜索通过 ODBC 并将它们替换为特定于 DBMS 的语法。 当驱动程序遇到无法识别的语法时，它假设语法是特定于 DBMS 的并将传递不修改数据源执行的 SQL 语句。  
  
 因此，有两个选项的语法，用于： SQL 92 语法 （和转义序列 ODBC） 和特定 DBMS 的语法。 这二者当中，仅 SQL 92 语法是可互操作，因此所有的可互操作应用程序应使用它。 不是可互操作的应用程序可以使用的 SQL 92 语法或特定于 DBMS 的语法。 特定于 DBMS 的语法有两大优点： 它们可以利用任何功能不受 SQL 92，而且它们是稍更快，因为该驱动程序不需要对其进行修改。 可以通过设置 SQL_ATTR_NOSCAN 语句属性，它将停止搜索并替换转义序列的驱动程序部分强制执行后一种功能。  
  
 如果使用的 SQL 92 语法时，如何它通过调用修改由驱动程序对应用程序可以发现**SQLNativeSql**。 调试应用程序时，这是通常很有用。 **SQLNativeSql**接受 SQL 语句并将其返回后该驱动程序进行了修改。 由于此函数在核心接口一致性级别，它被支持的所有驱动程序。
