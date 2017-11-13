---
title: "SQLGetDiagRec 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLGetDiagRec
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDiagRec
helpviewer_keywords:
- SQLGetDiagRec function [ODBC]
ms.assetid: ebdbac93-3d68-438f-8416-ef1f08e04269
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 591664f329f4c7feeb24fff52b809dba567d0b80
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetdiagrec-function"></a>SQLGetDiagRec 函数
**一致性**  
 版本引入了： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLGetDiagRec**返回多个字段包含错误、 警告和状态信息的诊断记录的当前值。 与不同**SQLGetDiagField**，这将返回每个调用，一个诊断字段**SQLGetDiagRec**返回多个常用包括 SQLSTATE，本机错误代码中，诊断记录的字段和诊断消息文本中。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLGetDiagRec(  
     SQLSMALLINT     HandleType,  
     SQLHANDLE       Handle,  
     SQLSMALLINT     RecNumber,  
     SQLCHAR *       SQLState,  
     SQLINTEGER *    NativeErrorPtr,  
     SQLCHAR *       MessageText,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   TextLengthPtr);  
```  
  
## <a name="arguments"></a>参数  
 *HandleType*  
 [输入]描述的类型的诊断为所需的句柄的句柄类型标识符。 必须是下列选项之一：  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 仅由驱动程序管理器和驱动程序使用 SQL_HANDLE_DBC_INFO_TOKEN 句柄。 应用程序不应使用此句柄类型。 有关 SQL_HANDLE_DBC_INFO_TOKEN 的详细信息，请参阅[开发中使用 ODBC 驱动程序的连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 *Handle*  
 [输入]诊断数据结构，指示的类型的句柄*HandleType*。 如果*HandleType*是 SQL_HANDLE_ENV，*处理*可以是共享或非共享的环境句柄。  
  
 *RecNumber*  
 [输入]指示应用程序从中查找信息的状态记录。 状态记录编号从 1。  
  
 *SQLState*  
 [输出]指向在其返回五个字符的 SQLSTATE 代码 （和终止 NULL） 为诊断记录的缓冲区的指针*RecNumber*。 前两个字符指示的类;接下来的三指示子类。 SQL_DIAG_SQLSTATE 诊断字段中包含此信息。 有关详细信息，请参阅[SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)。  
  
 *NativeErrorPtr*  
 [输出]指向在其中以返回特定于数据源的本机错误代码的缓冲区的指针。 SQL_DIAG_NATIVE 诊断字段中包含此信息。  
  
 *MessageText*  
 [输出]指向在其中返回的诊断消息文本字符串的缓冲区的指针。 SQL_DIAG_MESSAGE_TEXT 诊断字段中包含此信息。 字符串的格式，请参阅[诊断消息](../../../odbc/reference/develop-app/diagnostic-messages.md)。  
  
 如果*MessageText*为 NULL， *TextLengthPtr*仍将返回的字符 （不包括字符数据的 null 终止字符） 总数可用于返回指向的缓冲区中*MessageText*。  
  
 *BufferLength*  
 [输入]长度 **MessageText*以字符为单位的缓冲区。 没有诊断消息文本无最大长度。  
  
 *TextLengthPtr*  
 [输出]指向要返回的字符 （不包括所需的 null 终止字符的字符数） 总数在其中缓冲区的指针可用于返回在 *\*MessageText*。 如果可用于返回的字符数大于*BufferLength*中的诊断消息文本 *\*MessageText*截断为*BufferLength*减 null 终止字符的长度。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 **SQLGetDiagRec**不会发送自己的诊断记录。 它使用下列返回值来报告其自己执行的结果：  
  
-   SQL_SUCCESS： 该函数成功地返回诊断信息。  
  
-   SQL_SUCCESS_WITH_INFO: \* *MessageText*缓冲区是否太小，无法容纳请求的诊断消息。 未不生成任何诊断记录。 若要确定发生截断，应用程序必须进行比较*BufferLength*可用字节数，这写入的实际数目 **StringLengthPtr*。  
  
-   SQL_INVALID_HANDLE: 句柄由*HandleType*和*处理*不是有效的句柄。  
  
-   以下项之一发生 SQL_ERROR::  
  
    -   *RecNumber*为负或 0。  
  
    -   *BufferLength*小于零。  
  
    -   使用异步通知时，句柄的异步操作是不完整。  
  
-   SQL_NO_DATA: *RecNumber*存在的句柄中指定的诊断记录的数目大于*处理。* 此函数还为任何正返回 SQL_NO_DATA *RecNumber*是否存在的任何诊断记录*处理*。  
  
## <a name="comments"></a>注释  
 应用程序通常调用**SQLGetDiagRec** SQL_ERROR 或 SQL_SUCCESS_WITH_INFO ODBC 函数的以前调用已返回时。 但是，由于任何 ODBC 函数可以发布零个或多个诊断记录每次调用时，应用程序可以调用**SQLGetDiagRec**任何 ODBC 函数调用之后。 应用程序可以调用**SQLGetDiagRec**多次返回诊断数据结构中的部分或所有记录。 ODBC 有一定对可以在任何时候存储的诊断记录的数量没有限制。  
  
 **SQLGetDiagRec**不能用于从诊断数据结构的标头返回字段。 ( *RecNumber*参数必须大于 0。)应用程序应调用**SQLGetDiagField**为此目的。  
  
 **SQLGetDiagRec**只检索诊断信息中指定的句柄与最近关联*处理*自变量。 如果应用程序调用另一个 ODBC 函数，除非**SQLGetDiagRec**， **SQLGetDiagField**，或**SQLError**，从上以前的调用的任何诊断信息相同的句柄都将丢失。  
  
 应用程序可以扫描所有诊断记录的步骤循环、 递增*RecNumber*，只要**SQLGetDiagRec**返回 SQL_SUCCESS。 调用**SQLGetDiagRec**是非到标头和记录字段破坏性的。 应用程序可以调用**SQLGetDiagRec**再次在以后从只要为任何其他函数中，除记录中检索字段**SQLGetDiagRec**， **SQLGetDiagField**，或**SQLError**，已在此期间调用。 应用程序还可以通过调用检索诊断记录可用的总数的计数**SQLGetDiagField**来检索值 SQL_DIAG_NUMBER 字段，并调用**SQLGetDiagRec**相同的次数。  
  
 有关诊断数据结构的字段的说明，请参阅[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。 有关详细信息，请参阅[使用 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)和[实现 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)。  
  
 调用以异步方式执行以外的 API 将生成 HY010"函数序列错误"。 但是，在异步操作完成前，无法检索错误记录。  
  
## <a name="handletype-argument"></a>HandleType 自变量  
 每个句柄类型可以具有与之关联的诊断信息。 *HandleType*参数表示的句柄类型*处理*自变量。  
  
 某些标头和记录字段不能返回环境、 连接、 语句中，和描述符句柄。 为其字段并不适用于这些句柄所示的"标头字段"和"记录字段"部分中[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。  
  
 调用**SQLGetDiagRec**如果将返回 SQL_INVALID_HANDLE *HandleType*是 SQL_HANDLE_SENV，表示的共享的环境句柄。 但是，如果*HandleType*是 SQL_HANDLE_ENV，*处理*可以是共享或非共享的环境句柄。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|获取诊断记录的一个字段或诊断标头的字段|[SQLGetDiagField 函数](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 标头文件](../../../odbc/reference/install/odbc-header-files.md)   
 [示例 ODBC 程序](../../../odbc/reference/sample-odbc-program.md)

