---
title: SQLRowCount 函数 |微软文档
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRowCount
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLRowCount
helpviewer_keywords:
- SQLRowCount function [ODBC]
ms.assetid: 61e00a8a-9b3b-45b9-b397-7fe818822416
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2cbca03e7c3e381b803196a1bf7bb227ebeea03b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293367"
---
# <a name="sqlrowcount-function"></a>SQLRowCount Function（SQLRowCount 函数）
**一致性**  
 推出版本： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLRowCount**返回受**更新**、**插入**或**删除**语句影响的行数;**SQLBulk 操作**中的SQL_ADD、SQL_UPDATE_BY_BOOKMARK或SQL_DELETE_BY_BOOKMARK操作;或**SQLSetPos**中的SQL_UPDATE或SQL_DELETE操作。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLRowCount(  
      SQLHSTMT   StatementHandle,  
      SQLLEN *   RowCountPtr);  
```  
  
## <a name="arguments"></a>参数  
 *语句句柄*  
 [输入]语句句柄。  
  
 *罗CountPtr*  
 [输出]指向要返回行计数的缓冲区。 对于**SQLBulk 操作**中的SQL_ADD、SQL_UPDATE_BY_BOOKMARK和SQL_DELETE_BY_BOOKMARK操作的**UPDATE、INSERT**和**DELETE**语句，以及**SQLSetPos**中SQL_UPDATE或SQL_DELETE操作，在 "*RowCountPtr"* 中返回的值是受请求影响的行数，如果受影响的行数不可用，则为 -1。 **INSERT**  
  
 当调用**SQLExecute、SQLExecDirect、SQLBulk****操作****、SQLSetPos 或 SQLMore结果**时，诊断数据结构的SQL_DIAG_ROW_COUNT字段设置为行计数，行计数以与实现相关的方式缓存。 **SQLExecute** **SQLRowCount**返回缓存的行计数值。 缓存的行计数值有效，直到语句句柄设置回准备或分配状态，重新执行语句或调用**SQLCloseCursor。** 请注意，如果自设置SQL_DIAG_ROW_COUNT字段以来已调用函数，**则 SQLRowCount**返回的值可能与SQL_DIAG_ROW_COUNT字段中的值不同，因为 SQL_DIAG_ROW_COUNT字段被任何函数调用重置为 0。  
  
 对于其他语句和函数，驱动程序可以定义在\**RowCountPtr*中返回的值。 例如，某些数据源在获取行之前，可能能够返回**SELECT**语句或目录函数返回的行数。  
  
> [!NOTE]  
>  许多数据源无法在获取结果集中的行数之前返回它们;为了达到最大的互操作性，应用程序不应依赖此行为。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLRowCount**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_STMT的*句柄类型*和*语句句柄*的*句柄*。 下表列出了**SQLRowCount**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY010|函数序列错误|（DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用**SQLRowCount**函数时，此异步函数仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用语句*句柄*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。<br /><br /> （DM） 在调用**SQLExecute、SQLExecDirect、SQLBulk****操作**或**SQLSetPos**之前调用了*语句句柄*。 **SQLExecute**<br /><br /> （DM） 为*语句句柄*调用了异步执行函数，并且在调用此函数时仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*关联的驱动程序不支持该函数。|  
  
## <a name="comments"></a>注释  
 如果在语句句柄上执行的最后一个 SQL 语句不是**更新**、**插入**或**DELETE**语句，或者对**SQLBulk操作**的上一个调用中的*操作*参数不是SQL_ADD、SQL_UPDATE_BY_BOOKMARK或SQL_DELETE_BY_BOOKMARK，或者如果上一个调用**SQLSetPos**中的*操作*参数未SQL_UPDATE或SQL_DELETE，则 =*RowCountPtr*的值是驱动程序定义的。 有关详细信息，请参阅[确定受影响的行数](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行准备好的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
