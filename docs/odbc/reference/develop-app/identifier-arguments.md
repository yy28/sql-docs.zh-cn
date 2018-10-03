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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 156dfaf5c6a6a4ec06a0c96b5f726383cba32ba6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47609925"
---
# <a name="identifier-arguments"></a>标识符自变量
如果带引号的标识符参数中的字符串，该驱动程序中删除前导和尾随空格，并将按原义引号引起来的字符串。 如果不带引号的字符串，则该驱动程序删除尾随空格和折叠为大写的字符串。 设置标识符的参数为 null 指针将返回 SQL_ERROR 和 SQLSTATE HY009 （使用无效的 null 指针），除非参数为目录名称，并且不支持目录。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE，这些自变量被视为标识符参数。 在这种情况下，下划线 (_) 和百分号 （%） 将视为实际的字符不是作为一个搜索模式字符。 这些自变量被视为普通参数或模式参数，具体取决于该参数，如果此属性设置为 SQL_FALSE。  
  
 尽管包含特殊字符的标识符必须用引号引起来在 SQL 语句中，但它们必须未用引号引起来作为目录函数参数传递时由于按照字义解释引号字符传递到目录函数。 例如，假定标识符引号字符 (这是特定于驱动程序和通过返回**SQLGetInfo**) 是双引号 （"）。 首次调用**SQLTables**返回的结果集包含 Accounts Payable 表有关的信息，而第二次调用返回 Accounts Payable 表，这是可能不是所期望的信息。  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, "Accounts Payable", SQL_NTS, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "\"Accounts Payable\"", SQL_NTS, NULL, 0);  
```  
  
 带引号的标识符用于相同的名称，例如在 Oracle 中 ROWID 的伪列区分开来，则返回 true 的列名称。 如果目录函数的参数中传递"ROWID"，则该函数将使用 ROWID 伪列如果它存在。 如果伪列不存在，该函数将使用"行 ID"列。 如果 ROWID 目录函数的参数中传递，该函数将使用行 ID 列。  
  
 有关带引号的标识符的详细信息，请参阅[带引号的标识符](../../../odbc/reference/develop-app/quoted-identifiers.md)。
