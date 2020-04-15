---
title: 标识符参数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- identifier arguments [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], identifier
ms.assetid: b9de003f-cb49-4dec-b528-14a5b8ff12bd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6831eab30daebe37baecebe3ed7053537d7de8f8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300157"
---
# <a name="identifier-arguments"></a>标识符自变量
如果引用标识符参数中的字符串，驱动程序将删除前导和尾随空格，并从字面上处理引号中的字符串。 如果未引用字符串，驱动程序将删除尾随空格并将字符串折叠到大写。 将标识符参数设置为空指针将返回SQL_ERROR和 SQLSTATE HY009（无效使用空指针），除非参数是目录名称且不支持目录。  
  
 如果将SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，则这些参数将被视为标识符参数。 在这种情况下，下划线 （*） 和百分比符号 （%）将被视为实际字符，而不是搜索模式字符。 如果此属性设置为SQL_FALSE，则这些参数将被视为普通参数或模式参数，具体取决于参数。  
  
 尽管包含特殊字符的标识符必须在 SQL 语句中引用，但在作为目录函数参数传递时不得引用这些标识符，因为传递给目录函数的报价字符是字面上解释的。 例如，假设标识符引号字符（特定于驱动程序并通过**SQLGetInfo**返回）是双引号 （）。 对**SQLTables**的第一个调用返回一个包含有关应付帐款表的信息的结果集，而第二个调用返回有关"应付帐款"表的信息，这可能不是预期。  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, "Accounts Payable", SQL_NTS, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "\"Accounts Payable\"", SQL_NTS, NULL, 0);  
```  
  
 引用的标识符用于区分真实列名和同名的伪列，如 Oracle 中的 ROWID。 如果在目录函数的参数中传递了"ROWID"，则该函数将使用 ROWID 伪列（如果存在）。 如果伪列不存在，则函数将使用"ROWID"列。 如果在目录函数的参数中传递 ROWID，则该函数将使用 ROWID 列。  
  
 有关引用标识符的详细信息，请参阅[引用标识符](../../../odbc/reference/develop-app/quoted-identifiers.md)。
