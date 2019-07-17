---
title: SQLSetCursorName 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 842d21bc36b9360826b4b85aa7da2798782995c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68092992"
---
# <a name="sqlsetcursorname-function"></a>SQLSetCursorName 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：ISO 92  
  
 **摘要**  
 **SQLSetCursorName**游标名称相关联的活动语句。 如果应用程序不会调用**SQLSetCursorName**，驱动程序将所需的 SQL 语句处理生成游标名称。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLSetCursorName(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CursorName,  
     SQLSMALLINT   NameLength);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *CursorName*  
 [输入]游标名称。 针对高效处理游标名称不应在游标名称中包含任何前导或尾随空格，因此如果游标名称中包含分隔的标识符，分隔符应为游标名称中的第一个字符。  
  
 *NameLength*  
 [输入]以字符为单位的长度 **CursorName*。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLSetCursorName**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用来获取**SQLGetDiagRec**与*HandleType*的SQL_HANDLE_STMT 和一个*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLSetCursorName** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|Error|描述|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|游标名称超出了最大限制，因此使用仅最大允许的字符数。|  
|24000|游标状态无效|语句对应于*StatementHandle*本来就处于不执行或光标定位的状态。|  
|34000|无效的游标名称|中指定的游标名称 **CursorName*无效，因为它超出了最大长度由驱动程序，定义，或者开始"SQLCUR"或"SQL_CUR。"|  
|3C000|游标名称重复|中指定的游标名称 **CursorName*已存在。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY009|使用空指针无效|(DM) 参数*CursorName*是空指针。|  
|HY010|函数序列错误|(DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此 aynchronous 函数仍在执行时**SQLSetCursorName**调用函数。<br /><br /> (DM) 的调用以异步方式执行的函数*StatementHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 参数*NameLength*小于 0，但不是等于 SQL_NTS。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*StatementHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 游标名称仅用于相关的定位更新和删除语句 (例如，**更新**_表名_...**WHERE CURRENT OF** _游标名称_)。 有关详细信息，请参阅[定位更新和删除语句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)。 如果应用程序不会调用**SQLSetCursorName**来定义游标名称，在执行的查询语句，该驱动程序生成的名称以字母 SQL_CUR 开头且不超过 18 个字符的长度。  
  
 在连接中的所有游标名称必须都是唯一的。 游标名称的最大长度是由驱动程序定义的。 最大互操作性，建议应用程序限制为不超过 18 个字符的游标名称。 在 ODBC 3 *.x*，如果游标名称是带引号的标识符、 区分大小写的方式处理和它可以包含字符的 SQL 语法不允许或将专门，处理如空格或保留关键字。 如果游标名称必须以区分大小写的方式处理，它必须作为带引号的标识符传递。  
  
 设置游标名称也设置显式或隐式保持，直到使用删除与之关联的语句**SQLFreeHandle**。 **SQLSetCursorName**可以调用以进行重命名一个语句中的游标，只要将光标处于已分配或已准备状态。  
  
## <a name="code-example"></a>代码示例  
 在以下示例中，应用程序使用**SQLSetCursorName**设置语句的游标名称。 它然后使用该语句以从客户表中检索结果。 最后，它执行定位的更新来更改为 John Smith 的电话号码。 请注意，该应用程序使用的不同语句句柄**选择**并**更新**语句。  
  
 另一个代码示例，请参阅[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
```cpp  
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
|设置游标滚动选项|[SQLSetScrollOptions 函数](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
