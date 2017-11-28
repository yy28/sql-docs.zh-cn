---
title: "SQLRowCount 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLRowCount
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLRowCount
helpviewer_keywords: SQLRowCount function [ODBC]
ms.assetid: 61e00a8a-9b3b-45b9-b397-7fe818822416
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c46515b464ea694cfa6184072efb95e2459b1d00
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="sqlrowcount-function"></a>SQLRowCount Function（SQLRowCount 函数）
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLRowCount**返回受影响的行数**更新**，**插入**，或**删除**语句; SQL_ADD SQL_UPDATE_BY_BOOKMARK 或 SQL_中的 DELETE_BY_BOOKMARK 操作**SQLBulkOperations**; 或在 SQL_UPDATE 或 SQL_DELETE 操作**SQLSetPos**。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLRowCount(  
      SQLHSTMT   StatementHandle,  
      SQLLEN *   RowCountPtr);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *RowCountPtr*  
 [输出]指向在其中以返回行计数的缓冲区。 有关**更新**，**插入**，和**删除**语句，为中的 SQL_ADD、 SQL_UPDATE_BY_BOOKMARK 和 SQL_DELETE_BY_BOOKMARK 操作**SQLBulkOperations**，和中 SQL_UPDATE 或 SQL_DELETE 操作**SQLSetPos**中, 返回的值 **RowCountPtr*是受影响的行数请求或为-1 如果受影响的行数不可用。  
  
 当**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**， **SQLSetPos 或 SQLMoreResults**调用时，SQL_DIAG_ROW_COUNT诊断数据结构的字段设置为行计数和行计数进行缓存以依赖于实现的方式。 **SQLRowCount**返回缓存的行计数值。 缓存的行计数值是否有效，直到语句句柄重新设置为已准备或已分配状态，并重新执行该语句，或**SQLCloseCursor**调用。 请注意，是否由于 SQL_DIAG_ROW_COUNT 字段已设置已调用函数，返回的值**SQLRowCount**可能是不同于 SQL_DIAG_ROW_COUNT 字段中的值，因为 SQL_DIAG_ROW_COUNT 字段重置为由任何函数调用为 0。  
  
 对于其他语句和函数，该驱动程序可以定义中返回的值\* *RowCountPtr*。 例如，某些数据源可能能够返回通过返回的行数**选择**语句或目录函数之前提取行。  
  
> [!NOTE]  
>  多个数据源不能在一个结果集，在读取它们; 之前返回行的数最大互操作性，应用程序不应依赖此行为。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLRowCount**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLRowCount**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY010|函数序列错误|(DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLRowCount**调用函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*并返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 在调用之前调用该函数**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**为*StatementHandle*。<br /><br /> (DM) 以异步方式执行的函数曾为*StatementHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*StatementHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 如果语句句柄执行的最后一个 SQL 语句未**更新**，**插入**，或**删除**语句或如果*操作*对以前的调用中参数**SQLBulkOperations**未 SQL_ADD、 SQL_UPDATE_BY_BOOKMARK 或 SQL_DELETE_BY_BOOKMARK，或者如果*操作*对的上一个调用中的自变量**SQLSetPos** SQL_UPDATE 或 SQL_DELETE 的值不是 **RowCountPtr*是驱动程序定义。 有关详细信息，请参阅[确定受影响的行数](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行已准备的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
