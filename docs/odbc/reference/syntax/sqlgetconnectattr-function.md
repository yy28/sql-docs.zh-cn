---
title: SQLGetConnectAttr 函数 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e6076f14ff0c33fec38b99e9c43b8a688970a7a9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285627"
---
# <a name="sqlgetconnectattr-function"></a>SQLGetConnectAttr 函数
**一致性**  
 推出版本： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLGetConnectAttr**返回连接属性的当前设置。  
  
> [!NOTE]
>  有关驱动程序管理器将此功能映射到 ODBC 3 *.x*应用程序使用 ODBC 2 *.x*驱动程序时的详细信息，请参阅[映射应用程序向后兼容性的替换函数](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
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
 *连接句柄*  
 [输入] 连接句柄。  
  
 *特性*  
 [输入]要检索的属性。  
  
 *ValuePtr*  
 [输出]指向内存的指针，用于返回*属性*指定的属性的当前值。 对于整数类型属性，某些驱动程序可能只写入缓冲区的较低 32 位或 16 位，并且保持高阶位不变。 因此，应用程序应在调用此函数之前使用 SQLULEN 的缓冲区并将该值初始化为 0。  
  
 如果*ValuePtr*为 NULL，*则 StringLengthPtr*仍将返回可用返回*ValuePtr*指向的缓冲区中的字节总数（不包括字符数据的空终止字符）。  
  
 *缓冲区长度*  
 [输入]如果*属性*是 ODBC 定义的属性 *，ValuePtr*指向字符串或二进制缓冲区，则此参数应为\**ValuePtr*的长度。 如果*属性*是 ODBC 定义的属性\**，ValuePtr*是整数，则忽略*缓冲区长度*。 如果*\*ValuePtr*中的值是 Unicode 字符串（在调用**SQLGetConnectAttrW**时），*缓冲区长度*参数必须是偶数。  
  
 如果*属性*是驱动程序定义的属性，则应用程序通过设置*BufferLength*参数指示该属性对驱动程序管理器的性质。 *缓冲区长度*可以具有以下值：  
  
-   如果*\*ValuePtr*是指向字符串的指针，*则缓冲区长度*是字符串的长度。  
  
-   如果*\*ValuePtr*是指向二进制缓冲区的指针，则应用程序将SQL_LEN_BINARY_ATTR（*长度*）宏的结果放在*缓冲区长度*中。 这将在*缓冲区长度*中放置负值。  
  
-   如果*\*ValuePtr*是指向字符串或二进制字符串以外的值的指针，*则 BufferLength*应具有该值SQL_IS_POINTER。  
  
-   如果*\*ValuePtr*包含固定长度的数据类型，则*缓冲区长度*SQL_IS_INTEGER或SQL_IS_UINTEGER（视适用）。  
  
 *字符串长度 Ptr*  
 [输出]指向缓冲区的指针，用于返回可在\**ValuePtr*中返回的字节总数（不包括空终止字符）。 如果\* *ValuePtr*是空指针，则不返回任何长度。 如果属性值是字符串，并且可供返回的字节数大于*BufferLength*减去空终止字符的长度，则*\*ValuePtr*中的数据将截断为*BufferLength*减去空终止字符的长度，并且驱动程序为 null 终止。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetConnectAttr**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec，** 使用SQL_HANDLE_DBC的*句柄和**连接句柄*从诊断数据结构获取关联的 SQLSTATE*Handle*值。 下表列出了**SQLGetConnectAttr**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01004|字符串数据，右截断|\* *ValuePtr*中返回的数据被截断为*缓冲区长度*减去空终止字符的长度。 未压缩字符串值的长度在 #*StringLengthPtr*中返回。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|08003|连接未打开|（DM） 指定了需要打开连接*的属性*值。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagField**中的参数*MessageText*从诊断数据结构返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY010|函数序列错误|（DM） **SQLBrowseConnect**被调用用于*连接句柄*并返回SQL_NEED_DATA。 在**SQLBrowseConnect**返回SQL_SUCCESS_WITH_INFO或SQL_SUCCESS之前调用此功能。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用用于*连接处理*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY090|无效的字符串或缓冲区长度|（DM） * \*ValuePtr*是一个字符串，缓冲区长度小于零但不等于SQL_NTS。|  
|HY092|无效属性/选项标识符|为参数*属性*指定的值对于驱动程序支持的 ODBC 版本无效。|  
|HY114|驱动程序不支持连接级异步函数执行|（DM） 应用程序尝试为不支持异步连接操作的驱动程序启用具有SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE异步函数执行。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现可选功能|为参数*属性*指定的值是驱动程序支持的 ODBC 版本的有效 ODBC 连接属性，但驱动程序不支持该属性。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 对应于*连接句柄*的驱动程序不支持该功能。|  
  
## <a name="comments"></a>注释  
 有关连接属性的一般信息，请参阅[连接属性](../../../odbc/reference/develop-app/connection-attributes.md)。  
  
 有关可以设置的属性列表，请参阅[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。 请注意，如果*属性*指定返回字符串的属性 *，ValuePtr*必须是指向字符串缓冲区的指针。 返回的字符串（包括空终止字符）的最大长度将为*BufferLength*字节。  
  
 根据属性，应用程序在调用**SQLGetConnectAttr**之前不必建立连接。 但是，如果调用**SQLGetConnectAttr**并且指定的属性没有默认值，并且未通过事先调用**SQLSetConnectAttr**设置，**则 SQLGetConnectAttr**将返回SQL_NO_DATA。  
  
 如果*属性*SQL_ATTR_ TRACE 或 SQL_ATTR_ TRACEFILE，*则连接句柄*不必有效，如果*连接句柄*无效 **，SQLGetConnectAttr**将不会返回SQL_ERROR或SQL_INVALID_HANDLE。 这些属性适用于所有连接。 如果另一个参数无效 **，SQLGetConnectAttr**将返回SQL_ERROR或SQL_INVALID_HANDLE。  
  
 尽管应用程序可以使用**SQLSetConnectAttr**设置语句属性，但应用程序不能使用**SQLGetConnectAttr**来检索语句属性值;因此，应用程序无法使用 SQLGetConnectAttr 来检索语句属性值。它必须调用**SQLGetStmtAttr**来检索语句属性的设置。  
  
 SQL_ATTR_AUTO_IPD和SQL_ATTR_CONNECTION_DEAD连接属性都可以通过调用**SQLGetConnectAttr**返回，但不能通过调用**SQLSetConnectAttr**来设置。  
  
> [!NOTE]  
>  **SQLGetConnectAttr**没有异步支持。 实现**SQLGetConnectAttr**时，驱动程序可以通过最大限度地减少从服务器发送或请求信息的次数来提高性能。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|返回语句属性的设置|[SQLGetStmtAttr 函数](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|设置连接属性|[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|设置环境属性|[SQLSetEnvAttr 函数](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|设置语句属性|[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
