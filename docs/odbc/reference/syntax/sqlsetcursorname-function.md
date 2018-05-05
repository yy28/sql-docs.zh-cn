---
title: SQLSetCursorName 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLSetCursorName
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetCursorName
helpviewer_keywords:
- SQLSetCursorName function [ODBC]
ms.assetid: 4e055946-12d4-4589-9891-41617a50f34e
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 64c560f2934d04b098ed26c347d2819d90948e5f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetcursorname-function"></a>SQLSetCursorName 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLSetCursorName**将游标名称与活动语句相关联。 如果应用程序不会调用**SQLSetCursorName**，驱动程序会根据需要为 SQL 语句处理产生游标名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLSetCursorName(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CursorName,  
     SQLSMALLINT   NameLength);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *cursorName*  
 [输入]游标名称。 针对高效处理游标名称不应在游标名称，包括任何前导空格或尾随空格和如果游标名称包括分隔的标识符，应作为游标名称中的第一个字符位于分隔符。  
  
 *NameLength*  
 [输入]以字符为单位的长度 **CursorName*。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLSetCursorName**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用获取**SQLGetDiagRec**与*HandleType*的SQL_HANDLE_STMT 和*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLSetCursorName**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|游标名称超出最大限制，因此使用仅最大允许的字符数。|  
|24000|无效的游标状态|语句对应于*StatementHandle*本来就处于或者位于光标位置上执行的状态。|  
|34000|无效的临时表名称|中指定的游标名称 **CursorName*无效，因为它超出了最大长度定义由驱动程序，或它入门"SQLCUR"或"SQL_CUR。"|  
|3C000|游标名称重复|中指定的游标名称 **CursorName*已存在。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY009|不允许使用 null 指针|(DM) 自变量*CursorName*是空指针。|  
|HY010|函数序列错误|(DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此 aynchronous 函数仍在执行时**SQLSetCursorName**调用函数。<br /><br /> (DM) 以异步方式执行的函数曾为*StatementHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 自变量*NameLength*小于 0，但与 sql_nts 以不相等。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*StatementHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 游标名称仅在中使用定位更新和 delete 语句 (例如，**更新***表名*...**WHERE CURRENT OF** *游标名称*)。 有关详细信息，请参阅[定位更新和删除语句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)。 如果应用程序不会调用**SQLSetCursorName**定义游标名称，在执行的查询语句，该驱动程序生成的名称以字母 SQL_CUR 开头且不超过 18 个字符的长度。  
  
 在连接内的所有游标名称必须都是唯一的。 游标名称的最大长度是由驱动程序定义的。 最大互操作性，建议应用程序，限制为不能超过 18 个字符的游标名称。 ODBC 3 中 *.x*，如果游标名称是带引号的标识符视为区分大小写的方式，它可以包含字符的 SQL 语法将不允许或将专门，如空白或保留关键字。 如果游标名称必须以区分大小写的方式处理，则它必须传递作为带引号的标识符。  
  
 游标名称设置显式或隐式保持设置之前使用删除它与之关联的语句**SQLFreeHandle**。 **SQLSetCursorName**可以调用以进行重命名语句中的游标，只要光标位于未分配或已准备状态。  
  
## <a name="code-example"></a>代码示例  
 在下面的示例中，应用程序使用**SQLSetCursorName**设置语句游标名称。 它然后使用该语句以从客户表中检索结果。 最后，它将执行的定位的更新，以更改为 John Smith 的电话号码。 请注意，应用程序使用不同的语句的处理程序**选择**和**更新**语句。  
  
 另一个代码示例，请参阅[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
```  
#define NAME_LEN 50  
#define PHONE_LEN 10  
  
SQLHSTMT     hstmtSelect,  
SQLHSTMT     hstmtUpdate;  
SQLRETURN    retcode;  
SQLHDBC      hdbc;  
SQLCHAR      szName[NAME_LEN], szPhone[PHONE_LEN];  
SQLINTEGER   cbName, cbPhone;  
  
/* Allocate the statements and set the cursor name. */  
  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmtSelect);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmtUpdate);  
SQLSetCursorName(hstmtSelect, "C1", SQL_NTS);  
  
/* SELECT the result set and bind its columns to local buffers. */  
  
SQLExecDirect(hstmtSelect,  
      "SELECT NAME, PHONE FROM CUSTOMERS",  
      SQL_NTS);  
SQLBindCol(hstmtSelect, 1, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
SQLBindCol(hstmtSelect, 2, SQL_C_CHAR, szPhone, PHONE_LEN, &cbPhone);  
  
/* Read through the result set until the cursor is */  
/* positioned on the row for John Smith. */  
  
do  
 retcode = SQLFetch(hstmtSelect);  
while ((retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) &&  
   (strcmp(szName, "Smith, John") != 0));  
  
/* Perform a positioned update of John Smith's name. */  
  
if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
   SQLExecDirect(hstmtUpdate,  
   "UPDATE EMPLOYEE SET PHONE=\"2064890154\" WHERE CURRENT OF C1",  
   SQL_NTS);  
}  
```  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行已准备的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|返回游标名称|[SQLGetCursorName 函数](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|设置光标滚动选项|[SQLSetScrollOptions 函数](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
