---
title: "SQLGetDescRec 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLGetDescRec
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLGetDescRec
helpviewer_keywords: SQLGetDescRec function [ODBC]
ms.assetid: 325e0907-8e87-44e8-a111-f39e636a9cbc
caps.latest.revision: "30"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 569a3708c13a4182e651c902ce7e1f1f9c7711dd
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgetdescrec-function"></a>SQLGetDescRec 函数
**一致性**  
 版本引入了： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLGetDescRec**返回当前设置或多个字段的描述符记录的值。 描述返回的字段的名称、 数据类型和列或参数的数据的存储。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLGetDescRec(  
      SQLHDESC        DescriptorHandle,  
      SQLSMALLINT     RecNumber,  
      SQLCHAR *       Name,  
      SQLSMALLINT     BufferLength,  
      SQLSMALLINT *   StringLengthPtr,  
      SQLSMALLINT *   TypePtr,  
      SQLSMALLINT *   SubTypePtr,  
      SQLLEN *        LengthPtr,  
      SQLSMALLINT *   PrecisionPtr,  
      SQLSMALLINT *   ScalePtr,  
      SQLSMALLINT *   NullablePtr);  
```  
  
## <a name="arguments"></a>参数  
 *DescriptorHandle*  
 [输入]描述符句柄。  
  
 *RecNumber*  
 [输入]指示应用程序从中查找信息的描述符记录。 描述符记录从 1，与记录号 0 表示的书签记录编号。 *RecNumber*参数必须小于或等于 SQL_DESC_COUNT 的值。 如果*RecNumber*小于或等于 SQL_DESC_COUNT 但行不包含数据的列或参数中，调用**SQLGetDescRec**将返回字段的默认值。 (有关详细信息，请参阅"描述符字段的初始化" [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。)  
  
 *名称*  
 [输出]指向要返回的描述符记录 SQL_DESC_NAME 字段在其中的缓冲区的指针。  
  
 如果*名称*为 NULL， *StringLengthPtr*仍将返回的字符 （不包括字符数据的 null 终止字符） 总数可用于返回指向由的缓冲区中*名称*。  
  
 *BufferLength*  
 [输入]长度 **名称*缓冲区，以字符为单位。  
  
 *StringLengthPtr*  
 [输出]指向在其中以返回可用于在中返回数据的字符数的缓冲区的指针\**名称*缓冲区，不包括 null 终止字符。 字符数是否大于或等于*BufferLength*中的数据\**名称*截断为*BufferLength*的长度减null 终止字符，且由驱动程序以 null 结尾。  
  
 *TypePtr*  
 [输出]指向在其中为返回描述符记录的 SQL_DESC_TYPE 字段的值的缓冲区的指针。  
  
 *SubTypePtr*  
 [输出]对于其类型为 SQL_DATETIME 或 SQL_INTERVAL 的记录，这是指向在其中以返回 SQL_DESC_DATETIME_INTERVAL_CODE 字段的值的缓冲区的指针。  
  
 *LengthPtr*  
 [输出]指向在其中为返回描述符记录的 SQL_DESC_OCTET_LENGTH 字段的值的缓冲区的指针。  
  
 *PrecisionPtr*  
 [输出]指向在其中为返回描述符记录的 SQL_DESC_PRECISION 字段的值的缓冲区的指针。  
  
 *ScalePtr*  
 [输出]指向在其中为返回描述符记录的 SQL_DESC_SCALE 字段的值的缓冲区的指针。  
  
 *NullablePtr*  
 [输出]指向在其中为返回描述符记录的 SQL_DESC_NULLABLE 字段的值的缓冲区的指针。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 SQL_NO_DATA 或 SQL_INVALID_HANDLE。  
  
 如果返回 SQL_NO_DATA *RecNumber*大于当前的描述符记录数。  
  
 如果返回 SQL_NO_DATA *DescriptorHandle* IRD 句柄和语句处于已准备或执行状态但没有任何与其关联的打开光标。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetDescRec**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_DESC 和*处理*的*DescriptorHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLGetDescRec**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|缓冲区\**名称*不是否足够大以返回整个描述符字段。 因此，该字段已被截断。 在中返回未截断的描述符字段的长度 **StringLengthPtr*。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07009|无效的描述符索引|*FieldIdentifier*自变量为记录字段中， *RecNumber*参数已设置为 0，和*DescriptorHandle*自变量为 IPD 句柄。<br /><br /> (DM) *RecNumber*参数已设置为 0，且 SQL_ATTR_USE_BOOKMARKS 语句属性被设置为 SQL_UB_OFF，和*DescriptorHandle*自变量为 IRD 句柄。<br /><br /> *RecNumber*自变量为小于 0。|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已连接到数据源之间的通信链接。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY007|未准备关联的语句|*DescriptorHandle* IRD，与关联和关联的语句句柄当时不处于已准备或执行状态。|  
|HY010|函数序列错误|(DM) *DescriptorHandle*与关联*StatementHandle*其中一个以异步方式执行的函数 （而不此是） 调用和仍在执行时调用此函数。<br /><br /> (DM) *DescriptorHandle*与关联*StatementHandle*为其**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**成功调用并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。<br /><br /> (DM) 为与关联的连接句柄调用以异步方式执行的函数*DescriptorHandle*。 此异步函数仍在执行时**SQLGetDescRec**调用。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*DescriptorHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 应用程序可以调用**SQLGetDescRec**检索以下描述符字段的单个列或参数的值：  
  
-   SQL_DESC_NAME  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE （对于其类型为 SQL_DATETIME 或 SQL_INTERVAL 记录）  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_NULLABLE  
  
 **SQLGetDescRec**未检索标头字段的值。  
  
 应用程序可以通过将对应的自变量设置为 null 指针的字段来防止返回的字段的设置。  
  
 在应用程序调用**SQLGetDescRec**若要检索没有为特定描述符类型定义的字段的值，该函数将返回 SQL_SUCCESS 但返回为该字段的值是不确定。 例如，调用**SQLGetDescRec**对于 APD 或 ARD 的 SQL_DESC_NAME 或 SQL_DESC_NULLABLE 字段将返回 SQL_SUCCESS 但未定义的字段的值。  
  
 在应用程序调用**SQLGetDescRec**若要检索的字段为特定描述符类型定义但，没有默认值，并且尚未设置的值，该函数将返回 SQL_SUCCESS 但返回值该字段是未定义。 有关详细信息，请参阅"描述符字段的初始化" [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。  
  
 字段的值也可单独通过调用**SQLGetDescField**。 中的描述符标头或记录的字段的说明，请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。 有关描述符的详细信息，请参阅[描述符](../../../odbc/reference/develop-app/descriptors.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|绑定列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|将参数绑定|[SQLBindParameter 函数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|获取描述符字段|[SQLGetDescField 函数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|设置多个描述符字段|[SQLSetDescRec 函数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
