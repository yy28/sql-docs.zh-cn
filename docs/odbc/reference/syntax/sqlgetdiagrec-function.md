---
title: SQLGetDiagRec 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c404cbb1f29adbdcb49ef6bed8bb57a047f64f3b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67911320"
---
# <a name="sqlgetdiagrec-function"></a>SQLGetDiagRec 函数
**符合性**  
 版本引入了：ODBC 3.0 标准符合性：ISO 92  
  
 **摘要**  
 **SQLGetDiagRec**返回多个字段包含错误、 警告和状态信息的诊断记录的当前值。 与不同**SQLGetDiagField**，这会返回调用时，每个诊断字段**SQLGetDiagRec**返回多个常用的字段的诊断记录，包括 SQLSTATE、 本机错误代码，并诊断消息文本中。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
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
 [输入]描述诊断为其所需的句柄的类型的句柄类型标识符。 必须是下列选项之一：  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 只能由驱动程序管理器和驱动程序使用 SQL_HANDLE_DBC_INFO_TOKEN 句柄。 应用程序不应使用此句柄类型。 有关 SQL_HANDLE_DBC_INFO_TOKEN 详细信息，请参阅[ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 *Handle*  
 [输入]所指示的类型的诊断数据结构的句柄*HandleType*。 如果*HandleType*为 SQL_HANDLE_ENV，*处理*可以是共享或非共享的环境句柄。  
  
 *RecNumber*  
 [输入]指示从其应用程序查找信息的状态记录。 状态记录的编号从 1。  
  
 *SQLState*  
 [输出]指向用于返回五个字符的 SQLSTATE 代码 （和终止 NULL） 的诊断记录的缓冲区*RecNumber*。 前两个字符指示的类;下一步的三个指示子类。 SQL_DIAG_SQLSTATE 诊断字段中包含此信息。 有关详细信息，请参阅[SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)。  
  
 *NativeErrorPtr*  
 [输出]指向用于返回特定于数据源的本机错误代码的缓冲区。 SQL_DIAG_NATIVE 诊断字段中包含此信息。  
  
 *MessageText*  
 [输出]指向在其中返回的诊断消息的文本字符串的缓冲区的指针。 SQL_DIAG_MESSAGE_TEXT 诊断字段中包含此信息。 字符串的格式，请参阅[诊断消息](../../../odbc/reference/develop-app/diagnostic-messages.md)。  
  
 如果*MessageText*为 NULL， *TextLengthPtr*仍将返回的字符 （不包括字符数据的 null 终止字符） 总数可用于返回通过指向的缓冲区中*MessageText*。  
  
 *BufferLength*  
 [输入]长度 **MessageText*以字符为单位的缓冲区。 没有诊断消息文本的最大长度。  
  
 *TextLengthPtr*  
 [输出]指向用于返回的字符 （不包括所需的 null 终止字符的字符数） 总数的缓冲区可用于在中返回 *\*MessageText*。 如果可用于返回的字符数大于*BufferLength*中的诊断消息正文 *\*MessageText*截断为*BufferLength*减去 null 终止字符的长度。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 **SQLGetDiagRec**不会为其自身发送诊断记录。 它使用了以下返回值来报告其自身执行的结果：  
  
-   SQL_SUCCESS:该函数成功地返回诊断信息。  
  
-   SQL_SUCCESS_WITH_INFO:\* *MessageText*缓冲区是否太小而无法保存请求的诊断消息。 未不生成任何诊断记录。 若要确定发生了截断，应用程序必须进行比较*BufferLength*可用的字节，这写入的实际数目 **StringLengthPtr*。  
  
-   SQL_INVALID_HANDLE:指示句柄*HandleType*并*处理*不是有效的句柄。  
  
-   SQL_ERROR:出现下列情况之一：  
  
    -   *RecNumber*是负数或 0。  
  
    -   *BufferLength*小于零。  
  
    -   使用异步通知时，句柄上的异步操作是不完整。  
  
-   SQL_NO_DATA:*RecNumber*存在的句柄中指定的诊断记录数大于*处理。* 函数还将为任何正返回 SQL_NO_DATA *RecNumber*如果有没有可供诊断记录*处理*。  
  
## <a name="comments"></a>注释  
 应用程序通常会调用**SQLGetDiagRec** SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 时返回上次调用 ODBC 函数。 但是，因为任何 ODBC 函数可以发布零个或多个诊断记录每次调用它，应用程序可以调用**SQLGetDiagRec**任何 ODBC 函数调用之后。 应用程序可以调用**SQLGetDiagRec**多次诊断数据结构中返回的部分或所有记录。 ODBC 规定可以存放在任何一次的诊断记录数没有限制。  
  
 **SQLGetDiagRec**不能用于诊断数据结构的标头中返回字段。 ( *RecNumber*参数必须是大于 0。)应用程序应调用**SQLGetDiagField**实现此目的。  
  
 **SQLGetDiagRec**检索仅最近与中指定的句柄关联的诊断信息*处理*参数。 如果应用程序调用另一个 ODBC 函数，除非**SQLGetDiagRec**， **SQLGetDiagField**，或**SQLError**，从前面的调用上的任何诊断信息相同的句柄都将丢失。  
  
 应用程序可以扫描所有诊断记录的循环，递增*RecNumber*，只要**SQLGetDiagRec**返回 SQL_SUCCESS。 调用**SQLGetDiagRec**应是非破坏性的标头和记录字段。 应用程序可以调用**SQLGetDiagRec**再次在以后从只要为任何其他函数中，除记录检索字段**SQLGetDiagRec**， **SQLGetDiagField**，或**SQLError**，已在此期间调用。 应用程序还可以通过调用检索可用的诊断记录的总数的计数**SQLGetDiagField**若要检索的值 SQL_DIAG_NUMBER 字段中，并调用**SQLGetDiagRec**相同的次数。  
  
 诊断数据结构的字段的说明，请参阅[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。 有关详细信息，请参阅[使用 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)并[实现 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)。  
  
 调用而不是以异步方式执行的 API 会生成 HY010"函数序列错误"。 但是，在异步操作完成之前，无法检索错误记录。  
  
## <a name="handletype-argument"></a>HandleType 参数  
 每个句柄类型可以有与之关联的诊断信息。 *HandleType*自变量表示的句柄类型*处理*参数。  
  
 某些标头和记录字段不能句柄返回有关环境、 连接、 语句和描述符。 在"标头字段"和"记录字段"中的部分中指示该字段不适用于这些句柄[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。  
  
 调用**SQLGetDiagRec**将返回 SQL_INVALID_HANDLE，如果*HandleType*是 SQL_HANDLE_SENV，表示共享的环境句柄。 但是，如果*HandleType*为 SQL_HANDLE_ENV，*处理*可以是共享或非共享的环境句柄。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|获取诊断记录的字段或诊断标头的字段|[SQLGetDiagField 函数](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)   
 [示例 ODBC 程序](../../../odbc/reference/sample-odbc-program.md)
