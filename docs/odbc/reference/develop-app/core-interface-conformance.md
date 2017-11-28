---
title: "核心接口一致性 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- core-level interface conformance levels [ODBC]
ms.assetid: aaaa864a-6477-45ff-a50a-96d8db66a252
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 07c5896fc179f8224914d0af8b4aa9defa94b9bf
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="core-interface-conformance"></a>核心接口一致性
所有 ODBC 驱动程序必须都展示至少核心级别接口一致性。 由于核心级别中的功能所需的最通用的可互操作应用程序，该驱动程序可以使用此类应用程序。 中的核心级别的功能还对应到 ISO CLI 规范中定义的功能和打开组 CLI 规范中定义的必需功能。 核心级接口 – 符合的 ODBC 驱动程序允许应用程序执行所有以下操作：  
  
-   分配和释放所有类型的句柄，通过调用**SQLAllocHandle**和**SQLFreeHandle**。  
  
-   使用所有形式的**SQLFreeStmt**函数。  
  
-   将结果集中的列，绑定通过调用**SQLBindCol**。  
  
-   处理动态参数，通过调用包括数组中的参数，只可输入的方向**SQLBindParameter**和**SQLNumParams**。 (输出方向中的参数是功能中的 203[级别 2 的接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)  
  
-   指定绑定偏移量。  
  
-   使用数据在执行对话框中，涉及到调用**SQLParamData**和**SQLPutData**。  
  
-   通过调用管理游标和游标名称**SQLCloseCursor**， **SQLGetCursorName**，和**SQLSetCursorName**。  
  
-   访问的说明 （元数据） 的结果集，通过调用**SQLColAttribute**， **SQLDescribeCol**， **SQLNumResultCols**，和**SQLRowCount**. (列号 0 以检索书签元数据在这些函数的使用是功能中的 204[级别 2 的接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)  
  
-   查询数据字典中，通过调用目录函数**SQLColumns**， **SQLGetTypeInfo**， **SQLStatistics**，和**SQLTables**。  
  
     该驱动程序不需要支持多部分名称的数据库表和视图。 (有关详细信息，请参阅中的新功能 101[级别 1 的接口一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)和功能中的 201[级别 2 的接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)但是，某些功能的 SQL 92 规范，例如限定列和名称的索引，可以语法上与多部分命名。 ODBC 功能存在列表不是引入到这些方面的 SQL 92 的新选项。  
  
-   管理数据源和连接，通过调用**SQLConnect**， **SQLDataSources**， **SQLDisconnect**，和**SQLDriverConnect**。 获取驱动程序，无论哪个 ODBC 级别它们支持，通过调用的信息**SQLDrivers**。  
  
-   准备和执行 SQL 语句，通过调用**SQLExecDirect**， **SQLExecute**，和**SQLPrepare**。  
  
-   通过调用提取的结果集的一行或多个行，在向前方向仅， **SQLFetch**或通过调用**SQLFetchScroll**与*FetchOrientation*自变量设置为 SQL_FETCH_NEXT。  
  
-   通过调用获取在部件中，未绑定的列**SQLGetData**。  
  
-   通过调用获取的所有属性的当前值**SQLGetConnectAttr**， **SQLGetEnvAttr**，和**SQLGetStmtAttr**，并将所有属性都设置为其默认值和将某些属性设置为非默认值，通过调用**SQLSetConnectAttr**， **SQLSetEnvAttr**，和**SQLSetStmtAttr**。  
  
-   通过调用操作的描述符，某些字段**SQLCopyDesc**， **SQLGetDescField**， **SQLGetDescRec**， **SQLSetDescField**，和**SQLSetDescRec**。  
  
-   获取诊断信息，通过调用**SQLGetDiagField**和**SQLGetDiagRec**。  
  
-   通过调用检测驱动程序的功能， **SQLGetFunctions**和**SQLGetInfo**。 此外，检测任何文本替换为一个 SQL 语句发送到数据源中，通过调用之前的结果**SQLNativeSql**。  
  
-   使用的语法**SQLEndTran**提交的事务。 核心级驱动程序不需要支持 true 事务;因此，应用程序不能指定 SQL_ROLLBACK 也不 SQL_AUTOCOMMIT_OFF SQL_ATTR_AUTOCOMMIT 连接属性。 (有关详细信息，请参阅中的新功能 109[级别 2 的接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)  
  
-   调用**SQLCancel**取消执行中的数据对话框并在多线程环境中，若要取消另一个线程中 ODBC 函数执行。 核心级接口一致性不强制要求以异步执行的函数，也不是使用支持**SQLCancel**取消 ODBC 函数以异步方式执行。 平台和 ODBC 驱动程序都不需要驱动程序在同一时间进行独立的活动的多线程。 但是，在多线程环境中，ODBC 驱动程序必须是线程安全。 来自应用程序的请求的序列化是实现此规范，符合的方法，即使它可能造成严重性能问题。  
  
-   通过调用获取 SQL_BEST_ROWID 行标识列的表， **SQLSpecialColumns**。 (支持 SQL_ROWVER 是功能中的 208[级别 2 的接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)  
  
    > [!IMPORTANT]  
    >  ODBC 驱动程序必须实现核心接口一致性级别中的函数。
