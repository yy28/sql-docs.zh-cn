---
title: "处理错误和消息 |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-error-messages
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, about error handling
- errors [ODBC]
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], about messages
- ODBC error handling
- SQL_INVALID_HANDLE return code
- errors [ODBC], about error handling
- messages [ODBC]
ms.assetid: 74ea9630-e482-4a46-bb45-f5234f079b48
caps.latest.revision: "34"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8ace5aa790162d91203019d8c7d5cae5375cc281
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="handling-errors-and-messages"></a>处理错误和消息
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  当应用程序调用 ODBC 函数时，驱动程序执行该函数，并以两种方式返回诊断信息：返回代码指示 ODBC 函数总体成功或失败，诊断记录提供有关函数的详细信息。 诊断记录包含标题记录和状态记录。 即使该函数成功，也仍将至少返回一条诊断记录，即标题记录。  
  
 诊断信息用于在开发时捕获编程错误，例如硬编码的 SQL 语句中的无效句柄和语法错误。 此外，该信息还用于在运行时捕获运行时错误和警告，例如用户输入的 SQL 语句中的数据截断、规则冲突和语法错误。 程序逻辑通常基于返回代码。  
  
 例如，在应用程序调用**SQLFetch**若要检索结果集中的行，返回代码指示是否已到达结果集的末尾 (SQL_NO_DATA)，如果返回任何信息性消息 (SQL_SUCCESS_WITH_INFO)，或如果出错 (SQL_ERROR)。  
  
 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序返回 SQL_SUCCESS 以外的任何，应用程序可以调用**SQLGetDiagRec**检索任何信息性消息或错误消息。 使用**SQLGetDiagRec**滚动向上和向下设置如果有多条消息的消息。  
  
 返回代码 SQL_INVALID_HANDLE 始终指示编程错误，并且决不能在运行时遇到。 所有其他返回代码提供运行时信息，但 SQL_ERROR 可以指示编程错误。  
  
 原始[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机 API，Db-library c，允许应用程序安装回调错误处理和消息处理函数的返回的错误或消息。 某些 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句（如 PRINT、RAISERROR、DBCC 和 SET）将其结果返回到 DB-Library 消息处理程序函数，而不是结果集。 但是，ODBC API 不具备这种回调功能。 当[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序检测到传回的消息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，它将 ODBC 返回代码设置为 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR 和返回作为一个或多个诊断记录的消息。 因此，ODBC 应用程序必须仔细对其进行测试这些返回代码和调用**SQLGetDiagRec**检索消息数据。  
  
 有关跟踪错误的信息，请参阅[数据访问跟踪](http://go.microsoft.com/fwlink/?LinkId=125805)。 有关在中添加的错误跟踪的增强功能[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，请参阅[访问扩展事件日志中的诊断信息](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [处理生成消息的语句](../../relational-databases/native-client-odbc-error-messages/processing-statements-that-generate-messages.md)  
  
-   [诊断记录和字段](../../relational-databases/native-client-odbc-error-messages/diagnostic-records-and-fields.md)  
  
-   [本机错误号](../../relational-databases/native-client-odbc-error-messages/native-error-numbers.md)  
  
-   [SQLSTATE &#40; ODBC 错误代码 &#41;](../../relational-databases/native-client-odbc-error-messages/sqlstate-odbc-error-codes.md)  
  
-   [错误消息](../../relational-databases/native-client-odbc-error-messages/error-messages.md)  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client &#40; ODBC &#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
