---
title: 标识符参数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- identifier arguments [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], identifier
ms.assetid: b9de003f-cb49-4dec-b528-14a5b8ff12bd
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a4aed40268b5e9bb3dd3d4a37d43b45a7b6856ef
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="identifier-arguments"></a>标识符的自变量
如果带引号的标识符参数中的字符串，该驱动程序中删除前导空格和尾随空格，并将按原义在引号内的字符串。 如果不带引号的字符串，该驱动程序将删除尾随空白和折叠为大写的字符串。 设置标识符的参数为 null 指针返回 SQL_ERROR 和 SQLSTATE HY009 （不允许使用 null 指针），除非自变量是一个目录名称，并且不支持目录。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE，这些自变量将被视为标识符自变量。 在这种情况下，下划线 (_) 和百分号 （%） 将被视为不是作为搜索模式字符的实际字符。 这些自变量被视为普通自变量或 pattern 参数，具体取决于自变量，如果此属性设置为 SQL_FALSE。  
  
 虽然必须在 SQL 语句中引用包含特殊字符的标识符，它们必须不加引号时传递作为目录函数自变量，因为按照字义解释引号字符传递给目录函数。 例如，假定标识符引号字符 (这是特定于驱动程序和通过返回**SQLGetInfo**) 是双引号 （"）。 首次调用**SQLTables**返回的结果集包含 Accounts Payable 表有关的信息，而第二个调用返回有关"Accounts Payable"表，可能不是所期望的信息。  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, "Accounts Payable", SQL_NTS, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "\"Accounts Payable\"", SQL_NTS, NULL, 0);  
```  
  
 带引号的标识符用于从相同的名称，如 ROWID Oracle 中的伪列中区分 true 列名称。 如果"ROWID"中的目录函数自变量传递，该函数将使用 ROWID 伪列如果它存在。 如果伪列不存在，则该函数会使用"ROWID"列。 如果目录函数的自变量传入 ROWID，该函数会使用 ROWID 列。  
  
 有关带引号的标识符的详细信息，请参阅[带引号的标识符](../../../odbc/reference/develop-app/quoted-identifiers.md)。
