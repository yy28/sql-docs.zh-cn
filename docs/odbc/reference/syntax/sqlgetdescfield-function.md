---
title: SQLGetDescField 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cdf2990056c297d217248543812e347b61d3486d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103816"
---
# <a name="sqlgetdescfield-function"></a>SQLGetDescField 函数
**符合性**  
 版本引入了：ODBC 3.0 标准符合性：ISO 92  
  
 **摘要**  
 **SQLGetDescField**返回当前设置或描述符记录的单个字段的值。  
  
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
 [输入]指示从其应用程序查找信息的描述符记录。 描述符记录编号介于 0，使用 0 表示的书签记录的记录号。 如果*FieldIdentifier*参数指示的标头字段， *RecNumber*将被忽略。 如果*RecNumber*小于或等于 SQL_DESC_COUNT 但行不包含数据的列或参数，调用**SQLGetDescField**将返回的字段的默认值。 (详细信息，请参阅"初始化的描述符字段"中[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。)  
  
 *FieldIdentifier*  
 [输入]表示其值是要返回的描述符字段。 有关详细信息，请参阅"*FieldIdentifier*自变量"部分中[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。  
  
 *ValuePtr*  
 [输出]指向缓冲区中要返回其描述符信息。 数据类型取决于的值*FieldIdentifier*。  
  
 如果*ValuePtr*是整数类型、 应用程序应使用的缓冲区 sqlulen 生成和初始化为 0 的值之前调用此函数为某些驱动程序可能仅写入的低 32 位或 16 位的缓冲区和保留较高顺序位保持不变。  
  
 如果*ValuePtr*为 NULL， *StringLengthPtr*仍将返回的总字节数 （不包括字符数据的 null 终止字符） 可用于在通过指向的缓冲区中返回*ValuePtr*。  
  
 *BufferLength*  
 [输入]如果*FieldIdentifier*是一个 ODBC 定义的字段和*ValuePtr*指向字符字符串或二进制缓冲区中，此参数应为的长度\* *ValuePtr*. 如果*FieldIdentifier*是一个 ODBC 定义的字段和\* *ValuePtr*是一个整数*BufferLength*将被忽略。 如果中的值 *\*ValuePtr* Unicode 数据类型 (在调用时**SQLGetDescFieldW**)，则*BufferLength*参数必须为偶数。  
  
 如果*FieldIdentifier*是驱动程序定义的字段，该应用程序通过设置来指示字段到驱动程序管理器的性质*BufferLength*参数。 *BufferLength*可以具有以下值：  
  
-   如果 *\*ValuePtr*是指向字符字符串，则*BufferLength*是 sql_nts; 的字符串的长度。  
  
-   如果 *\*ValuePtr*是指向二进制缓冲区的指针，则 SQL_LEN_BINARY_ATTR 将结果放置于该应用程序 (*长度*) 中的宏*BufferLength*。 这会在负值*BufferLength*。  
  
-   如果 *\*ValuePtr*是指向字符的字符串或二进制字符串以外的值，则*BufferLength*应具有 SQL_IS_POINTER 的值。  
  
-   如果 *\*ValuePtr*是包含固定长度的数据类型，然后*BufferLength*是 SQL_IS_INTEGER、 SQL_IS_UINTEGER、 SQL_IS_SMALLINT 或 SQL_IS_USMALLINT，根据需要。  
  
 *StringLengthPtr*  
 [输出]指向用于返回的总字节数 （不包括 null 终止字符所需的字节数） 缓冲区的指针可用于在返回 **ValuePtr*。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 SQL_NO_DATA 或 SQL_INVALID_HANDLE。  
  
 如果返回 SQL_NO_DATA *RecNumber*大于当前的描述符记录数。  
  
 如果返回 SQL_NO_DATA *DescriptorHandle* IRD 句柄和该语句是在准备或执行状态但没有与之关联的任何打开的游标。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetDescField**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用来获取**SQLGetDiagRec**与*HandleType*的SQL_HANDLE_STMT 和一个*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLGetDescField** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|Error|描述|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|缓冲区\* *ValuePtr*是否不足够大以返回整个描述符字段，以便该字段已被截断。 在返回未截断的描述符字段的长度 **StringLengthPtr*。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07009|描述符索引无效|（数据挖掘） *RecNumber*参数为等于 0，SQL_ATTR_USE_BOOKMARK 语句属性是 SQL_UB_OFF，并*DescriptorHandle*参数为 IRD 句柄。 （返回此错误可以是显式分配的描述符只能如果描述符与语句句柄相关联。）<br /><br /> *FieldIdentifier*自变量是一个记录字段中， *RecNumber*参数为 0，并且*DescriptorHandle*参数为 IPD 句柄。<br /><br /> *RecNumber*参数为小于 0。|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY007|未准备关联的语句|*DescriptorHandle*与关联*StatementHandle* IRD 和相关联的语句句柄必须尚未准备或执行。|  
|HY010|函数序列错误|（数据挖掘） *DescriptorHandle*与关联*StatementHandle*其中 （而不此是） 的异步执行函数调用和仍在执行时调用此函数。<br /><br /> （数据挖掘） *DescriptorHandle*与关联*StatementHandle*为其**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**调用和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。<br /><br /> (DM) 为与之关联的连接句柄调用以异步方式执行的函数*DescriptorHandle*。 此异步函数仍在执行时**SQLGetDescField**调用函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY021|描述符信息不一致|SQL_DESC_TYPE 和 SQL_DESC_DATETIME_INTERVAL_CODE 字段未形成有效的 ODBC SQL 类型、 有效的特定于驱动程序的 SQL 类型 （适用于 Ipd) 或有效的 ODBC C 类型 （适用于 Apd 或 ARDs）。|  
|HY090|字符串或缓冲区长度无效|（数据挖掘）  *\*ValuePtr*是一个字符串，并*BufferLength*小于零。|  
|HY091|描述符字段标识符无效|*FieldIdentifier*不 ODBC 定义的字段，而且不是实现定义的值。<br /><br /> *FieldIdentifier*未定义的有关*DescriptorHandle*。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*DescriptorHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 应用程序可以调用**SQLGetDescField**以返回单个字段的描述符记录的值。 调用**SQLGetDescField**可在任何描述符类型，包括标头字段、 记录字段和书签字段中返回的任何字段的设置。 应用程序可以通过重复的调用来获得相同或不同描述符，按任意顺序中的多个字段的设置**SQLGetDescField**。 **SQLGetDescField**也可以调用返回驱动程序定义的描述符字段。  
  
 出于性能原因，应用程序不应调用**SQLGetDescField** IRD 语句之前执行的。  
  
 也可以对单个调用中检索描述名称、 数据类型和列或参数的数据的存储的多个字段的设置**SQLGetDescRec**。 **SQLGetStmtAttr**可以调用也是语句属性的描述符标头中返回单个字段的设置。 **SQLColAttribute**， **SQLDescribeCol**，和**SQLDescribeParam**返回记录或书签的字段。  
  
 当应用程序调用**SQLGetDescField**若要检索特定的描述符类型未定义的字段的值，该函数将返回 SQL_SUCCESS，但返回的字段的值是未定义。 例如，调用**SQLGetDescField** APD 或 ARD SQL_DESC_NAME 或 SQL_DESC_NULLABLE 字段将返回 SQL_SUCCESS，但未定义的字段的值。  
  
 当应用程序调用**SQLGetDescField**要检索的字段为特定的描述符类型定义但，没有默认值，并且尚未设置值，该函数将返回 SQL_SUCCESS 但返回值为该字段是未定义。 描述符字段和字段的说明的初始化详细信息，请参阅"初始化的描述符字段"中[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。 描述符的详细信息，请参阅[描述符](../../../odbc/reference/develop-app/descriptors.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|获取多个描述符字段|[SQLGetDescRec 函数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|设置单一的描述符字段|[SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|设置多个描述符字段|[SQLSetDescRec 函数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
