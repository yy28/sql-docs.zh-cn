---
title: 核心接口一致性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- core-level interface conformance levels [ODBC]
ms.assetid: aaaa864a-6477-45ff-a50a-96d8db66a252
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e41d71cd3651e1db5d1a533159012b645b8c7764
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63043753"
---
# <a name="core-interface-conformance"></a>核心接口一致性
所有 ODBC 驱动程序必须都有至少核心级别接口一致性。 由于核心级别中的功能所需的最通用的可互操作应用程序，该驱动程序可以使用此类应用程序。 核心级别中的功能也对应到 ISO CLI 规范中定义的功能和打开组 CLI 规范中定义的必需功能。 核心级别接口符合的 ODBC 驱动程序允许应用程序执行所有以下操作：  
  
-   分配和释放所有类型的句柄，通过调用**SQLAllocHandle**并**SQLFreeHandle**。  
  
-   使用的所有窗体**SQLFreeStmt**函数。  
  
-   将结果集列绑定通过调用**SQLBindCol**。  
  
-   处理动态参数，通过调用包括参数，仅，在输入方向的数组**SQLBindParameter**并**SQLNumParams**。 (输出方向中的参数是功能中的 203[级别 2 接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)  
  
-   指定绑定偏移量。  
  
-   使用执行时数据对话框中，涉及对调用**SQLParamData**并**SQLPutData**。  
  
-   通过调用管理游标和游标名称**SQLCloseCursor**， **SQLGetCursorName**，并**SQLSetCursorName**。  
  
-   获取结果集的访问权限 （元数据） 的说明，通过调用**SQLColAttribute**， **SQLDescribeCol**， **SQLNumResultCols**，和**SQLRowCount**. (使用这些函数在列号 0 以检索书签元数据是功能中的 204[级别 2 接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)  
  
-   通过调用目录函数来查询数据字典**SQLColumns**， **SQLGetTypeInfo**， **SQLStatistics**，以及**SQLTables**。  
  
     该驱动程序不需要支持的数据库表和视图的多部分名称。 (有关详细信息，请参阅中的新功能 101[级别 1 接口一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)和功能中的 201[级别 2 接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)但是，SQL-92 规范，如限定列和索引名称的某些功能将与多部分命名语法相当。 不应存在 ODBC 功能列表引入到这些方面的 SQL-92 的新选项。  
  
-   管理数据源和连接，通过调用**SQLConnect**， **SQLDataSources**， **SQLDisconnect**，以及**SQLDriverConnect**。 获取驱动程序，无论哪个 ODBC 级别它们支持，通过调用的信息**SQLDrivers**。  
  
-   准备和执行 SQL 语句，通过调用**SQLExecDirect**， **SQLExecute**，并**SQLPrepare**。  
  
-   通过调用提取结果集的一行或多个行，只是向前**SQLFetch**或通过调用**SQLFetchScroll**与*FetchOrientation*参数将设置为 SQL_FETCH_NEXT。  
  
-   获取未绑定的列在部件中，通过调用**SQLGetData**。  
  
-   通过调用获取的所有属性的当前值**SQLGetConnectAttr**， **SQLGetEnvAttr**，并**SQLGetStmtAttr**，并将所有属性都设置为其默认值和将某些属性设置为非默认值，通过调用**SQLSetConnectAttr**， **SQLSetEnvAttr**，并**SQLSetStmtAttr**。  
  
-   通过调用操作描述符，某些字段**SQLCopyDesc**， **SQLGetDescField**， **SQLGetDescRec**， **SQLSetDescField**，并**SQLSetDescRec**。  
  
-   获取诊断信息，通过调用**SQLGetDiagField**并**SQLGetDiagRec**。  
  
-   检测驱动程序功能，通过调用**SQLGetFunctions**并**SQLGetInfo**。 此外，检测的结果发送到数据源中，通过调用之前对 SQL 语句所做的任何文本替换**SQLNativeSql**。  
  
-   使用的语法**SQLEndTran**提交的事务。 核心级驱动程序不需要支持事务，则返回 true;因此，应用程序不能指定 SQL_ROLLBACK 也不 SQL_AUTOCOMMIT_OFF SQL_ATTR_AUTOCOMMIT 连接属性。 (有关详细信息，请参阅中的新功能 109[级别 2 接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)  
  
-   调用**SQLCancel**取消执行时数据对话框并在多线程环境中，若要取消 ODBC 函数中执行另一个线程。 核心级别接口一致性不强制要求对异步执行函数，也不使用的支持**SQLCancel**取消 ODBC 函数以异步方式执行。 平台和 ODBC 驱动程序都不需要是多线程驱动程序在同一时间进行独立的活动。 但是，在多线程环境中，ODBC 驱动程序必须是线程安全。 来自应用程序的请求的序列化是符合的方式来实现此规范，即使它可能造成严重性能问题。  
  
-   通过调用获取表的 SQL_BEST_ROWID 行标识列**SQLSpecialColumns**。 (支持 SQL_ROWVER 是功能中的 208[级别 2 接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)  
  
    > [!IMPORTANT]  
    >  ODBC 驱动程序必须实现的核心接口一致性级别中的函数。
