---
title: 标识符参数 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300157"
---
# <a name="identifier-arguments"></a>标识符自变量
如果引用标识符参数中的字符串，则驱动程序将删除前导空格和尾随空格，并按字面处理引号内的字符串。 如果字符串未加引号，则驱动程序将删除尾随空格并将字符串折叠为大写。 如果将标识符参数设置为 null 指针，则将返回 SQL_ERROR 和 SQLSTATE HY009 （null 指针的使用无效），除非该参数是目录名称，并且不支持目录。  
  
 如果 SQL_ATTR_METADATA_ID 语句特性设置为 SQL_TRUE，则这些参数被视为标识符参数。 在这种情况下，下划线（_）和百分号（%）将被视为实际字符，而不是搜索模式字符。 如果将此属性设置为 SQL_FALSE，则这些参数将被视为普通参数或模式参数，具体取决于参数。  
  
 尽管包含特殊字符的标识符必须在 SQL 语句中用引号引起来，但在将它们作为目录函数参数传递时不得用引号括起来，因为传递给目录函数的引号字符将按原义解释。 例如，假设标识符引用字符（特定于驱动程序并通过**SQLGetInfo**返回）是一个双引号（"）。 对**SQLTables**的第一次调用返回包含有关应付帐款表的信息的结果集，而第二次调用返回 "应付帐款" 表的相关信息，这可能不是预期的情况。  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, "Accounts Payable", SQL_NTS, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "\"Accounts Payable\"", SQL_NTS, NULL, 0);  
```  
  
 带引号的标识符用于区分同一名称的伪列中的真实列名，如 Oracle 中的 ROWID。 如果在目录函数的参数中传递 "ROWID"，则函数将使用 ROWID 伪列（如果存在）。 如果伪列不存在，则该函数将与 "ROWID" 列一起使用。 如果在目录函数的参数中传递 ROWID，则函数将使用 ROWID 列。  
  
 有关带引号的标识符的详细信息，请参阅[带引号的标识符](../../../odbc/reference/develop-app/quoted-identifiers.md)。
