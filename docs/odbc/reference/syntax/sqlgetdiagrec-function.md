---
title: SQLGetDiarec 函数 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 39069526e254903509ddfef00b7bd4844f3d9e10
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285377"
---
# <a name="sqlgetdiagrec-function"></a>SQLGetDiagRec 函数
**一致性**  
 推出版本： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLGetDiagRec**返回包含错误、警告和状态信息的诊断记录多个字段的当前值。 与**SQLGetDiagField**（每次调用返回一个诊断字段 ） 不同 **，SQLGetDiagRec**返回诊断记录的几个常用字段，包括 SQLSTATE、本机错误代码和诊断消息文本。  
  
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
 [输入]描述需要诊断的句柄类型的句柄类型标识符。 必须是下列选项之一：  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN句柄仅由驱动程序管理器和驱动程序使用。 应用程序不应使用此句柄类型。 有关SQL_HANDLE_DBC_INFO_TOKEN的详细信息，请参阅在[ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 *Handle*  
 [输入]诊断数据结构的句柄，由*HandleType*指示的类型。 如果*HandleType*是SQL_HANDLE_ENV，*则句柄*可以是共享环境句柄，也可以是非共享环境句柄。  
  
 *RecNumber*  
 [输入]指示应用程序从中查找信息的状态记录。 状态记录从 1 编号。  
  
 *SQLState*  
 [输出]指向用于返回诊断记录*RecNumber*的五个字符 SQLSTATE 代码（和终止 NULL）的缓冲区的指针。 前两个字符指示类;第二个字符指示类。接下来的三个表示子类。 此信息包含在SQL_DIAG_SQLSTATE诊断字段中。 有关详细信息，请参阅[SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)。  
  
 *本机错误 Ptr*  
 [输出]指向缓冲区的指针，用于返回特定于数据源的本机错误代码。 此信息包含在SQL_DIAG_NATIVE诊断字段中。  
  
 *MessageText*  
 [输出]指向要返回诊断消息文本字符串的缓冲区的指针。 此信息包含在SQL_DIAG_MESSAGE_TEXT诊断字段中。 有关字符串的格式，请参阅[诊断消息](../../../odbc/reference/develop-app/diagnostic-messages.md)。  
  
 如果*MessageText*为*NULL，TextLengthPtr*仍将返回可在*MessageText*指向的缓冲区中返回的字符总数（不包括字符数据的空终止字符）。  
  
 *缓冲区长度*  
 [输入]以字符表示*消息文本*缓冲区的长度。 诊断消息文本没有最大长度。  
  
 *文本长度 Ptr*  
 [输出]指向一个缓冲区的指针，其中返回可在*\*MessageText*中返回的字符总数（不包括 null 终止字符所需的字符数）。 如果可用返回的字符数大于*BufferLength，* 则*\*MessageText*中的诊断消息文本将截断为*BufferLength*减去空终止字符的长度。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 **SQLGetDiagRec**不会自行发布诊断记录。 它使用以下返回值来报告其自身执行的结果：  
  
-   SQL_SUCCESS：该功能已成功返回诊断信息。  
  
-   SQL_SUCCESS_WITH_INFO：\**消息文本*缓冲区太小，无法保存请求的诊断消息。 未生成诊断记录。 要确定发生截断，应用程序必须将*BufferLength*与实际可用字节数进行比较，该字节数写入 **StringLengthPtr*。  
  
-   *SQL_INVALID_HANDLE：HandleType*和*Handle*指示的句柄不是有效的句柄。  
  
-   SQL_ERROR： 发生了以下情况之一：  
  
    -   *RecNumber*为负数或 0。  
  
    -   *缓冲区长度*小于零。  
  
    -   使用异步通知时，句柄上的异步操作未完成。  
  
-   SQL_NO_DATA： *RecNumber*大于*在 Handle*中指定的句柄存在的诊断记录数。 如果*Handle*没有诊断记录，则函数还会返回任何正*RecNumber* SQL_NO_DATA。  
  
## <a name="comments"></a>注释  
 当以前对 ODBC 函数的调用已返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，应用程序通常调用**SQLGetDiagRec。** 但是，由于任何 ODBC 函数每次调用时都可以发布零个或多个诊断记录，因此应用程序可以在任何 ODBC 函数调用后调用**SQLGetDiarec。** 应用程序可以多次调用**SQLGetDiagRec**以返回诊断数据结构中的部分或全部记录。 ODBC 对可同时存储的诊断记录的数量没有限制。  
  
 **SQLGetDiagRec**不能用于从诊断数据结构的标头返回字段。 *（RecNumber*参数必须大于 0。为此，应用程序应调用**SQLGetDiagField。**  
  
 **SQLGetDiagRec**仅检索最近与*Handle*参数中指定的句柄关联的诊断信息。 如果应用程序调用另一个 ODBC 函数 **（SQLGetDiarec、SQLGetDiagField**或**SQLError），** 则同一句柄上以前调用的任何诊断信息都丢失。 **SQLGetDiagField**  
  
 应用程序可以通过循环扫描所有诊断记录，增加*RecNumber，* 只要**SQLGetDiagRec**返回SQL_SUCCESS。 对**SQLGetDiagRec 的**调用对标头和记录字段没有破坏性。 应用程序可以在以后再次调用**SQLGetDiagRec**从记录中检索字段，只要在此期间没有调用除**SQLGetDiagRec、SQLGetDiagField****SQLGetDiagField**或**SQLError**之外的其他函数。 应用程序还可以检索可用诊断记录总数计数，通过调用**SQLGetDiagField**检索SQL_DIAG_NUMBER字段的值，然后多次调用**SQLGetDiagRec。**  
  
 有关诊断数据结构字段的说明，请参阅[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。 有关详细信息，请参阅使用[SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) [并实现 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)。  
  
 调用异步执行的 API 以外的 API 将生成 HY010"函数序列错误"。 但是，在异步操作完成之前无法检索错误记录。  
  
## <a name="handletype-argument"></a>句柄类型参数  
 每个句柄类型都可以具有与其关联的诊断信息。 *HandleType*参数表示*句柄*参数的句柄类型。  
  
 无法为环境、连接、语句和描述符句柄返回某些标头和记录字段。 在[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)中的"标题字段"和"记录字段"部分中指示字段不适用的句柄。  
  
 如果*handleType*是SQL_HANDLE_SENV的，则对**SQLGetDiagRec**的调用将返回SQL_INVALID_HANDLE，该操作表示共享环境句柄。 但是，如果*HandleType* SQL_HANDLE_ENV，*则句柄*可以是共享环境句柄，也可以是非共享环境句柄。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|获取诊断记录的字段或诊断标头的字段|[SQLGetDiagField 函数](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 标题文件](../../../odbc/reference/install/odbc-header-files.md)   
 [示例 ODBC 程序](../../../odbc/reference/sample-odbc-program.md)
