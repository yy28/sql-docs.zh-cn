---
title: SQLGetConnectAttr Function | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConnectAttr
helpviewer_keywords:
- SQLGetConnectAttr function [ODBC]
ms.assetid: 2cb4ffa8-19d3-4664-8c2f-6682cdcc3f33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7051c94e4883c57daab4d5706feb073323e1c371
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65538050"
---
# <a name="sqlgetconnectattr-function"></a>SQLGetConnectAttr 函数
**符合性**  
 版本引入了：ODBC 3.0 标准符合性：ISO 92  
  
 **摘要**  
 **SQLGetConnectAttr**返回连接属性的当前设置。  
  
> [!NOTE]
>  详细了解驱动程序管理器映射的内容到此函数时 ODBC 3 *.x*应用程序使用 ODBC 2 *.x*驱动程序，请参阅[用于向后映射替换函数应用程序的兼容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLGetConnectAttr(  
     SQLHDBC        ConnectionHandle,  
     SQLINTEGER     Attribute,  
     SQLPOINTER     ValuePtr,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>参数  
 *ConnectionHandle*  
 [输入] 连接句柄。  
  
 *Attribute*  
 [输入]要检索的特性。  
  
 *ValuePtr*  
 [输出]指向用于返回由指定的属性的当前值的内存的指针*属性*。 对于整数类型属性，某些驱动程序可能只能写入低 32 位或 16 位的缓冲区，并保留较高顺序位保持不变。 因此，应用程序应使用 sqlulen 生成的缓冲区，并调用此函数之前，初始化为 0 的值。  
  
 如果*ValuePtr*为 NULL， *StringLengthPtr*仍将返回的总字节数 （不包括字符数据的 null 终止字符） 可用于在通过指向的缓冲区中返回*ValuePtr*。  
  
 *BufferLength*  
 [输入]如果*特性*是一个 ODBC 定义的属性和*ValuePtr*指向字符字符串或二进制缓冲区中，此参数应为的长度\* *ValuePtr*. 如果*特性*是一个 ODBC 定义的属性和\* *ValuePtr*是一个整数*BufferLength*将被忽略。 如果中的值 *\*ValuePtr*是 Unicode 字符串 (在调用时**SQLGetConnectAttrW**)，则*BufferLength*参数必须为偶数。  
  
 如果*特性*是一个驱动程序定义的属性，该应用程序通过设置指示特性的驱动程序管理器的性质*BufferLength*参数。 *BufferLength*可以具有以下值：  
  
-   如果 *\*ValuePtr*是一个字符串，指向*BufferLength*是字符串的长度。  
  
-   如果 *\*ValuePtr* SQL_LEN_BINARY_ATTR 的结果是指向二进制缓冲区中，在应用程序的位置的指针 (*长度*) 中的宏*BufferLength*。 这会在负值*BufferLength*。  
  
-   如果 *\*ValuePtr*是指向字符的字符串或二进制字符串以外的值*BufferLength*应具有 SQL_IS_POINTER 的值。  
  
-   如果 *\*ValuePtr*包含一个固定长度的数据类型*BufferLength*是 SQL_IS_INTEGER 或 SQL_IS_UINTEGER，根据需要。  
  
 *StringLengthPtr*  
 [输出]指向在其中返回的总字节数 （不包括 null 终止字符） 的缓冲区的指针可用于在中返回\* *ValuePtr*。 如果\* *ValuePtr*是 null 指针，则返回任何长度。 如果属性值是一个字符串，并且可用于返回的字节数大于*BufferLength* null 终止字符中的数据的长度减去 *\*ValuePtr*截断为*BufferLength*减去的 null 终止字符的长度是由驱动程序以 null 结尾。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetConnectAttr**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用获取从诊断数据结构**SQLGetDiagRec** 与*HandleType*设为 SQL_HANDLE_DBC 和一个*处理*的*ConnectionHandle*。 下表列出了通常由返回的 SQLSTATE 值**SQLGetConnectAttr** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明. 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|中返回的数据\* *ValuePtr*已被截断为*BufferLength*减去 null 终止字符的长度。 在返回未截断的字符串值的长度 **StringLengthPtr*。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08003|连接未打开|（数据挖掘）*特性*指定所需的打开连接的值。|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 诊断数据结构中的参数返回的错误消息*MessageText*中**SQLGetDiagField**描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY010|函数序列错误|（数据挖掘） **SQLBrowseConnect**曾为*ConnectionHandle*和返回 SQL_NEED_DATA。 此函数调用之前**SQLBrowseConnect**返回 SQL_SUCCESS_WITH_INFO 或 SQL_SUCCESS。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*ConnectionHandle*和返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|（数据挖掘）  *\*ValuePtr*是一个字符串和 BufferLength 是小于零，但不是等于 SQL_NTS。|  
|HY092|属性/选项标识符无效|为参数指定的值*特性*对 ODBC 驱动程序支持的版本无效。|  
|HY114|驱动程序不支持连接级别异步函数执行|(DM) 应用程序尝试在启用 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 与驱动程序不支持异步连接操作的异步函数执行。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|为参数指定的值*特性*的 ODBC 版本支持的驱动程序，但不受驱动程序是一个有效的 ODBC 连接属性。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 对应的驱动程序*ConnectionHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 有关连接属性的常规信息，请参阅[连接属性](../../../odbc/reference/develop-app/connection-attributes.md)。  
  
 可以设置的属性的列表，请参阅[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。 请注意，如果*特性*指定返回的字符串的属性*ValuePtr*必须是指向字符串缓冲区的指针。 将返回的字符串，包括 null 终止字符的最大长度*BufferLength*字节。  
  
 具体取决于该属性，应用程序无需建立连接之前，调用**SQLGetConnectAttr**。 但是，如果**SQLGetConnectAttr**称为和指定的属性不具有默认值和调用之前尚未设置**SQLSetConnectAttr**， **SQLGetConnectAttr**将返回 sql_no_data 为止。  
  
 如果*特性*SQL_ATTR_ 跟踪或 SQL_ATTR_ TRACEFILE *ConnectionHandle*不必是有效的并且**SQLGetConnectAttr**不会返回 SQL_ERROR 或 SQL_INVALID_HANDLE 如果*ConnectionHandle*无效。 这些属性适用于所有连接。 **SQLGetConnectAttr**将返回 SQL_ERROR 或 SQL_INVALID_HANDLE 如果另一个参数无效。  
  
 尽管应用程序可以通过使用设置语句属性**SQLSetConnectAttr**，应用程序不能使用**SQLGetConnectAttr**若要检索的语句属性值; 它必须调用**SQLGetStmtAttr**检索的语句属性设置。  
  
 可以通过调用返回 SQL_ATTR_AUTO_IPD 和 SQL_ATTR_CONNECTION_DEAD 连接属性**SQLGetConnectAttr**但不能通过调用设置**SQLSetConnectAttr**。  
  
> [!NOTE]  
>  没有为异步支持**SQLGetConnectAttr**。 在实现时**SQLGetConnectAttr**，驱动程序可以通过最小化发送或从服务器请求信息的次数来提高性能。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|返回语句属性的设置|[SQLGetStmtAttr 函数](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|将连接属性设置|[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|设置一个环境属性|[SQLSetEnvAttr 函数](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|设置语句属性|[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
