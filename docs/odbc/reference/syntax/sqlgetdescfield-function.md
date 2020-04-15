---
title: SQLGetDescfield 函数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDescField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDescField
helpviewer_keywords:
- SQLGetDescField function [ODBC]
ms.assetid: f09ff660-1e4a-4370-be85-90d4da0487d3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89972d7f36b436868cc8e243b03827f095b90492
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285471"
---
# <a name="sqlgetdescfield-function"></a>SQLGetDescField 函数
**一致性**  
 推出版本： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLGetDescField**返回描述符记录的单个字段的当前设置或值。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLGetDescField(  
     SQLHDESC        DescriptorHandle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     FieldIdentifier,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```  
  
## <a name="arguments"></a>参数  
 *DescriptorHandle*  
 [输入]描述符句柄。  
  
 *RecNumber*  
 [输入]指示应用程序从中查找信息的描述符记录。 描述符记录从 0 编号，记录编号 0 是书签记录。 如果*字段标识符*参数指示标题字段，则*忽略 RecNumber。* 如果*RecNumber*小于或等于SQL_DESC_COUNT但该行不包含列或参数的数据，则对**SQLGetDescField**的调用将返回字段的默认值。 （有关详细信息，请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中的"描述字段的初始化"。  
  
 *FieldIdentifier*  
 [输入]指示要返回其值的描述符的字段。 有关详细信息，请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中的"*字段标识符*参数"部分。  
  
 *ValuePtr*  
 [输出]指向要返回描述符信息的缓冲区的指针。 数据类型取决于*字段标识符*的值。  
  
 如果*ValuePtr*是整数类型，则应用程序应使用 SQLULEN 的缓冲区，并在调用此函数之前将值初始化为 0，因为某些驱动程序可能只写入缓冲区的较低 32 位或 16 位，并且保持高阶位不变。  
  
 如果*ValuePtr*为 NULL，*则 StringLengthPtr*仍将返回可用返回*ValuePtr*指向的缓冲区中的字节总数（不包括字符数据的空终止字符）。  
  
 *缓冲区长度*  
 [输入]如果*Field标识符*是 ODBC 定义的字段 *，ValuePtr*指向字符串或二进制缓冲区，则此参数应为\**ValuePtr*的长度。 如果*字段标识符*是 ODBC 定义的字段\**，ValuePtr*是整数，则忽略*缓冲区长度*。 如果*\*ValuePtr*中的值是 Unicode 数据类型（在调用**SQLGetDescFieldW**时），*缓冲区长度*参数必须是偶数。  
  
 如果*Field标识符*是驱动程序定义的字段，则应用程序通过设置*BufferLength*参数向驱动程序管理器指示该字段的性质。 *缓冲区长度*可以具有以下值：  
  
-   如果*\*ValuePtr*是指向字符串的指针，则*缓冲区长度*是字符串的长度或SQL_NTS。  
  
-   如果*\*ValuePtr*是指向二进制缓冲区的指针，则应用程序将SQL_LEN_BINARY_ATTR（*长度*）宏的结果放在*缓冲区长度*中。 这将在*缓冲区长度*中放置负值。  
  
-   如果*\*ValuePtr*是指向字符串或二进制字符串以外的值的指针，则*BufferLength*应具有该值SQL_IS_POINTER。  
  
-   如果*\*ValuePtr*包含固定长度的数据类型，则*缓冲区长度*是SQL_IS_INTEGER、SQL_IS_UINTEGER、SQL_IS_SMALLINT或SQL_IS_USMALLINT（视适用）。  
  
 *字符串长度 Ptr*  
 [输出]指向要返回在 #*ValuePtr*中返回的字节总数（不包括空终止字符所需的字节数）的缓冲区的指针。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_NO_DATA或SQL_INVALID_HANDLE。  
  
 如果*RecNumber*大于当前描述符记录数，则返回SQL_NO_DATA。  
  
 如果*描述符句柄*是 IRD 句柄，并且语句处于准备或执行状态，但没有与其关联的打开游标，则返回SQL_NO_DATA。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetDescField**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_STMT的*句柄类型*和*语句句柄*的*句柄*。 下表列出了**SQLGetDescField**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01004|字符串数据，右截断|缓冲区\* *ValuePtr*不够大，无法返回整个描述符字段，因此该字段被截断。 未压缩的描述符字段的长度在 #*StringLengthPtr*中返回。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|07009|无效描述符索引|（DM） *RecNumber*参数等于 0，SQL_ATTR_USE_BOOKMARK语句属性SQL_UB_OFF，*描述符句柄*参数是 IRD 句柄。 （仅当描述符与语句句柄关联时，才能为显式分配的描述符返回此错误。<br /><br /> *字段标识符*参数是记录字段 *，RecNumber*参数为 0，*描述符句柄*参数是 IPD 句柄。<br /><br /> *RecNumber*参数小于 0。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY007|未准备关联语句|*描述符句柄*作为 IRD 与*语句句柄*相关联，并且关联的语句句柄尚未准备或执行。|  
|HY010|函数序列错误|（DM）*描述符处理*与*语句句柄*相关联，在调用此函数时，调用了异步执行函数（不是此函数），并且仍在执行。<br /><br /> （DM）*描述符句柄*与*语句句柄*相关联，SQL_NEED_DATA调用并返回 SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLExecute****SQLExecDirect****SQLSetPos。** 在发送所有执行时数据参数或列的数据之前，调用了此功能。<br /><br /> （DM） 对于与*描述符句柄*关联的连接句柄，调用了异步执行函数。 调用**SQLGetDescField**函数时，此异步函数仍在执行。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY021|描述符信息不一致|SQL_DESC_TYPE字段和SQL_DESC_DATETIME_INTERVAL_CODE字段不形成有效的 ODBC SQL 类型、有效的特定于驱动程序的 SQL 类型（对于 IPD）或有效的 ODBC C 类型（对于 AD 或 AD）。|  
|HY090|无效的字符串或缓冲区长度|（DM） * \*ValuePtr*是一个字符串，*缓冲区长度*小于零。|  
|HY091|无效描述符字段标识符|*字段标识符*不是 ODBC 定义的字段，不是实现定义的值。<br /><br /> 对于*描述符处理*，未定义*字段标识符*。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*描述符处理*关联的驱动程序不支持该函数。|  
  
## <a name="comments"></a>注释  
 应用程序可以调用**SQLGetDescField**来返回描述符记录的单个字段的值。 对**SQLGetDescField**的调用可以返回任何描述符类型中的任何字段的设置，包括标头字段、记录字段和书签字段。 应用程序可以通过对**SQLGetDescField**进行重复调用，以任意顺序获取相同或不同描述符中的多个字段的设置。 也可以调用**SQLGetDescField**来返回驱动程序定义的描述符字段。  
  
 出于性能原因，应用程序在执行语句之前不应调用**SQLGetDescField**进行 IRD。  
  
 在**SQLGetDescRec**的单个调用中，还可以检索描述列或参数数据的名称、数据类型和存储的多个字段的设置。 可以调用**SQLGetStmtAttr**来返回描述符标头中单个字段的设置，该字段也是语句属性。 **SQLCol属性****、SQL描述科尔**和**SQL 描述Param**返回记录或书签字段。  
  
 当应用程序调用**SQLGetDescField**检索特定描述符类型未定义的字段的值时，该函数返回SQL_SUCCESS但返回该字段的值未定义。 例如，为 APD 或 ARD 的SQL_DESC_NAME或SQL_DESC_NULLABLE字段调用**SQLGetDescField**将返回SQL_SUCCESS但字段的未定义值。  
  
 当应用程序调用**SQLGetDescField**检索为特定描述符类型定义但尚未设置默认值但尚未设置的字段的值时，该函数返回SQL_SUCCESS但返回该字段的值未定义。 有关描述符字段的初始化和字段描述的详细信息，请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中的"描述符字段的初始化"。 有关描述符的详细信息，请参阅[描述符](../../../odbc/reference/develop-app/descriptors.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|获取多个描述符字段|[SQLGetDescRec 函数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|设置单个描述符字段|[SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|设置多个描述符字段|[SQLSetDescRec 函数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
