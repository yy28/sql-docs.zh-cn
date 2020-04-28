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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 886ded1cd79b35488c0d47df3dbd8055dc6a8016
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302129"
---
# <a name="core-interface-conformance"></a>核心接口一致性
所有 ODBC 驱动程序必须至少表现出核心级别的接口一致性。 由于核心级别的功能是大多数一般可互操作应用程序所需的功能，因此该驱动程序可用于此类应用程序。 核心级别的功能还对应于 ISO CLI 规范中定义的功能和开放组 CLI 规范中定义的 nonoptional 功能。 与核心级别接口相容的 ODBC 驱动程序允许应用程序执行以下所有操作：  
  
-   通过调用**SQLAllocHandle**和**SQLFreeHandle**，分配和释放所有类型的句柄。  
  
-   使用**SQLFreeStmt**函数的所有窗体。  
  
-   绑定结果集列，方法是调用**SQLBindCol**。  
  
-   通过调用**SQLBindParameter**和**SQLNumParams**，仅在输入方向上处理动态参数（包括参数数组）。 （输出方向的参数是[第2级接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的功能203。）  
  
-   指定绑定偏移量。  
  
-   使用执行时数据对话框，涉及对**SQLParamData**和**SQLPutData**的调用。  
  
-   通过调用**SQLCloseCursor**、 **SQLGetCursorName**和**SQLSetCursorName**来管理游标和游标名称。  
  
-   通过调用**SQLColAttribute**、 **SQLDescribeCol**、 **SQLNumResultCols**和**SQLRowCount**，获取对结果集的说明（元数据）的访问权限。 （将这些函数用于列号0时，检索书签元数据是[第2级接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的功能204。）  
  
-   查询数据字典，方法是调用目录函数**SQLColumns**、 **SQLGetTypeInfo**、 **SQLStatistics**和**SQLTables**。  
  
     驱动程序无需支持数据库表和视图的多部分名称。 （有关详细信息，请参阅第[1 级接口一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)中的功能101和[级别2接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的功能201。）但是，SQL-92 规范的某些功能（如列限定和索引的名称）在语法上与多部分命名类似。 ODBC 功能的现有列表并不用于向 SQL-92 的这些方面引入新的选项。  
  
-   通过调用**SQLConnect**、 **SQLDataSources**、 **SQLDisconnect**和**SQLDriverConnect**来管理数据源和连接。 通过调用**SQLDrivers**获取有关驱动程序的信息，而不管它们支持哪个 ODBC 级别。  
  
-   通过调用**SQLExecDirect**、 **SQLExecute**和**SQLPREPARE**，准备和执行 SQL 语句。  
  
-   只是通过调用**SQLFetch**或调用**SQLFetchScroll** ，并将*FetchOrientation*参数设置为 SQL_FETCH_NEXT 来获取结果集的一行或多行（仅向前方向）。  
  
-   通过调用**SQLGetData**，在部分中获取未绑定列。  
  
-   通过调用**SQLGetConnectAttr**、 **SQLGetEnvAttr**和**SQLGetStmtAttr**获取所有属性的当前值，并将所有属性设置为其默认值，并通过调用**SQLSetConnectAttr**、 **SQLSetEnvAttr**和**SQLSetStmtAttr**将某些属性设置为非默认值。  
  
-   通过调用**SQLCopyDesc**、 **SQLGetDescField**、 **SQLGetDescRec**、 **SQLSetDescField**和**SQLSetDescRec**来处理描述符的某些字段。  
  
-   通过调用**SQLGetDiagField**和**SQLGetDiagRec**获取诊断信息。  
  
-   通过调用**SQLGetFunctions**和**SQLGetInfo**来检测驱动程序功能。 此外，还可以通过调用**SQLNativeSql**来检测对 SQL 语句进行的任何文本替换的结果，并将其发送到数据源。  
  
-   使用**SQLEndTran**的语法来提交事务。 核心级驱动程序无需支持真正的事务;因此，应用程序不能为 SQL_ATTR_AUTOCOMMIT 连接属性指定 SQL_ROLLBACK 和 SQL_AUTOCOMMIT_OFF。 （有关详细信息，请参阅[第2级接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的功能109。）  
  
-   调用**SQLCancel**可取消执行时数据对话框，在多线程环境中，取消在另一个线程中执行的 ODBC 函数。 核心级接口一致性不会强制支持函数的异步执行，也不会使用**SQLCancel**来取消异步执行的 ODBC 函数。 平台和 ODBC 驱动程序都不需要多线程，因此驱动程序可以同时执行独立的活动。 但在多线程环境中，ODBC 驱动程序必须是线程安全的。 从应用程序进行的请求序列化是实现此规范的一致方法，即使它可能会导致严重的性能问题。  
  
-   通过调用**SQLSpecialColumns**获取表的 SQL_BEST_ROWID 行标识列。 （支持 SQL_ROWVER 是[第2级接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的功能208。）  
  
    > [!IMPORTANT]  
    >  ODBC 驱动程序必须在核心接口一致性级别实现函数。
