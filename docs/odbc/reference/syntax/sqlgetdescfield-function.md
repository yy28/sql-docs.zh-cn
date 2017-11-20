---
title: "SQLGetDescField 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1cbf48f5346d507505573391598cbd98017ccd8d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetdescfield-function"></a>SQLGetDescField 函数
**一致性**  
 版本引入了： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLGetDescField**返回的当前设置或描述符记录的单个字段的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
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
 [输入]指示应用程序从中查找信息的描述符记录。 描述符记录与记录号 0 表示的书签记录编号从 0。 如果*FieldIdentifier*自变量表示标头字段， *RecNumber*将被忽略。 如果*RecNumber*小于或等于 SQL_DESC_COUNT 但行不包含数据的列或参数中，调用**SQLGetDescField**将返回字段的默认值。 (有关详细信息，请参阅"描述符字段的初始化" [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。)  
  
 *FieldIdentifier*  
 [输入]表示其值是要返回的描述符字段。 有关详细信息，请参阅"*FieldIdentifier*自变量"部分中[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。  
  
 *ValuePtr*  
 [输出]指向要返回其描述符信息中的缓冲区的指针。 数据类型的值取决于*FieldIdentifier*。  
  
 如果*ValuePtr*是整数类型、 应用程序应使用的缓冲区 SQLULEN 和初始化为 0 的值之前调用此函数为某些驱动程序可能仅写入的低 32 位或 16 位的缓冲区并使较高顺序位保持不变。  
  
 如果*ValuePtr*为 NULL， *StringLengthPtr*仍将返回的 （不包括字符数据的 null 终止字符） 的字节总数可用于返回指向由的缓冲区中*ValuePtr*。  
  
 *BufferLength*  
 [输入]如果*FieldIdentifier*是一个 ODBC 定义的字段和*ValuePtr*指向字符字符串或二进制缓冲区时，此参数应为的长度\* *ValuePtr*. 如果*FieldIdentifier*是一个 ODBC 定义的字段和\* *ValuePtr*是一个整数， *BufferLength*将被忽略。 如果中的值 *\*ValuePtr* Unicode 数据类型 (在调用时**SQLGetDescFieldW**)，则*BufferLength*参数必须为偶数。  
  
 如果*FieldIdentifier*是驱动程序定义的字段，该应用程序通过设置来指明字段到驱动程序管理器的性质*BufferLength*自变量。 *BufferLength*可以具有下列值：  
  
-   如果 *\*ValuePtr*然后是指向字符串， *BufferLength*是字符串或 sql_nts 以的长度。  
  
-   如果 *\*ValuePtr*为指向二进制缓冲区的指针，则将 SQL_LEN_BINARY_ATTR 结果放置于应用程序 (*长度*) 中的宏*BufferLength*。 这会在负值*BufferLength*。  
  
-   如果 *\*ValuePtr*然后是指向字符字符串或二进制字符串以外的值的*BufferLength*应具有 SQL_IS_POINTER 的值。  
  
-   如果 *\*ValuePtr*是包含固定长度的数据类型，则*BufferLength*是 SQL_IS_INTEGER、 SQL_IS_UINTEGER、 SQL_IS_SMALLINT 或 SQL_IS_USMALLINT，根据需要。  
  
 *StringLengthPtr*  
 [输出]指向要返回的 （不包括所需的 null 终止字符的字节数） 的字节总数在其中缓冲区指针可用于返回在 **ValuePtr*。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 SQL_NO_DATA 或 SQL_INVALID_HANDLE。  
  
 如果返回 SQL_NO_DATA *RecNumber*大于当前的描述符记录数。  
  
 如果返回 SQL_NO_DATA *DescriptorHandle* IRD 句柄和语句处于已准备或执行状态但没有任何与其关联的打开光标。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetDescField**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用获取**SQLGetDiagRec**与*HandleType*的SQL_HANDLE_STMT 和*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLGetDescField**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|缓冲区\* *ValuePtr*不是否足够大以返回整个描述符字段中，因此该字段已被截断。 在中返回未截断的描述符字段的长度 **StringLengthPtr*。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07009|无效的描述符索引|(DM) *RecNumber*参数已等于 0、 SQL_ATTR_USE_BOOKMARK 语句属性 SQL_UB_OFF，和*DescriptorHandle*自变量为 IRD 句柄。 （此错误可以显式分配的描述符仅当才能返回的描述符与语句句柄关联。）<br /><br /> *FieldIdentifier*自变量为记录字段中， *RecNumber*自变量为 0，和*DescriptorHandle*自变量为 IPD 句柄。<br /><br /> *RecNumber*自变量为小于 0。|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已连接到数据源之间的通信链接。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY007|未准备关联的语句|*DescriptorHandle*与关联*StatementHandle* IRD，以及相关联的语句句柄具有尚未准备或执行。|  
|HY010|函数序列错误|(DM) *DescriptorHandle*与关联*StatementHandle*其中一个以异步方式执行的函数 （而不此是） 调用和仍在执行时调用此函数。<br /><br /> (DM) *DescriptorHandle*与关联*StatementHandle*为其**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**成功调用并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。<br /><br /> (DM) 为与关联的连接句柄调用以异步方式执行的函数*DescriptorHandle*。 此异步函数仍在执行时**SQLGetDescField**调用函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY021|描述符信息不一致|SQL_DESC_TYPE 和 SQL_DESC_DATETIME_INTERVAL_CODE 字段不构成有效的 ODBC SQL 类型、 有效的特定于驱动程序的 SQL 类型 （用于 IPDs) 或有效的 ODBC C 类型 （对于 APDs 或 ARDs）。|  
|HY090|字符串或缓冲区长度无效|(DM)  *\*ValuePtr*为字符字符串，和*BufferLength*小于零。|  
|HY091|描述符字段标识符无效|*FieldIdentifier*不 ODBC 定义的字段，且不为实现定义的值。<br /><br /> *FieldIdentifier*未定义为*DescriptorHandle*。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*DescriptorHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 应用程序可以调用**SQLGetDescField**以返回单个字段的描述符记录的值。 调用**SQLGetDescField**可以在任何描述符类型，包括标头字段、 记录字段和书签字段中返回任何字段的设置。 应用程序可以通过重复调用来获取的相同或不同的描述符，按任意顺序中的多个字段的设置**SQLGetDescField**。 **SQLGetDescField**还可以调用返回驱动程序定义描述符字段。  
  
 出于性能原因，应用程序不应调用**SQLGetDescField**为 IRD 之前执行语句。  
  
 此外可以对单个调用中检索描述了名称、 数据类型和列或参数的数据的存储的多个字段的设置**SQLGetDescRec**。 **SQLGetStmtAttr**可以调用以返回单个字段的设置也是一个语句属性描述符标头中。 **SQLColAttribute**， **SQLDescribeCol**，和**SQLDescribeParam**返回记录或书签的字段。  
  
 在应用程序调用**SQLGetDescField**若要检索没有为特定描述符类型定义的字段的值，该函数将返回 SQL_SUCCESS 但返回为该字段的值是不确定。 例如，调用**SQLGetDescField**对于 APD 或 ARD 的 SQL_DESC_NAME 或 SQL_DESC_NULLABLE 字段将返回 SQL_SUCCESS 但未定义的字段的值。  
  
 在应用程序调用**SQLGetDescField**若要检索的字段为特定描述符类型定义但，没有默认值，并且尚未设置的值，该函数将返回 SQL_SUCCESS 但返回值为该字段是不确定。 有关描述符字段和字段的说明的初始化详细信息，请参阅"描述符字段的初始化" [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。 有关描述符的详细信息，请参阅[描述符](../../../odbc/reference/develop-app/descriptors.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|获取多个描述符字段|[SQLGetDescRec 函数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|设置单个描述符字段|[SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|设置多个描述符字段|[SQLSetDescRec 函数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)

