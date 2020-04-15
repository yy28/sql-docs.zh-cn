---
title: 核心接口一致性 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 886ded1cd79b35488c0d47df3dbd8055dc6a8016
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302129"
---
# <a name="core-interface-conformance"></a>核心接口一致性
所有 ODBC 驱动程序必须至少显示核心级接口一致性。 由于 Core 级别的功能是大多数通用可互操作应用程序所需的功能，因此驱动程序可以使用此类应用程序。 核心级别的功能也对应于 ISO CLI 规范中定义的功能以及开放组 CLI 规范中定义的非可选功能。 核心级接口一致的 ODBC 驱动程序允许应用程序执行以下所有操作：  
  
-   通过调用**SQLAllocHandle**和**SQLFreeHandle**来分配和释放所有类型的句柄。  
  
-   使用**SQLFreeStmt**函数的所有形式。  
  
-   通过调用**SQLBindCol**绑定结果集列。  
  
-   仅通过调用**SQLBind 参数**和**SQLNumParams**处理动态参数（包括参数数组）。 （输出方向的参数是[2 级接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的要素 203 。  
  
-   指定绑定偏移量。  
  
-   使用执行时的数据对话框，涉及对**SQLParamData**和**SQLPutData**的调用。  
  
-   通过调用**SQLCloseCursor、SQLGetCursorName**和**SQLSetCursorName**来管理游标和游标名称。 **SQLCloseCursor**  
  
-   通过调用 SQLColattribute、SQLDescribeCol、SQLNumResultCols 和**SQLDescribeCol** **SQLRowCount，** 访问结果集的描述（元数据）。 **SQLColAttribute** **SQLNumResultCols** （在列号 0 上使用这些函数来检索书签元数据是[2 级接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的功能 204 。  
  
-   通过调用目录函数**SQLColumns、SQLGetTypeInfo、SQL****SQLColumns****统计**和**SQLTables**查询数据字典。  
  
     不需要驱动程序来支持数据库表和视图的多部分名称。 （有关详细信息，请参阅[级别 1 接口一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)中的要素 101 和 2[级接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的功能 201 。但是，SQL-92 规范的某些功能（如列限定和索引名称）在语法上可与多部分命名相媲美。 本 ODBC 功能列表无意在 SQL-92 的这些方面引入新选项。  
  
-   通过调用**SQLConnect** **、SQLDataSources、SQL****断开连接**和**SQLDriverConnect**来管理数据源和连接。 通过调用**SQLDrivers**获取有关驱动程序的信息，无论他们支持哪个 ODBC 级别。  
  
-   通过调用**SQLExecDirect、SQLExecute**和**SQLExecute****SQLPrepare**来准备和执行 SQL 语句。  
  
-   仅按正向方向获取结果集的一行或多行，通过调用**SQLFetch**或调用**SQLFetchScroll，** 将*Fetch 方向*参数设置为SQL_FETCH_NEXT。  
  
-   通过调用**SQLGetData，** 获取部分未绑定列。  
  
-   通过调用**SQLGetConnectAttr、SQLGetEnvAttr**和**SQLGetStmtAttr**获取所有属性的当前值，并将所有属性设置为其默认值，并通过调用**SQLSetConnectAttr、SQLSetEnvAttr**和**SQLGetEnvAttr****SQLSetStmtAttr**将某些属性设置为非默认值。 **SQLSetEnvAttr**  
  
-   通过调用 SQLCopyDesc、SQLGetDescField、SQLGetDescRec、SQLSetDescField 和**SQLSetDescRec，** 操作描述符的某些**字段**。 **SQLCopyDesc** **SQLGetDescField** **SQLGetDescRec**  
  
-   通过调用**SQLGetDiagField**和**SQLGetDiagRec**获取诊断信息。  
  
-   通过调用**SQLGet 函数**和**SQLGetInfo 来**检测驱动程序功能。 此外，通过调用**SQLNativeSql，** 在 SQL 语句发送到数据源之前，检测对 SQL 语句所做的任何文本替换的结果。  
  
-   使用**SQLEndTran**的语法提交事务。 核心级驱动程序不需要支持真正的事务;因此，应用程序不能为SQL_ATTR_AUTOCOMMIT连接属性指定SQL_ROLLBACK或SQL_AUTOCOMMIT_OFF。 （有关详细信息，请参阅[2 级接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的功能 109 。  
  
-   调用**SQLCancel**以取消执行时的数据对话框，并在多线程环境中取消在另一个线程中执行的 ODBC 函数。 核心级接口一致性不要求支持异步执行函数，也不要求使用**SQLCancel**取消异步执行的 ODBC 函数。 平台和 ODBC 驱动程序都不需要多线程，以便驱动程序同时进行独立活动。 但是，在多线程环境中，ODBC 驱动程序必须是线程安全的。 应用程序请求的序列化是实现此规范的一种一致方法，即使它可能会造成严重的性能问题。  
  
-   通过调用**SQL 特别列**获取表的SQL_BEST_ROWID行标识列。 （支持SQL_ROWVER是[2 级接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的功能 208 。  
  
    > [!IMPORTANT]  
    >  ODBC 驱动程序必须实现核心接口一致性级别的功能。
