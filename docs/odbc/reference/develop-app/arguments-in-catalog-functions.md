---
title: 目录函数中的自变量 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 649c00f1db486dab4a996138be4e26b0e270fbae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106295"
---
# <a name="arguments-in-catalog-functions"></a>目录函数中的自变量
所有目录函数都接受自变量与该应用程序可以将限制返回的数据的作用域。 例如，第一个和第二个调用到**SQLTables**下面的代码中返回的结果集包含所有表有关的信息，而第三个调用返回订单表有关的信息：  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, NULL, 0, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "%", SQL_NTS, NULL, 0);  
SQLTables(hstmt3, NULL, 0, NULL, 0, "Orders", SQL_NTS, NULL, 0);  
```  
  
 目录函数字符串参数分为四种不同类型： 普通参数 (OA)、 模式值自变量 (PV)、 标识符 (ID)、 参数和值列表自变量 （批量许可）。 大多数字符串自变量可以是两种不同类型，具体取决于 SQL_ATTR_METADATA_ID 语句属性的值之一。 下表列出了每个目录函数的参数，并描述 SQL_ATTR_METADATA_ID SQL_TRUE 或 SQL_FALSE 值的参数的类型。  
  
|函数|参数|键入时 SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_FALSE|键入时 SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_TRUE|  
|--------------|--------------|---------------------------------------------------------------|--------------------------------------------------------------|  
|**SQLColumnPrivileges**|*CatalogName* *SchemaName* *TableName* *ColumnName*|OA OA OA PV|ID ID ID ID|  
|**SQLColumns**|*CatalogName* *SchemaName* *TableName* *ColumnName*|OA PV PV PV|ID ID ID ID|  
|**SQLForeignKeys**|*PKCatalogName* *PKSchemaName* *PKTableName* *FKCatalogName* *FKSchemaName* *FKTableName*|OA OA OA OA OA OA|ID ID ID ID ID ID|  
|**SQLPrimaryKeys**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID 为 ID ID|  
|**SQLProcedureColumns**|*CatalogName* *SchemaName* *ProcName* *ColumnName*|OA PV PV PV|ID ID ID ID|  
|**SQLProcedures**|*CatalogName* *SchemaName* *ProcName*|OA PV PV|ID 为 ID ID|  
|**SQLSpecialColumns**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID 为 ID ID|  
|**SQLStatistics**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID 为 ID ID|  
|**SQLTablePrivileges**|*CatalogName* *SchemaName* *TableName*|OA PV PV|ID 为 ID ID|  
|**SQLTables**|*CatalogName* *SchemaName* *TableName* *TableType*|PV PV PV 批量许可|ID ID ID 批量许可|  
  
 本部分包含以下主题。  
  
-   [普通自变量](../../../odbc/reference/develop-app/ordinary-arguments.md)  
  
-   [模式值自变量](../../../odbc/reference/develop-app/pattern-value-arguments.md)  
  
-   [标识符自变量](../../../odbc/reference/develop-app/identifier-arguments.md)  
  
-   [值列表自变量](../../../odbc/reference/develop-app/value-list-arguments.md)
