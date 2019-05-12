---
title: SQLRowCount 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRowCount
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRowCount
helpviewer_keywords:
- SQLRowCount function [ODBC]
ms.assetid: 61e00a8a-9b3b-45b9-b397-7fe818822416
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6ccc858603fc5662f380c5d3ae48d777005ddac4
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537154"
---
# <a name="sqlrowcount-function"></a>SQLRowCount Function（SQLRowCount 函数）
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：ISO 92  
  
 **摘要**  
 **SQLRowCount**返回受影响的行数**更新**，**插入**，或**删除**语句; SQL_ADD SQL_UPDATE_BY_BOOKMARK 或 SQL_中的 DELETE_BY_BOOKMARK 操作**SQLBulkOperations**; 或在 SQL_UPDATE 或 SQL_DELETE 操作**SQLSetPos**。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLRowCount(  
      SQLHSTMT   StatementHandle,  
      SQLLEN *   RowCountPtr);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *RowCountPtr*  
 [输出]指向用于返回行计数的缓冲区。 有关**更新**，**插入**，并**删除**语句中的 SQL_ADD、 SQL_UPDATE_BY_BOOKMARK 和 SQL_DELETE_BY_BOOKMARK 操作的**SQLBulkOperations**，以及在 SQL_UPDATE 或 SQL_DELETE 操作**SQLSetPos**中, 返回的值 **RowCountPtr*是受影响的行数请求或-1，如果受影响的行数不可用。  
  
 当**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**， **SQLSetPos 或 SQLMoreResults**调用 SQL_DIAG_ROW_COUNT诊断数据结构的字段设置为行计数和行计数进行缓存以依赖于实现的方式。 **SQLRowCount**返回缓存的行计数值。 缓存的行计数值是否有效，直到语句句柄重新设置为已准备好或已分配状态，并重新执行该语句，或**SQLCloseCursor**调用。 请注意，是否由于 SQL_DIAG_ROW_COUNT 字段已设置，已被调用的函数，返回的值**SQLRowCount**因为 SQL_DIAG_ROW_COUNT 字段重置为可能不同于 SQL_DIAG_ROW_COUNT 字段中的值由任何函数调用为 0。  
  
 对于其他语句和函数，该驱动程序可能会定义中返回的值\* *RowCountPtr*。 例如，某些数据源可能无法返回所返回的行数**选择**语句或之前提取行的目录函数。  
  
> [!NOTE]  
>  多个数据源不能返回结果集中提取它们; 之前的行数最大互操作性，应用程序不应依赖此行为。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLRowCount**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用来获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和一个*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLRowCount** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY010|函数序列错误|(DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLRowCount**调用函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*和返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 在调用之前已调用函数**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos** 为*StatementHandle*。<br /><br /> (DM) 的调用以异步方式执行的函数*StatementHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*StatementHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 如果不是语句句柄上执行的最后一个 SQL 语句**更新**，**插入**，或**删除**语句或 if*操作*在上一个调用的参数**SQLBulkOperations** SQL_ADD、 SQL_UPDATE_BY_BOOKMARK 或 SQL_DELETE_BY_BOOKMARK，不是或者如果*操作*以前调用中的参数**SQLSetPos** SQL_UPDATE 或 SQL_DELETE 的值不是 **RowCountPtr*是驱动程序定义。 有关详细信息，请参阅[确定受影响的行数](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行已准备的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
