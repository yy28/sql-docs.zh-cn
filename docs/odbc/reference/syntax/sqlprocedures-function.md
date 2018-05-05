---
title: SQLProcedures 函数 |Microsoft 文档
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
- SQLProcedures
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLProcedures
helpviewer_keywords:
- SQLProcedures function [ODBC]
ms.assetid: d0d9ef10-2fd4-44a5-9334-649f186f4ba0
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 486616002b58db8de8de5cd3e54e13c286b2587d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlprocedures-function"></a>SQLProcedures 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： ODBC  
  
 **摘要**  
 **SQLProcedures**返回的特定数据源中存储的过程名称的列表。 *过程*是泛型的术语，用于描述*可执行对象*，或可以使用输入和输出参数调用一个已命名的实体。 过程的详细信息，请参阅[过程](../../../odbc/reference/develop-app/procedures-odbc.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLProcedures(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      ProcName,  
     SQLSMALLINT    NameLength3);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *CatalogName*  
 [输入]过程目录。 如果驱动程序支持目录，对于某些表但没有为其他，如当驱动程序检索数据从不同 Dbms，空字符串 ("") 表示没有目录的那些表。 *CatalogName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *CatalogName*视为标识符和其大小写并不重要。 如果它是 SQL_FALSE， *CatalogName*是的普通自变量; 它原义，处理和其大小写很重要。 有关详细信息，请参阅[目录函数中的参数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [输入]以字符为单位的长度 **CatalogName*。  
  
 *schemaName*  
 [输入]过程的架构名称的字符串的搜索模式。 如果驱动程序支持架构有关的某些过程而不是其他人，如当驱动程序检索数据从不同 Dbms，空字符串 ("") 表示没有架构这些过程。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *SchemaName*视为标识符和其大小写并不重要。 如果它是 SQL_FALSE， *SchemaName*是一个模式值参数; 它原义，处理和其大小写很重要。  
  
 *NameLength2*  
 [输入]以字符为单位的长度 **SchemaName*。  
  
 *ProcName*  
 [输入]过程名称的字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *ProcName*视为标识符和其大小写并不重要。 如果它是 SQL_FALSE， *ProcName*是一个模式值参数; 它原义，处理和其大小写很重要。  
  
 *NameLength3*  
 [输入]以字符为单位的长度 **ProcName*。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLProcedures**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLProcedures**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已连接到数据源之间的通信链接。|  
|24000|无效的游标状态|在打开游标的*StatementHandle*，和**SQLFetch**或**SQLFetchScroll**已调用一样。 此错误返回由驱动程序管理器中，如果**SQLFetch**或**SQLFetchScroll**未返回 SQL_NO_DATA，并且如果由驱动程序返回**SQLFetch**或**SQLFetchScroll**已返回 SQL_NO_DATA。<br /><br /> 在打开游标的*StatementHandle*，但**SQLFetch**或**SQLFetchScroll**不调用一样。|  
|40001|序列化失败|事务已回滚，因为资源死锁与另一个事务。|  
|40003|未知的语句结束|此函数在执行期间失败关联的连接，无法确定事务的状态。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY008|已取消操作|为启用了异步处理*StatementHandle*。 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*。 然后在再次调用该函数*StatementHandle*。<br /><br /> 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自中的不同线程多线程应用程序。|  
|HY009|不允许使用 null 指针|SQL_ATTR_METADATA_ID 语句属性已设置为 SQL_TRUE， *CatalogName*自变量为 null 指针和 SQL_CATALOG_NAME*信息类型*支持中返回该目录名称。<br /><br /> (DM) SQL_ATTR_METADATA_ID 语句属性已设置为 SQL_TRUE，和*SchemaName*或*ProcName*自变量是空指针。|  
|HY010|函数序列错误|(DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍已执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*并返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 以异步方式执行的函数 （而不是此的一个） 曾为*StatementHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 之一的名称长度自变量的值小于 0，但不是等于 sql_nts 以。<br /><br /> 名称长度自变量之一的值超出限制的相应名称的最大长度值。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|指定了过程目录，并且在驱动程序或数据源不支持目录。<br /><br /> 指定了过程架构，并且在驱动程序或数据源不支持架构。<br /><br /> 为过程架构或过程名称指定字符串的搜索模式和数据源不支持为一个或多个这些自变量的搜索模式。<br /><br /> 驱动程序或数据源不支持 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 语句属性的当前设置的组合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 语句属性已设置为 SQL_UB_VARIABLE，且 SQL_ATTR_CURSOR_TYPE 语句属性被设置为该驱动程序不支持书签游标类型。|  
|HYT00|超时时间已到|查询超时期限过期之前返回请求的结果集的数据源。 通过设置的超时期限**SQLSetStmtAttr**，SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*StatementHandle*不支持此函数。|  
|IM017|在异步通知模式中禁用轮询|使用通知模型，则每当轮询处于禁用状态。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上的上一个异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用了通知模式， **SQLCompleteAsync**必须在要执行的后处理工作并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 **SQLProcedures**列出请求的范围中的所有过程。 用户可能或可能没有执行任何这些过程的权限。 若要检查可访问性，应用程序可以调用**SQLGetInfo**和检查 SQL_ACCESSIBLE_PROCEDURES 信息值。 否则，应用程序必须能够处理的情况下，其中用户选择一个系统不能执行的过程。 有关如何可能使用此信息的信息，请参阅[过程](../../../odbc/reference/develop-app/procedures-odbc.md)。  
  
> [!NOTE]  
>  有关常规使用、 自变量和返回的数据的 ODBC 目录函数的详细信息，请参阅[目录函数](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 **SQLProcedures**标准的结果集，按 PROCEDURE_CAT、 PROCEDURE_SCHEMA 和 PROCEDURE_NAME 排序的形式返回结果。  
  
> [!NOTE]  
>  **SQLProcedures**可能不会返回所有过程。 应用程序可以使用任何有效的过程，而不考虑是否将它返回由**SQLProcedures**。  
  
 下面的列已重命名为 ODBC 3 *.x*。 列名称更改不会影响向后兼容性原因是应用程序绑定的列号。  
  
|ODBC 2.0 列|ODBC 3 *.x*列|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|过程 _OWNER|过程 _SCHEM|  
  
 若要确定 PROCEDURE_CAT、 PROCEDURE_SCHEM 和 PROCEDURE_NAME 列的实际长度，应用程序可以调用**SQLGetInfo**使用 SQL_MAX_CATALOG_NAME_LEN、 SQL_MAX_SCHEMA_NAME_LEN 和 SQL_MAX_PROCEDURE_NAME_LEN 选项。  
  
 下表列出在结果集中的列。 可通过该驱动程序定义列 8 (PROCEDURE_TYPE) 之外的其他列。 应用程序应访问驱动程序的特定列按倒计时从结果集的末尾，而不是指定显式的序号位置。 有关详细信息，请参阅[目录函数返回数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|列名|列号|数据类型|注释|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1|Varchar|过程目录标识符;如果不适用于数据源为 NULL。 如果驱动程序支持目录有关的某些过程而不是其他人，例如，如果驱动程序从不同 Dbms 检索数据，它将返回空字符串 ("") 对于这些没有目录的过程。|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|过程架构标识符;如果不适用于数据源为 NULL。 如果驱动程序支持架构对于一些过程，但对于其他操作系统，例如，如果驱动程序从不同 Dbms 检索数据，它将返回空字符串 ("") 对于这些没有架构的过程。|  
|PROCEDURE_NAME (ODBC 2.0)|3|Varchar 不为 NULL|过程标识符。|  
|NUM_INPUT_PARAMS (ODBC 2.0)|4|N/A|保留供将来使用。 应用程序不应依赖于这些结果列中返回的数据。|  
|NUM_OUTPUT_PARAMS (ODBC 2.0)|5|N/A|保留供将来使用。 应用程序不应依赖于这些结果列中返回的数据。|  
|NUM_RESULT_SETS (ODBC 2.0)|6|N/A|保留供将来使用。 应用程序不应依赖于这些结果列中返回的数据。|  
|备注 (ODBC 2.0)|7|Varchar|过程的说明。|  
|PROCEDURE_TYPE (ODBC 2.0)|8|Smallint|定义过程类型：<br /><br /> SQL_PT_UNKNOWN： 无法确定是否该过程返回一个值。<br /><br /> SQL_PT_PROCEDURE： 返回的对象是一个过程;也就是说，它不具有返回值。<br /><br /> SQL_PT_FUNCTION： 返回的对象是一个函数;也就是说，它具有一个返回值。|  
  
 *SchemaName*和*ProcName*参数接受搜索模式。 有关有效的搜索模式的详细信息，请参阅[模式值自变量](../../../odbc/reference/develop-app/pattern-value-arguments.md)。  
  
## <a name="code-example"></a>代码示例  
 请参阅[过程调用](../../../odbc/reference/develop-app/procedure-calls.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|绑定到结果集中的列的缓冲区|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|提取单个行或只进方向中的数据块|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取的数据块，或通过结果滚动设置|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|返回有关的驱动程序或数据源的信息|[SQLGetInfo 函数](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|返回的参数和结果集的过程的列|[SQLProcedureColumns 函数](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|  
|调用存储的过程的语法|[执行语句](../../../odbc/reference/develop-app/executing-statements-odbc.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
