---
title: SQLTablePrivileges 函数 |Microsoft 文档
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
- SQLTablePrivileges
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLTablePrivileges
helpviewer_keywords:
- SQLTablePrivileges function [ODBC]
ms.assetid: 8cfdb64f-64c5-47e6-ad57-0533ac630afa
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7df16f3e0a84f96848883ece8e4cb8aa535244a4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqltableprivileges-function"></a>SQLTablePrivileges Function（SQLTablePrivileges 函数）
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： ODBC  
  
 **摘要**  
 **SQLTablePrivileges**返回的表，以及与每个表相关联的权限列表。 该驱动程序返回在指定的语句上作为结果集的信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLTablePrivileges(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *CatalogName*  
 [输入]表目录。 如果驱动程序支持目录，对于某些表但没有为其他，如当驱动程序检索数据从不同 Dbms，空字符串 ("") 表示没有目录的那些表。 *CatalogName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *CatalogName*视为标识符和其大小写并不重要。 如果它是 SQL_FALSE， *CatalogName*是的普通自变量; 它原义，处理和其大小写很重要。 有关详细信息，请参阅[目录函数中的参数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [输入]以字符为单位的长度 **CatalogName*。  
  
 *schemaName*  
 [输入]架构名称的字符串的搜索模式。 如果驱动程序支持的架构，对于某些表但没有为其他，如当驱动程序检索数据从不同 Dbms，空字符串 ("") 表示没有架构的那些表。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *SchemaName*视为标识符和其大小写并不重要。 如果它是 SQL_FALSE， *SchemaName*是一个模式值参数; 它原义，处理和其大小写很重要。  
  
 *NameLength2*  
 [输入]以字符为单位的长度 **SchemaName*。  
  
 *TableName*  
 [输入]表名称的字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *TableName*视为标识符和其大小写并不重要。 如果它是 SQL_FALSE， *TableName*是一个模式值参数; 它原义，处理和其大小写很重要。  
  
 *NameLength3*  
 [输入]以字符为单位的长度 **TableName*。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLTablePrivileges**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可能会通过调用获取**SQLGetDiagRec**与*HandleType*SQL_HANDLE_STMT 和*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLTablePrivileges**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明. 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已连接到数据源之间的通信链接。|  
|24000|无效的游标状态|在打开游标的*StatementHandle*，和**SQLFetch**或**SQLFetchScroll**已调用一样。 此错误返回由驱动程序管理器中，如果**SQLFetch**或**SQLFetchScroll**未返回 SQL_NO_DATA 和在驱动程序返回**SQLFetch**或**SQLFetchScroll**已返回 SQL_NO_DATA。<br /><br /> 在打开游标的*StatementHandle*，但**SQLFetch**或**SQLFetchScroll**不调用一样。|  
|40001|序列化失败|事务已回滚，因为资源死锁与另一个事务。|  
|40003|未知的语句结束|此函数在执行期间失败关联的连接，无法确定事务的状态。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY008|已取消操作|为启用了异步处理*StatementHandle*。 **SQLTablePrivileges**调用函数，并且它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*。 则**SQLTablePrivileges**函数上调用了再次*StatementHandle*。<br /><br /> **SQLTablePrivileges**调用函数，并且它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*从多线程应用程序中的不同线程。|  
|HY009|不允许使用 null 指针|SQL_ATTR_METADATA_ID 语句属性已设置为 SQL_TRUE， *CatalogName*自变量为 null 指针和 SQL_CATALOG_NAME*信息类型*支持中返回该目录名称。<br /><br /> (DM) SQL_ATTR_METADATA_ID 语句属性已设置为 SQL_TRUE，和*SchemaName*或*TableName*自变量是空指针。|  
|HY010|函数序列错误|(DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLTablePrivileges**调用函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*并返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 以异步方式执行的函数 （而不是此的一个） 曾为*StatementHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 之一的名称长度自变量的值小于 0，但不是等于 sql_nts 以。<br /><br /> 名称长度自变量之一的值超出限制的相应的限定符或名称的最大长度值。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|指定了目录，并且在驱动程序或数据源不支持目录。<br /><br /> 指定了架构，并且在驱动程序或数据源不支持架构。<br /><br /> 为表架构、 表名或列名，指定字符串的搜索模式和数据源不支持为一个或多个这些自变量的搜索模式。<br /><br /> 驱动程序或数据源不支持 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 语句属性的当前设置的组合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 语句属性已设置为 SQL_UB_VARIABLE，且 SQL_ATTR_CURSOR_TYPE 语句属性被设置为该驱动程序不支持书签游标类型。|  
|HYT00|超时时间已到|查询超时期限过期之前的数据源返回了结果集。 通过设置的超时期限**SQLSetStmtAttr**，SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*StatementHandle*不支持该函数。|  
|IM017|在异步通知模式中禁用轮询|使用通知模型，则每当轮询处于禁用状态。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上的上一个异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用了通知模式， **SQLCompleteAsync**必须在要执行的后处理工作并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 *SchemaName*和*TableName*参数接受搜索模式。 有关有效的搜索模式的详细信息，请参阅[模式值自变量](../../../odbc/reference/develop-app/pattern-value-arguments.md)。  
  
 **SQLTablePrivileges**标准的结果集，按 TABLE_CAT、 TABLE_SCHEM、 TABLE_NAME、 权限和被授权者排序的形式返回结果。  
  
 若要确定 TABLE_CAT、 TABLE_SCHEM 和 TABLE_NAME 列的实际长度，应用程序可以调用**SQLGetInfo**使用 SQL_MAX_CATALOG_NAME_LEN、 SQL_MAX_SCHEMA_NAME_LEN 和 SQL_MAX_TABLE_NAME_LEN 选项。  
  
> [!NOTE]  
>  有关常规使用、 自变量和返回的数据的 ODBC 目录函数的详细信息，请参阅[目录函数](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 下面的列已重命名为 ODBC 3 *.x*。 列名称更改不会影响向后兼容性原因是应用程序绑定的列号。  
  
|ODBC 2.0 列|ODBC 3 *.x*列|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 下表列出在结果集中的列。 可通过该驱动程序定义列 7 (IS_GRANTABLE) 之外的其他列。 应用程序应访问驱动程序的特定列按倒计时从结果集的末尾，而不是指定显式的序号位置。 有关详细信息，请参阅[目录函数返回数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|列名|列号|数据类型|注释|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|目录名称;如果不适用于数据源为 NULL。 如果驱动程序支持目录对于某些表，但对于其他操作系统，例如，如果驱动程序从不同 Dbms 检索数据，它将返回空字符串 ("") 不具有目录这些表。|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|架构名称;如果不适用于数据源为 NULL。 如果驱动程序支持架构对于某些表，但对于其他操作系统，例如，如果驱动程序从不同 Dbms 检索数据，它将返回空字符串 ("") 不具有架构这些表。|  
|TABLE_NAME (ODBC 1.0)|3|Varchar 不为 NULL|表名。|  
|授权者 (ODBC 1.0)|4|Varchar|授予权限; 用户名称如果不适用于数据源为 NULL。<br /><br /> 对于被授权者列中的值与对象的所有者的所有行，授权者列将"（_s）"。|  
|被授权者 (ODBC 1.0)|5|Varchar 不为 NULL|向其授予特权的用户的名称。|  
|特权 (ODBC 1.0)|6|Varchar 不为 NULL|表的权限。 可能是以下或数据源 – 特定权限之一。<br /><br /> 选择： 被授权者可以检索表的一个或多个列的数据。<br /><br /> 插入： 允许被授权者要插入到表中包含一个或多个列的数据的新行。<br /><br /> 更新： 允许被授权者更新一个或多个列的表中的数据。<br /><br /> 删除： 被授权者有权从表中删除的数据行。<br /><br /> 引用： 被授权者允许引用约束中的表的一个或多个列 (例如，唯一、 引用，或检查约束的表)。<br /><br /> 允许被授权者的给定的表特权的作用域是操作的数据源而定。 例如，更新权限可能允许被授权者更新在一个数据源的表中的所有列和仅授权者另一个数据源具有更新权限这些列。|  
|IS_GRANTABLE (ODBC 1.0)|7|Varchar|该值指示是否允许被授权者授予其他用户; 的权限"是"、"否"，或如果未知或不适用于数据源为 NULL。<br /><br /> 特权是可授予或不但不是同时可授予。 返回的结果集**SQLColumnPrivileges**永远不会将包含为其 IS_GRANTABLE 列除外的所有列都包含相同的值的两行。|  
  
## <a name="code-example"></a>代码示例  
 有关的类似函数的代码示例，请参阅[SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|绑定到结果集中的列的缓冲区|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|返回为一列或列的权限|[SQLColumnPrivileges 函数](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|返回一个表或表中的列|[SQLColumns 函数](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|提取单个行或只进方向中的数据块|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取的数据块，或通过结果滚动设置|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|返回表统计信息和索引|[SQLStatistics 函数](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|数据源中返回表的列表|[SQLTables 函数](../../../odbc/reference/syntax/sqltables-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
