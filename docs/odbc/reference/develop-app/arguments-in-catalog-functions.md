---
title: 目录函数中的参数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arguments in catalog functions [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], about arguments
- functions [ODBC], catalog functions
ms.assetid: f5e0abec-8f24-42e0-b94f-16dd1f2004fd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 819c10d0b137d5e0999c1e10bf22810392509f76
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81288163"
---
# <a name="arguments-in-catalog-functions"></a>目录函数中的自变量
所有目录函数都接受应用程序可用于限制返回的数据范围的参数。 例如，在以下代码中对**SQLTables**的第一次和第二次调用返回包含有关所有表的信息的结果集，而第三次调用返回 Orders 表的相关信息：  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, NULL, 0, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "%", SQL_NTS, NULL, 0);  
SQLTables(hstmt3, NULL, 0, NULL, 0, "Orders", SQL_NTS, NULL, 0);  
```  
  
 目录函数字符串参数分为四种不同的类型：普通参数（OA）、模式值参数（PV）、标识符参数（ID）和值列表参数（VL）。 大多数字符串参数可以是两种不同类型之一，具体取决于 SQL_ATTR_METADATA_ID 语句特性的值。 下表列出了每个目录函数的参数，并描述了 SQL_ATTR_METADATA_ID 的 SQL_TRUE 或 SQL_FALSE 值的参数的类型。  
  
|函数|参数|键入 when SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_FALSE|键入 when SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_TRUE|  
|--------------|--------------|---------------------------------------------------------------|--------------------------------------------------------------|  
|**SQLColumnPrivileges**|*CatalogName* *SchemaName* *TableName* *ColumnName*|OA OA OA PV|ID ID ID|  
|**SQLColumns**|*CatalogName* *SchemaName* *TableName* *ColumnName*|OA PV PV|ID ID ID|  
|**SQLForeignKeys**|*PKCatalogName* *PKSchemaName* *PKTableName* *FKCatalogName* *FKSchemaName* *FKTableName*|OA OA OA OA OA|ID ID ID ID ID|  
|**SQLPrimaryKeys**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID ID ID|  
|**SQLProcedureColumns**|*CatalogName* *SchemaName* *ProcName* *ColumnName*|OA PV PV|ID ID ID|  
|**SQLProcedures**|*CatalogName* *SchemaName* *ProcName*|OA PV PV|ID ID ID|  
|**SQLSpecialColumns**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID ID ID|  
|**SQLStatistics**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID ID ID|  
|**SQLTablePrivileges**|*CatalogName* *SchemaName* *TableName*|OA PV PV|ID ID ID|  
|**SQLTables**|*CatalogName* *SchemaName* *TableName* *TableType*|PV PV PV VL|ID ID ID VL|  
  
 本部分包含以下主题。  
  
-   [普通自变量](../../../odbc/reference/develop-app/ordinary-arguments.md)  
  
-   [模式值自变量](../../../odbc/reference/develop-app/pattern-value-arguments.md)  
  
-   [标识符自变量](../../../odbc/reference/develop-app/identifier-arguments.md)  
  
-   [值列表自变量](../../../odbc/reference/develop-app/value-list-arguments.md)
