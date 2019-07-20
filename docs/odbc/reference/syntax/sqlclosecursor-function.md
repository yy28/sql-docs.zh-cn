---
title: SQLCloseCursor 函数 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCloseCursor
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLCloseCursor
helpviewer_keywords:
- SQLCloseCursor function [ODBC]
ms.assetid: 05b0a054-e28d-4e16-b5b0-07418486b372
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ef336a4deb734c0e44f9c15ae7f9faf0dcb32d93
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343154"
---
# <a name="sqlclosecursor-function"></a>SQLCloseCursor 函数
**度**  
 引入的版本:ODBC 3.0 标准符合性:ISO 92  
  
 **摘要**  
 **SQLCloseCursor**关闭已在语句上打开的游标, 并放弃挂起的结果。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLCloseCursor(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 送语句句柄。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLCloseCursor**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 时, 可以通过使用*SQLGetDiagRec 的 HandleType*和*SQL_HANDLE_STMT*的*句柄*调用**StatementHandle**来获取关联的 SQLSTATE 值。 下表列出了通常由**SQLCloseCursor**返回的 SQLSTATE 值, 并对该函数的上下文中的每个值进行了说明:"(DM)" 表示法位于驱动程序管理器返回的 SQLSTATEs 的说明之前。 除非另有说明, 否则与每个 SQLSTATE 值相关联的返回代码为 SQL_ERROR。  
  
|SQLSTATE|Error|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驱动程序特定的信息性消息。 (函数返回 SQL_SUCCESS_WITH_INFO。)|  
|24000|无效的游标状态|*StatementHandle*上没有打开的游标。 (这仅由 ODBC 3 返回。*x*驱动程序。)|  
|HY000|一般错误|发生了一个错误, 该错误没有特定的 SQLSTATE, 没有为其定义实现特定的 SQLSTATE。 MessageText 缓冲区中**的 SQLGetDiagRec**返回的错误消息描述了错误及其原因。  *\**|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成此函数所需的内存。|  
|HY010|函数序列错误|(DM) 为与*StatementHandle*关联的连接句柄调用了异步执行的函数, 并且在调用此函数时仍在执行该函数。<br /><br /> (DM) 为*StatementHandle*调用了异步执行的函数, 并且在调用此函数时仍在执行该函数。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSETPOS**调用了*StatementHandle*并返回了 SQL_NEED_DATA。 在为所有执行时数据参数或列发送数据之前, 将调用此函数。|  
|HY013|内存管理错误|未能处理函数调用, 原因可能是由于内存不足而无法访问基础内存对象。|  
|HY117|由于未知的事务状态, 连接被挂起。 仅允许断开连接和只读函数。|(DM) 有关挂起状态的详细信息, 请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时已过期|连接超时期限在数据源响应请求之前过期。 连接超时期限通过**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 设置。|  
|IM001|驱动程序不支持此功能|(DM) 与*StatementHandle*关联的驱动程序不支持该函数。|  
  
## <a name="comments"></a>注释  
 如果没有打开的游标, 则**SQLCloseCursor**将返回 SQLSTATE 24000 (无效的游标状态)。 调用**SQLCloseCursor**等效于通过 SQL_CLOSE 选项调用**SQLFreeStmt** , 但如果语句中没有打开的游标, 则**SQLFreeStmt** with SQL_CLOSE 对应用程序没有影响, **SQLCloseCursor**返回 SQLSTATE 24000 (无效的游标状态)。  
  
> [!NOTE]  
>  如果为 ODBC 3。使用 ODBC 2 的*x*应用程序。*x*驱动程序在未打开任何游标时调用**SQLCloseCursor** , 未返回 SQLSTATE 24000 (无效的游标状态), 因为驱动程序管理器会将**SQLCloseCursor**映射到带有 SQL_CLOSE 的**SQLFreeStmt** 。  
  
 有关详细信息, 请参阅[关闭光标](../../../odbc/reference/develop-app/closing-the-cursor.md)。  
  
## <a name="code-example"></a>代码示例  
 请参阅[SQLBrowseConnect 函数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)和[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|正在取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|释放句柄|[SQLFreeHandle 函数](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|处理多个结果集|[SQLMoreResults 函数](../../../odbc/reference/syntax/sqlmoreresults-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
