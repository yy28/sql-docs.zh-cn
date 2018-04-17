---
title: SQLStatistics 函数 |Microsoft 文档
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
ms.topic: article
apiname:
- SQLStatistics
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLStatistics
helpviewer_keywords:
- SQLStatistics function [ODBC]
ms.assetid: 45210682-cfea-4e5d-9951-bcf1cbe10f41
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d18b910da6bf23aa507c3fecc7994a59cf74e705
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sqlstatistics-function"></a>SQLStatistics 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLStatistics**检索有关单个表和索引与表相关联的统计信息的列表。 驱动程序返回信息作为结果集。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLStatistics(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CatalogName,  
     SQLSMALLINT     NameLength1,  
     SQLCHAR *       SchemaName,  
     SQLSMALLINT     NameLength2,  
     SQLCHAR *       TableName,  
     SQLSMALLINT     NameLength3,  
     SQLUSMALLINT    Unique,  
     SQLUSMALLINT    Reserved);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *CatalogName*  
 [输入]目录名称。 如果驱动程序支持目录，对于某些表但没有为其他，如当驱动程序检索数据从不同 Dbms，空字符串 ("") 指示没有目录的那些表。 *CatalogName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *CatalogName*视为标识符和其大小写并不重要。 如果它是 SQL_FALSE， *CatalogName*是的普通自变量; 它原义，处理和其大小写很重要。 有关详细信息，请参阅[目录函数中的参数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [输入]以字符为单位的长度 **CatalogName*。  
  
 *schemaName*  
 [输入]架构名称。 如果驱动程序支持的架构，对于某些表但没有为其他，如当驱动程序检索数据从不同 Dbms，空字符串 ("") 指示没有架构的那些表。 *SchemaName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *SchemaName*视为标识符和其大小写并不重要。 如果它是 SQL_FALSE， *SchemaName*是的普通自变量; 它原义，处理和其大小写很重要。  
  
 *NameLength2*  
 [输入]以字符为单位的长度 **SchemaName*。  
  
 *TableName*  
 [输入]表名。 此参数不能为 null 指针。 *SchemaName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *TableName*视为标识符和其大小写并不重要。 如果它是 SQL_FALSE， *TableName*是的普通自变量; 它原义，处理和其大小写很重要。  
  
 *NameLength3*  
 [输入]以字符为单位的长度 **TableName*。  
  
 *唯一*  
 [输入]类型的索引： SQL_INDEX_UNIQUE 或 SQL_INDEX_ALL。  
  
 *保留*  
 [输入]指示基数和页中的列的结果集的重要性。 以下选项会影响返回的基数和页仅限列;如果即使基数和页不会返回，则返回索引信息。  
  
 SQL_ENSURE 请求该驱动程序无条件地检索统计信息。 （仅符合 Open Group 标准和不支持 ODBC 扩展驱动程序将不能支持 SQL_ENSURE。）  
  
 SQL_QUICK 请求，该驱动程序将检索的基数和页面，仅当从服务器可迅速获得。 在这种情况下，驱动程序不能保证是最新值。 (写入到 Open Group 标准的应用程序将始终从 ODBC 3 获得 SQL_QUICK 行为*.x*的兼容驱动程序。)  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLStatistics**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLStatistics**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已连接到数据源之间的通信链接。|  
|24000|无效的游标状态|在打开游标的*StatementHandle*，和**SQLFetch**或**SQLFetchScroll**已调用一样。 此错误返回由驱动程序管理器中，如果**SQLFetch**或**SQLFetchScroll**未返回 SQL_NO_DATA 和在驱动程序返回**SQLFetch**或**SQLFetchScroll**已返回 SQL_NO_DATA。<br /><br /> 在打开游标的*StatementHandle*，但**SQLFetch**或**SQLFetchScroll**不调用一样。|  
|40001|序列化失败|事务已回滚，由于资源死锁与另一个事务。|  
|40003|未知的语句结束|此函数在执行期间失败关联的连接，无法确定事务的状态。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY008|已取消操作|为启用了异步处理*StatementHandle*。 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*，然后调用该函数已在上再次*StatementHandle*。<br /><br /> 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自中的不同线程多线程应用程序。|  
|HY009|不允许使用 null 指针|*TableName*自变量是空指针。<br /><br /> SQL_ATTR_METADATA_ID 语句属性已设置为 SQL_TRUE， *CatalogName*自变量为 null 指针和 SQL_CATALOG_NAME*信息类型*支持中返回该目录名称。<br /><br /> (DM) SQL_ATTR_METADATA_ID 语句属性已设置为 SQL_TRUE，和*SchemaName*自变量是空指针。|  
|HY010|函数序列错误|(DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLStatistics**调用函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*并返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 以异步方式执行的函数 （而不是此的一个） 曾为*StatementHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 之一的名称长度自变量的值小于 0，但不是等于 sql_nts 以。<br /><br /> 名称长度自变量之一的值超出限制的相应名称的最大长度值。|  
|HY100|唯一性选项类型超出了范围|(DM) 无效*Unique*指定的值。|  
|HY101|准确性选项类型超出了范围|(DM) 无效*保留*指定的值。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|指定了目录，并且在驱动程序或数据源不支持目录。<br /><br /> 指定了架构，并且在驱动程序或数据源不支持架构。<br /><br /> 驱动程序或数据源不支持 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 语句属性的当前设置的组合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 语句属性已设置为 SQL_UB_VARIABLE，且 SQL_ATTR_CURSOR_TYPE 语句属性被设置为该驱动程序不支持书签游标类型。|  
|HYT00|超时时间已到|查询超时期限过期之前返回请求的结果集的数据源。 通过设置的超时期限**SQLSetStmtAttr**，SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*StatementHandle*不支持该函数。|  
|IM017|在异步通知模式中禁用轮询|使用通知模型，则每当轮询处于禁用状态。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上的上一个异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用了通知模式， **SQLCompleteAsync**必须在要执行的后处理工作并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 **SQLStatistics**返回有关单个表作为标准的结果集，按 NON_UNIQUE、 类型、 INDEX_QUALIFIER、 INDEX_NAME 和 ORDINAL_POSITION 排序的信息。 结果集将合并统计信息 （基数和页结果集的列） 中为表使用有关每个索引的信息。 有关如何可能使用此信息的信息，请参阅[使用的目录数据](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
 若要确定 TABLE_CAT、 TABLE_SCHEM、 TABLE_NAME 和 COLUMN_NAME 列的实际长度，应用程序可以调用**SQLGetInfo**使用 SQL_MAX_CATALOG_NAME_LEN、 SQL_MAX_SCHEMA_NAME_LEN、 SQL_MAX_TABLE_NAME_LEN，和 SQL_MAX_COLUMN_NAME_LEN 选项。  
  
> [!NOTE]  
>  有关常规使用、 自变量和返回的数据的 ODBC 目录函数的详细信息，请参阅[目录函数](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 下面的列已重命名为 ODBC 3*.x*。 列名称更改不会影响向后兼容性原因是应用程序绑定的列号。  
  
|ODBC 2.0 列|ODBC 3*.x*列|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|SEQ_IN_INDEX|ORDINAL_POSITION|  
|COLLATION|ASC_OR_DESC|  
  
 下表列出在结果集中的列。 可通过该驱动程序定义列 13 (FILTER_CONDITION) 之外的其他列。 应用程序应访问驱动程序的特定列的倒计时从结尾处的结果集而不是指定显式的序号位置。 有关详细信息，请参阅[目录函数返回数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|列名|列号|数据类型|注释|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|适用于的统计信息或索引; 表的目录名称如果不适用于数据源为 NULL。 如果驱动程序支持目录对于某些表，但对于其他操作系统，例如，如果驱动程序从不同 Dbms 检索数据，它将返回空字符串 ("") 不具有目录这些表。|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|适用于的统计信息或索引; 表的架构名称如果不适用于数据源为 NULL。 如果驱动程序支持架构对于某些表，但对于其他操作系统，例如，如果驱动程序从不同 Dbms 检索数据，它将返回空字符串 ("") 不具有架构这些表。|  
|TABLE_NAME (ODBC 1.0)|3|Varchar 不为 NULL|表的统计信息或索引适用的表的名称。|  
|NON_UNIQUE (ODBC 1.0)|4|Smallint|指示是否索引不允许重复的值：<br /><br /> 如果索引值可以是唯一的 SQL_TRUE。<br /><br /> 如果索引值必须是唯一的 SQL_FALSE。<br /><br /> 如果类型是 SQL_TABLE_STAT，则返回 NULL。|  
|INDEX_QUALIFIER (ODBC 1.0)|5|Varchar|用于限定索引的标识符名称这样做**DROP INDEX**;如果数据源不支持索引限定符，或者如果类型为 SQL_TABLE_STAT，则返回 NULL。 如果此列中返回一个非 null 值，它必须用于限定索引名称上**DROP INDEX**语句; 否则，应使用 TABLE_SCHEM 来限定索引名称。|  
|INDEX_NAME (ODBC 1.0)|6|Varchar|索引名称;如果类型是 SQL_TABLE_STAT，则返回 NULL。|  
|类型 (ODBC 1.0)|7|Smallint（非 NULL）|返回的信息的类型：<br /><br /> SQL_TABLE_STAT 指示 （基数或页列中） 中的表的统计信息。<br /><br /> SQL_INDEX_BTREE 指示 B 树索引。<br /><br /> SQL_INDEX_CLUSTERED 指示聚集的索引。<br /><br /> SQL_INDEX_CONTENT 指示内容索引。<br /><br /> SQL_INDEX_HASHED 指示哈希的索引。<br /><br /> SQL_INDEX_OTHER 指示另一种索引。|  
|ORDINAL_POSITION (ODBC 1.0)|8|Smallint|列序列号的索引 （从 1 开始）;如果类型是 SQL_TABLE_STAT，则返回 NULL。|  
|COLUMN_NAME (ODBC 1.0)|9|Varchar|列名称。 如果列基于一个表达式，如薪金 + 优势，返回的表达式;如果无法确定表达式，则返回空字符串。 如果类型是 SQL_TABLE_STAT，则返回 NULL。|  
|ASC_OR_DESC (ODBC 1.0)|10|Char （1)|排序的列的序列:"A"升序;按降序排序;"D"如果数据源不支持列排序顺序，或者如果类型为 SQL_TABLE_STAT，则返回 NULL。|  
|基数 (ODBC 1.0)|11|Integer|表或索引作为参数; 的基数如果类型是 SQL_TABLE_STAT; 在表中的行数如果类型不是 SQL_TABLE_STAT; 的索引中的唯一值数目如果值从数据源不可用，则返回 NULL。|  
|页 (ODBC 1.0)|12|Integer|用于存储的索引或表; 的页面数表类型是否为 SQL_TABLE_STAT; 的页面数如果类型不是 SQL_TABLE_STAT; 的索引的页面数如果值从数据源不可用，或者如果不适用于数据源，则返回 NULL。|  
|FILTER_CONDITION (ODBC 2.0)|13|Varchar|如果索引是一个筛选的索引，这是筛选条件，如薪金 > 30000;如果无法确定筛选条件，这是一个空字符串。<br /><br /> 如果索引不是一个筛选的索引，则为 NULL，它无法确定是否索引已筛选的索引或类型 SQL_TABLE_STAT。|  
  
 如果结果集中的一行对应于一个表，该驱动程序将类型设置为 SQL_TABLE_STAT，并将 NON_UNIQUE、 INDEX_QUALIFIER、 INDEX_NAME、 ORDINAL_POSITION、 COLUMN_NAME 和 ASC_OR_DESC 设置为 NULL。 如果基数或页从数据源不可用，该驱动程序会将它们设置为 NULL。  
  
## <a name="code-example"></a>代码示例  
 有关的类似函数的代码示例，请参阅[SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|绑定到结果集中的列的缓冲区|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|正在提取单个行或只进方向中的数据块。|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取的数据块，或通过结果滚动设置|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|返回外键的列|[SQLForeignKeys 函数](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|  
|返回主键的列|[SQLPrimaryKeys 函数](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
