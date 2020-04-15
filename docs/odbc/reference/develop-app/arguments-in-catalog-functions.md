---
title: 目录函数中的参数 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288163"
---
# <a name="arguments-in-catalog-functions"></a>目录函数中的自变量
所有目录函数都接受应用程序可以限制返回的数据范围的参数。 例如，以下代码中对**SQLTable**的第一次和第二次调用返回一个包含所有表信息的结果集，而第三个调用返回有关 Orders 表的信息：  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, NULL, 0, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "%", SQL_NTS, NULL, 0);  
SQLTables(hstmt3, NULL, 0, NULL, 0, "Orders", SQL_NTS, NULL, 0);  
```  
  
 目录函数字符串参数分为四种不同类型：普通参数 （OA）、模式值参数 （PV）、标识符参数 （ID） 和值列表参数 （VL）。 大多数字符串参数可以是两种不同类型的类型之一，具体取决于SQL_ATTR_METADATA_ID语句属性的值。 下表列出了每个目录函数的参数，并描述了SQL_TRUE或SQL_ATTR_METADATA_ID值的SQL_FALSE参数的类型。  
  
|函数|参数|SQL_时键入<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_FALSE|SQL_时键入<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_TRUE|  
|--------------|--------------|---------------------------------------------------------------|--------------------------------------------------------------|  
|**SQLColumnPrivileges**|*目录名称**架构名称**表名称**列名称*|OA OA OA 光伏|ID ID ID ID|  
|**SQLColumns**|*目录名称**架构名称**表名称**列名称*|OA 光伏光伏光伏|ID ID ID ID|  
|**SQLForeignKeys**|*PK 目录名称**PK 名称* *PKtable 名称* *FKcatalog 名称* *FKschema 名称* *FKtable 名称*|OA OA OA OA OA OA|ID ID ID ID ID ID|  
|**SQLPrimaryKeys**|*目录名称**架构名称**表名称*|OA OA OA|ID ID ID|  
|**SQLProcedureColumns**|*目录名称**架构名称* *Procname* *列名称*|OA 光伏光伏光伏|ID ID ID ID|  
|**SQLProcedures**|*目录名称**架构名称* *ProcName*|OA 光伏光伏|ID ID ID|  
|**SQLSpecialColumns**|*目录名称**架构名称**表名称*|OA OA OA|ID ID ID|  
|**SQLStatistics**|*目录名称**架构名称**表名称*|OA OA OA|ID ID ID|  
|**SQLTablePrivileges**|*目录名称**架构名称**表名称*|OA 光伏光伏|ID ID ID|  
|**SQLTables**|*目录名称**架构名称**表名称**表类型*|光伏光伏光伏 VL|ID ID ID VL|  
  
 本部分包含以下主题。  
  
-   [普通自变量](../../../odbc/reference/develop-app/ordinary-arguments.md)  
  
-   [模式值自变量](../../../odbc/reference/develop-app/pattern-value-arguments.md)  
  
-   [标识符自变量](../../../odbc/reference/develop-app/identifier-arguments.md)  
  
-   [值列表自变量](../../../odbc/reference/develop-app/value-list-arguments.md)
