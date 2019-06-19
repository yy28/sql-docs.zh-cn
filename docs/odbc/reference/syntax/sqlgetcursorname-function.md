---
title: SQLGetCursorName 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 33e2d1f4630228d4c59487c2a5f9de891e87ece5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537381"
---
# <a name="sqlgetcursorname-function"></a>SQLGetCursorName 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：ISO 92  
  
 **摘要**  
 **SQLGetCursorName**返回与指定语句相关联的游标名称。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLGetCursorName(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CursorName,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   NameLengthPtr);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *CursorName*  
 [输出]指向在其中返回的游标名称的缓冲区的指针。  
  
 如果*CursorName*为 NULL， *NameLengthPtr*仍将返回的字符 （不包括字符数据的 null 终止字符） 总数可用于返回通过指向的缓冲区中*CursorName*。  
  
 *BufferLength*  
 [输入]长度\* *CursorName*，以字符为单位。 如果中的值 *\*CursorName*是 Unicode 字符串 (在调用时**SQLGetCursorNameW**)，则*BufferLength*参数必须为偶数。  
  
 *NameLengthPtr*  
 [输出]指向用于返回的字符 （不包括 null 终止字符） 总数的内存可用于在中返回\* *CursorName*。 可用于返回的字符数是否大于或等于*BufferLength*中的游标名称\* *CursorName*截断为*BufferLength*减去 null 终止字符的长度。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetCursorName**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可以通过调用获取关联的 SQLSTATE 值**SQLGetDiagRec**与*HandleType*设置为 SQL_HANDLE_STMT，和一个*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLGetCursorName** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|缓冲区\* *CursorName*是否不足够大以返回整个游标名称，因此游标名称已被截断。 在返回未截断的游标名称的长度 **NameLengthPtr*。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY010|函数序列错误|(DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLGetCursorName**调用函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*和返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 的调用以异步方式执行的函数*StatementHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY015|没有可用的游标名称|(DM) 驱动程序是 ODBC 2 *.x*驱动程序时没有打开的游标语句上和没有游标名称设置与**SQLSetCursorName**。|  
|HY090|字符串或缓冲区长度无效|(DM) 的参数中指定的值*BufferLength*小于 0。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*StatementHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 游标名称仅用于相关的定位更新和删除语句 (例如，**更新**_表名_...**WHERE CURRENT OF** _游标名称_)。 有关详细信息，请参阅[定位更新和删除语句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)。 如果应用程序不会调用**SQLSetCursorName**来定义游标名称，该驱动程序生成的名称。 此名称以字母 SQL_CUR 开头。  
  
> [!NOTE]
>  在 ODBC 2 *.x*，没有任何打开的游标和通过调用设置没有名称时**SQLSetCursorName**，调用**SQLGetCursorName**返回 SQLSTATE HY015 （没有游标名称可用）。 在 ODBC 3 *.x*，这不再为 true; 无论何时**SQLGetCursorName**是调用，该驱动程序返回的游标名称。  
  
 **SQLGetCursorName**返回该值指示是否显式或隐式创建的名称的游标的名称。 如果，则会隐式生成的游标名称**SQLSetCursorName**不调用。 **SQLSetCursorName**可以调用以进行重命名一个语句中的游标，只要将光标处于已分配或已准备状态。  
  
 显式或隐式设置游标名称保留设置直到*StatementHandle*与它关联删除后，使用**SQLFreeHandle**与*HandleType*设置为 SQL_HANDLE_STMT。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行已准备的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|准备执行的语句|[SQLPrepare 函数](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|设置游标名称|[SQLSetCursorName 函数](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
