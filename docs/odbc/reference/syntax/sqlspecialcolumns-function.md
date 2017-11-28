---
title: "SQLSpecialColumns 函数 |Microsoft 文档"
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
apiname: SQLSpecialColumns
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLSpecialColumns
helpviewer_keywords: SQLSpecialColumns function [ODBC]
ms.assetid: bb2d9f21-bda0-4e50-a8be-f710db660034
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4c7f4a796fe40327c1d3691e0178876da010130e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="sqlspecialcolumns-function"></a>SQLSpecialColumns 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： Open Group  
  
 **摘要**  
 **SQLSpecialColumns**检索有关指定表中的列的以下信息：  
  
-   最佳列集中的唯一标识表中的行。  
  
-   由事务更新行中的任何值时将自动更新的列。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLSpecialColumns(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   IdentifierType,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3,  
     SQLSMALLINT   Scope,  
     SQLSMALLINT   Nullable);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *IdentifierType*  
 [输入]若要返回的列类型。 必须是以下值之一：  
  
 SQL_BEST_ROWID： 返回的最佳列，通过检索值的列或列，来唯一地标识指定表中允许任何行集。 列可以伪列或者专为此目的 （如 Oracle ROWID 或 Ingres TID） 或列或表的任何唯一索引的列。  
  
 SQL_ROWVER： 返回的列中指定的表中，如果任何由任何 （如下所示 SQLBase ROWID 或 Sybase 时间戳） 的事务更新行中的任何值时自动更新数据源。  
  
 *CatalogName*  
 [输入]表的目录名称。 如果驱动程序支持目录，对于某些表但没有为其他，如当驱动程序检索数据从不同 Dbms，空字符串 ("") 表示没有目录的那些表。 *CatalogName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *CatalogName*视为标识符和其大小写并不重要。 如果它是 SQL_FALSE， *CatalogName*是的普通自变量; 它原义，处理和其大小写很重要。 有关详细信息，请参阅[目录函数中的参数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [输入]以字符为单位的长度 **CatalogName*。  
  
 *SchemaName*  
 [输入]表的架构名称。 如果驱动程序支持的架构，对于某些表但没有为其他，如当驱动程序检索数据从不同 Dbms，空字符串 ("") 表示没有架构的那些表。 *SchemaName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *SchemaName*视为标识符和其大小写并不重要。 如果它是 SQL_FALSE， *SchemaName*是的普通自变量; 它原义，处理和其大小写很重要。  
  
 *NameLength2*  
 [输入]以字符为单位的长度 **SchemaName*。  
  
 *表名*  
 [输入]表名。 此参数不能为 null 指针。 *TableName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *TableName*视为标识符和其大小写并不重要。 如果它是 SQL_FALSE， *TableName*是的普通自变量; 它原义，处理和其大小写很重要。  
  
 *NameLength3*  
 [输入]以字符为单位的长度 **TableName*。  
  
 *作用域*  
 [输入]Rowid 的最低要求的范围。 返回的 rowid 可能是更大范围。 必须是下列选项之一：  
  
 SQL_SCOPE_CURROW: rowid 保证仅在该行上定位时才有效。 如果行已更新或删除由另一个事务，请使用 rowid 中更高版本重新选择可能不会返回一行。  
  
 SQL_SCOPE_TRANSACTION： 保证 rowid 才能在当前事务的持续时间内有效。  
  
 SQL_SCOPE_SESSION: rowid 被保证是有效的会话的持续时间内 （跨事务边界）。  
  
 *可以为 Null*  
 [输入]确定是否返回特殊可以具有 NULL 值的列。 必须是下列选项之一：  
  
 SQL_NO_NULLS： 排除特殊可以有 NULL 值的列。 某些驱动程序无法支持 SQL_NO_NULLS，并且这些驱动程序将返回一个空结果集如果 SQL_NO_NULLS 已指定。 仅当它是绝对必要，则应为此用例和请求 SQL_NO_NULLS 做好准备应用程序。  
  
 SQL_NULLABLE： 返回特殊列，即使它们可以具有 NULL 值。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLSpecialColumns**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可能会通过调用获取**SQLGetDiagRec**与*HandleType*的SQL_HANDLE_STMT 和*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLSpecialColumns**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已连接到数据源之间的通信链接。|  
|24000|无效的游标状态|在打开游标的*StatementHandle*，和**SQLFetch**或**SQLFetchScroll**已调用一样。 此错误返回由驱动程序管理器中，如果**SQLFetch**或**SQLFetchScroll**未返回 SQL_NO_DATA 和在驱动程序返回**SQLFetch**或**SQLFetchScroll**已返回 SQL_NO_DATA。<br /><br /> 在打开游标的*StatementHandle*，但**SQLFetch**或**SQLFetchScroll**不调用一样。|  
|40001|序列化失败|事务已回滚，因为资源死锁与另一个事务。|  
|40003|未知的语句结束|此函数在执行期间失败关联的连接，无法确定事务的状态。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY008|已取消操作|为启用了异步处理*StatementHandle*。 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*。 然后在再次调用该函数*StatementHandle*。<br /><br /> 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自中的不同线程多线程应用程序。|  
|HY009|不允许使用 null 指针|*TableName*自变量是空指针。<br /><br /> SQL_ATTR_METADATA_ID 语句属性已设置为 SQL_TRUE， *CatalogName*自变量为 null 指针和 SQL_CATALOG_NAME*信息类型*支持中返回该目录名称。<br /><br /> (DM) SQL_ATTR_METADATA_ID 语句属性已设置为 SQL_TRUE，和*SchemaName*自变量是空指针。|  
|HY010|函数序列错误|(DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此函数仍在执行时**SQLSpecialColumns**调用。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*并返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 以异步方式执行的函数 （而不是此的一个） 曾为*StatementHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 之一的长度参数的值小于 0，但不是等于 sql_nts 以。<br /><br /> 长度参数之一的值超出限制的相应名称的最大长度值。 可以通过调用获取每个名称的最大长度**SQLGetInfo**与*信息类型*值： SQL_MAX_CATALOG_NAME_LEN、 SQL_MAX_SCHEMA_NAME_LEN 或 SQL_MAX_TABLE_NAME_LEN。|  
|HY097|列类型超出了范围|(DM) 无效*IdentifierType*指定的值。|  
|HY098|作用域类型超出了范围|(DM) 无效*作用域*指定的值。|  
|HY099|可以为 null 的类型超出了范围|(DM) 无效*可以为 Null*指定的值。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|指定了目录，并且在驱动程序或数据源不支持目录。<br /><br /> 指定了架构，并且在驱动程序或数据源不支持架构。<br /><br /> 驱动程序或数据源不支持 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 语句属性的当前设置的组合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 语句属性已设置为 SQL_UB_VARIABLE，且 SQL_ATTR_CURSOR_TYPE 语句属性被设置为该驱动程序不支持书签游标类型。|  
|HYT00|超时时间已到|查询超时期限过期之前返回请求的结果集的数据源。 通过设置的超时期限**SQLSetStmtAttr**，SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*StatementHandle*不支持该函数。|  
|IM017|在异步通知模式中禁用轮询|使用通知模型，则每当轮询处于禁用状态。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上的上一个异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用了通知模式， **SQLCompleteAsync**必须在要执行的后处理工作并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 当*IdentifierType*自变量是 SQL_BEST_ROWID， **SQLSpecialColumns**返回的列或唯一标识表中的每一行的列。 这些列始终在中使用*选择列表*或**其中**子句。 **SQLColumns**、 用于对表的列返回的各种信息不一定返回的列的唯一标识每一行，或通过更新行中的任何值时将自动更新的列事务。 例如， **SQLColumns**可能不返回 Oracle 伪列 ROWID。 正因如此**SQLSpecialColumns**用于返回这些列。 有关详细信息，请参阅[使用的目录数据](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
> [!NOTE]  
>  有关常规使用、 自变量和返回的数据的 ODBC 目录函数的详细信息，请参阅[目录函数](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 如果没有唯一标识在表中，每一行的列**SQLSpecialColumns**返回一个不用于任何行的行集; 的后续调用**SQLFetch**或**SQLFetchScroll**在帐单上返回 SQL_NO_DATA。  
  
 如果*IdentifierType*，*作用域*，或*可以为 Null*自变量指定的数据源，不支持特征**SQLSpecialColumns**返回空结果集。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *CatalogName*， *SchemaName*，和*TableName*自变量视为用作标识符，因此它们不能设置为在某些情况下是 null 指针。 (有关详细信息，请参阅[目录函数中的参数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。)  
  
 **SQLSpecialColumns**标准的结果集，排序的作用域的形式返回结果。  
  
 下面的列已重命名为 ODBC 3*.x*。 列名称更改不会影响向后兼容性原因是应用程序绑定的列号。  
  
|ODBC 2.0 列|ODBC 3*.x*列|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
  
 若要确定 COLUMN_NAME 列的实际长度，应用程序可以调用**SQLGetInfo** SQL_MAX_COLUMN_NAME_LEN 选项。  
  
 下表列出在结果集中的列。 可通过该驱动程序定义列 8 (PSEUDO_COLUMN) 之外的其他列。 应用程序应访问驱动程序的特定列按倒计时从结果集的末尾，而不是指定显式的序号位置。 有关详细信息，请参阅[目录函数返回数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|列名|列号|数据类型|注释|  
|-----------------|-------------------|---------------|--------------|  
|作用域 (ODBC 1.0)|1|Smallint|Rowid 实际范围。 包含以下值之一：<br /><br /> SQL_SCOPE_CURROW SQL_SCOPE_TRANSACTION SQL_SCOPE_SESSION<br /><br /> 则返回 NULL *IdentifierType*是 SQL_ROWVER。 有关每个值的说明，请参阅说明*作用域*"语法中，"此部分中前面。|  
|COLUMN_NAME (ODBC 1.0)|2|Varchar 不为 NULL|列名称。 该驱动程序返回的列没有名称为空字符串。|  
|DATA_TYPE (ODBC 1.0)|3|Smallint（非 NULL）|SQL 数据类型。 这可以是 ODBC SQL 数据类型或特定于驱动程序的 SQL 数据类型。 有关有效的 ODBC SQL 数据类型的列表，请参阅[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)。 有关特定于驱动程序的 SQL 数据类型的信息，请参阅驱动程序的文档。|  
|TYPE_NAME (ODBC 1.0)|4|Varchar 不为 NULL|数据源 – 依赖于数据类型名称;例如，"CHAR"、"VARCHAR"、"货币"、"长 VARBINARY"或者"CHAR （） FOR BIT DATA"。|  
|COLUMN_SIZE (ODBC 1.0)|5|Integer|对数据源列的大小。 有关列大小的详细信息，请参阅[列大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|BUFFER_LENGTH (ODBC 1.0)|6|Integer|传输上的数据的长度以字节为单位**SQLGetData**或**SQLFetch**如果 SQL_C_DEFAULT 指定的操作。 对于数值数据，此大小可能不同于数据源上存储的数据的大小。 此值是字符或二进制数据的 COLUMN_SIZE 列相同。 有关详细信息，请参阅[列大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|DECIMAL_DIGITS (ODBC 1.0)|7|Smallint|对数据源列的小数位数。 不适用十进制数字数据类型返回 NULL。 有关十进制数字的详细信息，请参阅[列大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|PSEUDO_COLUMN (ODBC 2.0)|8|Smallint|指示列是否为伪列中的，例如 Oracle ROWID:<br /><br /> SQL_PC_UNKNOWN SQL_PC_NOT_PSEUDO SQL_PC_PSEUDO**注意：**的最大互操作性，伪列应未用引号引起来与标识符引号字符由**SQLGetInfo**。|  
  
 应用程序检索 SQL_BEST_ROWID 值后，应用程序可以使用这些值来重新选择该行中定义的作用域。 **选择**保证语句返回一行或任何行。  
  
 如果应用程序 reselects 基于 rowid 列或列的行，并且找不到行，该行已删除或修改 rowid 列可以假定应用程序。 反过来也不成立： 即使 rowid 未更改，可能已更改的行中的其他列。  
  
 返回为 SQL_BEST_ROWID 可用于应用程序需要进行向前滚动，并返回可在结果集中检索最新的数据从一组行的列类型的列。 列或列 rowid 保证不能更改时位于该行上。  
  
 列或列 rowid 可能保持有效即使光标未定位在行;应用程序可以通过检查结果集中的范围列来确定。  
  
 返回为 SQL_ROWVER 可用于应用程序需要能够检查时所在的行已重新使用 rowid 是否已更新给定行中的任何列的列类型的列。 例如，重新选择行使用 rowid 后, 应用程序可以比较 SQL_ROWVER 列于只提取中以前的值。 如果 SQL_ROWVER 列中的值不同于以前的值，应用程序可以发出警报上显示的数据已更改的用户。  
  
## <a name="code-example"></a>代码示例  
 有关的类似函数的代码示例，请参阅[SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|绑定到结果集中的列的缓冲区|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|返回一个表或表中的列|[SQLColumns 函数](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|提取单个行或只进方向中的数据块|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取的数据块，或通过结果滚动设置|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|返回主键的列|[SQLPrimaryKeys 函数](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
