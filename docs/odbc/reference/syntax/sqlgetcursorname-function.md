---
title: SQLGetCursorName 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLGetCursorName
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetCursorName
helpviewer_keywords:
- SQLGetCursorName function [ODBC]
ms.assetid: e6e92199-7bb6-447c-8987-049a4c6ce05d
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f8e2490321aae6b155da3486cb78b1f5740738c6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetcursorname-function"></a>SQLGetCursorName 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLGetCursorName**返回与指定语句相关联的游标名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLGetCursorName(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CursorName,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   NameLengthPtr);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *cursorName*  
 [输出]指向在其返回游标名称的缓冲区的指针。  
  
 如果*CursorName*为 NULL， *NameLengthPtr*仍将返回的字符 （不包括字符数据的 null 终止字符） 总数可用于返回指向的缓冲区中*CursorName*。  
  
 *BufferLength*  
 [输入]长度\* *CursorName*，以字符为单位。 如果中的值 *\*CursorName*为 Unicode 字符串 (在调用时**SQLGetCursorNameW**)，则*BufferLength*参数必须为偶数。  
  
 *NameLengthPtr*  
 [输出]指向要返回的字符 （不包括 null 终止字符） 总数在其中的内存可用于返回在\* *CursorName*。 可用于返回的字符数是否大于或等于*BufferLength*中的游标名称\* *CursorName*截断为*BufferLength*减 null 终止字符的长度。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetCursorName**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可通过调用获取关联的 SQLSTATE 值**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLGetCursorName**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|缓冲区\* *CursorName*不是否足够大以返回整个游标名称，因此该游标名称已被截断。 在中返回未截断的光标名称的长度 **NameLengthPtr*。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY010|函数序列错误|(DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLGetCursorName**调用函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*并返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 以异步方式执行的函数曾为*StatementHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY015|没有可用的游标名称|(DM) 驱动程序是 ODBC 2 *.x*驱动程序，语句上没有任何打开的游标，并且没有游标名称必须已用设置**SQLSetCursorName**。|  
|HY090|字符串或缓冲区长度无效|(DM) 参数中指定的值*BufferLength*小于 0。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*StatementHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 游标名称仅在中使用定位更新和 delete 语句 (例如，**更新***表名*...**WHERE CURRENT OF** *游标名称*)。 有关详细信息，请参阅[定位更新和删除语句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)。 如果应用程序不会调用**SQLSetCursorName**若要定义游标名称，该驱动程序生成的名称。 此名称以字母 SQL_CUR 开头。  
  
> [!NOTE]  
>  在 ODBC 2 *.x*，当存在任何打开的游标，并且已通过调用设置没有名称**SQLSetCursorName**，调用**SQLGetCursorName**返回 SQLSTATE HY015 （没有游标名称可用）。 ODBC 3 中 *.x*，这已经不成问题，则返回 true; 无论何时**SQLGetCursorName**是调用，该驱动程序返回的游标名称。  
  
 **SQLGetCursorName**返回的游标是否显式或隐式创建的名称的名称。 如果游标名称隐式生成**SQLSetCursorName**不调用。 **SQLSetCursorName**可以调用以进行重命名语句中的游标，只要光标位于未分配或已准备状态。  
  
 直到将显式或隐式设置游标名称保留*StatementHandle*与它关联会被删除，使用**SQLFreeHandle**与*HandleType* SQL_HANDLE_STMT。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行已准备的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|准备执行的语句|[SQLPrepare 函数](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|设置游标名称|[SQLSetCursorName 函数](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
