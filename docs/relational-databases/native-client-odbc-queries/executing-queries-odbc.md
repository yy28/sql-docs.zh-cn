---
title: "执行查询 (ODBC) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-queries
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ODBC applications, executing queries
- SQL Server Native Client ODBC driver, statements
- ODBC applications, statements
- SQL Server Native Client ODBC driver, queries
- queries [ODBC]
ms.assetid: d935bcba-8ce6-4159-8395-6c86431602ad
caps.latest.revision: "32"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c94ad284fbdf13dff9169a07a4ae2b45562f41e8
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="executing-queries-odbc"></a>执行查询 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  在 ODBC 应用程序初始化连接句柄并与数据源连接后，它为连接句柄分配一个或多个语句句柄。 然后执行应用程序可以[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]语句句柄上的语句。 执行 SQL 语句时的一般事件顺序为：  
  
1.  设置所有所需的语句属性。  
  
2.  构造语句。  
  
3.  执行语句。  
  
4.  检索任何结果集。  
  
 应用程序检索 SQL 语句所返回的所有结果集中的所有行后，它可以在同一语句句柄上执行其他查询。 如果应用程序确定，它不需要检索特定结果集中的所有行，它可以取消的结果集通过调用 rest [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)或[SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md)。  
  
 如果在 ODBC 应用程序中必须使用不同数据多次执行同一 SQL 语句，可以在 SQL 语句的构造中使用用问号 (?) 表示的参数标记：  
  
```  
INSERT INTO MyTable VALUES (?, ?, ?)  
```  
  
 每个参数标记可以然后绑定到程序变量通过调用[SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)。  
  
 执行所有 SQL 语句并处理它们的结果集之后，应用程序释放语句句柄。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序还支持每个连接句柄的多个语句句柄。 在连接级别管理事务，以便将针对单个连接句柄上的所有语句句柄执行的所有工作视为同一事务的一部分来管理。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [分配语句句柄](../../relational-databases/native-client-odbc-queries/allocating-a-statement-handle.md)  
  
-   [构造 SQL 语句 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-queries/constructing-an-sql-statement-odbc.md)  
  
-   [为游标构造 SQL 语句](../../relational-databases/native-client-odbc-queries/constructing-sql-statements-for-cursors.md)  
  
-   [使用语句参数](../../relational-databases/native-client-odbc-queries/using-statement-parameters.md)  
  
-   [正在执行语句 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
-   [释放语句句柄](../../relational-databases/native-client-odbc-queries/freeing-a-statement-handle.md)  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client &#40; ODBC &#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
