---
title: SQLStatistics 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f4277c6606392c91ffb3de40ace658cd68461f01
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65536255"
---
# <a name="sqlstatistics-function"></a>SQLStatistics 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：ISO 92  
  
 **摘要**  
 **SQLStatistics**检索有关单个表和索引与表关联的统计信息的列表。 驱动程序返回的信息作为结果集。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
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
 [输入]目录名称。 如果驱动程序支持目录有关的某些表而不是其他人，例如当驱动程序检索数据从不同 Dbms，空字符串 ("") 指示没有目录的那些表。 *CatalogName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *CatalogName*视为标识符和其大小写并不重要。 SQL_FALSE，若是*CatalogName*是普通参数; 按字面意思，处理和其大小写很重要。 有关详细信息，请参阅[中目录函数的自变量](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [输入]以字符为单位的长度 **CatalogName*。  
  
 *SchemaName*  
 [输入]架构名称。 如果驱动程序支持架构有关的某些表而不是其他人，例如当驱动程序检索数据从不同 Dbms，空字符串 ("") 指示没有架构的那些表。 *SchemaName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *SchemaName*视为标识符和其大小写并不重要。 SQL_FALSE，若是*SchemaName*是普通参数; 按字面意思，处理和其大小写很重要。  
  
 *NameLength2*  
 [输入]以字符为单位的长度 **SchemaName*。  
  
 *TableName*  
 [输入]表名称。 此参数不能为 null 指针。 *SchemaName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *TableName*视为标识符和其大小写并不重要。 SQL_FALSE，若是*TableName*是普通参数; 按字面意思，处理和其大小写很重要。  
  
 *NameLength3*  
 [输入]以字符为单位的长度 **TableName*。  
  
 *唯一*  
 [输入]索引的类型：SQL_INDEX_UNIQUE 或 SQL_INDEX_ALL。  
  
 Reserved   
 [输入]指示基数和页中的列的结果集的重要性。 以下选项会影响返回的基数和页仅限于列;如果即使基数和页不会返回，则返回索引的信息。  
  
 SQL_ENSURE 请求驱动程序无条件地检索统计信息。 （仅符合 Open Group 标准并不支持 ODBC 扩展驱动程序将不能以支持 SQL_ENSURE。）  
  
 SQL_QUICK 请求驱动程序检索基数和页仅当从服务器可迅速获得。 在这种情况下，驱动程序不能保证是最新值。 (Open Group 标准编写的应用程序将始终从 ODBC 3 获得 SQL_QUICK 行为 *.x*-兼容驱动程序。)  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLStatistics**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用来获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和一个*处理*的*StatementHandle*。 下表列出了通常由返回的 SQLSTATE 值**SQLStatistics** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|24000|游标状态无效|在打开游标的*StatementHandle*，并**SQLFetch**或**SQLFetchScroll**已调用一样。 如果此错误返回由驱动程序管理器**SQLFetch**或**SQLFetchScroll**未返回 SQL_NO_DATA 和时，返回的驱动程序**SQLFetch**或**SQLFetchScroll**已返回 sql_no_data 为止。<br /><br /> 在打开游标的*StatementHandle*，但**SQLFetch**或**SQLFetchScroll**尚未调用。|  
|40001|序列化失败|事务已回滚，由于其他事务与资源死锁。|  
|40003|语句完成情况未知|此函数中，在执行期间失败关联的连接，无法确定事务的状态。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY008|操作已取消|异步处理的已启用*StatementHandle*。 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*，然后调用该函数是在上再次*StatementHandle*。<br /><br /> 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自不同线程中多线程应用程序。|  
|HY009|使用空指针无效|*TableName*参数是空指针。<br /><br /> SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *CatalogName*参数为 null 指针和 SQL_CATALOG_NAME*信息类型*支持目录名称返回。<br /><br /> (DM) SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE，并*SchemaName*参数是空指针。|  
|HY010|函数序列错误|(DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLStatistics**调用函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*和返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 的调用以异步方式执行的函数 （不是此类似） *StatementHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 之一的名称长度参数值小于 0 但不是等于 SQL_NTS。<br /><br /> 名称长度参数之一的值超出相应名称的最大长度值。|  
|HY100|唯一性选项类型超出了范围|(DM) 无效*Unique*指定的值。|  
|HY101|准确性选项类型超出了范围|(DM) 无效*保留*指定的值。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|指定一个目录，并在驱动程序或数据源不支持目录。<br /><br /> 指定了架构，并且在驱动程序或数据源不支持架构。<br /><br /> 驱动程序或数据源不支持 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 语句属性的当前设置的组合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_VARIABLE，并且 SQL_ATTR_CURSOR_TYPE 语句属性设置为游标类型，该驱动程序不支持书签。|  
|HYT00|超时时间已到|查询超时期限过期之前请求的结果集返回的数据源。 通过设置超时期限**SQLSetStmtAttr**，SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*StatementHandle*不支持该函数。|  
|IM017|轮询异步通知模式中禁用|只要使用通知模型，将禁用轮询。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上以前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用通知模式，则**SQLCompleteAsync**必须要对其进行后期处理并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 **SQLStatistics**返回有关单个表作为标准的结果集，按 NON_UNIQUE、 类型、 INDEX_QUALIFIER、 INDEX_NAME 和 ORDINAL_POSITION 排序的信息。 结果集将合并统计信息 （在结果集的基数和页列） 的表与每个索引有关的信息。 有关可以如何使用此信息的信息，请参阅[使用的目录数据](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
 若要确定 TABLE_CAT、 按 TABLE_SCHEM、 TABLE_NAME 和 COLUMN_NAME 列的实际长度，应用程序可以调用**SQLGetInfo**使用 SQL_MAX_CATALOG_NAME_LEN、 SQL_MAX_SCHEMA_NAME_LEN、 SQL_MAX_TABLE_NAME_LEN，和 SQL_MAX_COLUMN_NAME_LEN 选项。  
  
> [!NOTE]  
>  有关常规使用、 参数以及 ODBC 目录函数返回的数据的详细信息，请参阅[目录函数](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 以下各列已重命名为 ODBC 3 *.x*。 列名称更改不会影响后向兼容性，因为应用程序将绑定的列号。  
  
|ODBC 2.0 列|ODBC 3 *.x*列|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|SEQ_IN_INDEX|ORDINAL_POSITION|  
|COLLATION|ASC_OR_DESC|  
  
 下表列出了在结果集中的列。 列 13 (FILTER_CONDITION) 之外的其他列可以定义由驱动程序。 应用程序应获得访问驱动程序特定列的倒计时从结果集而不是指定显式的序号位置的末尾。 有关详细信息，请参阅[目录函数返回数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|列名|列号|数据类型|注释|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|目录名称的表的统计信息或索引应用于;如果不适用于数据源为 NULL。 如果驱动程序支持目录有关的某些表而不是其他人，如当驱动程序检索数据时从不同 Dbms，它返回空字符串 ("") 不具有目录这些表。|  
|按 TABLE_SCHEM (ODBC 1.0)|2|Varchar|应用于的统计信息或索引; 的表的架构名称如果不适用于数据源为 NULL。 如果驱动程序支持架构有关的某些表而不是其他人，如当驱动程序检索数据时从不同 Dbms，它返回空字符串 ("") 不具有架构的这些表。|  
|TABLE_NAME (ODBC 1.0)|3|Varchar 不为 NULL|表的统计信息或索引应用的表的名称。|  
|NON_UNIQUE (ODBC 1.0)|4|Smallint|指示是否索引不允许重复的值：<br /><br /> 如果可以将非唯一索引值，SQL_TRUE。<br /><br /> 如果索引值必须是唯一的 SQL_FALSE。<br /><br /> 如果类型为 SQL_TABLE_STAT，则返回 NULL。|  
|INDEX_QUALIFIER (ODBC 1.0)|5|Varchar|用于限定索引的标识符名称这样做**DROP INDEX**;如果数据源不支持索引限定符或类型是否为 SQL_TABLE_STAT，则返回 NULL。 如果在此列中返回非 null 值，则它必须用于限定索引名称在**DROP INDEX**语句; 否则，应使用以 TABLE_SCHEM 来限定索引名称。|  
|INDEX_NAME (ODBC 1.0)|6|Varchar|索引名称;如果类型为 SQL_TABLE_STAT，则返回 NULL。|  
|类型 (ODBC 1.0)|7|Smallint（非 NULL）|要返回的信息类型：<br /><br /> SQL_TABLE_STAT 指示 （中的基数或页面列中） 的表的统计信息。<br /><br /> SQL_INDEX_BTREE 指示 B 树索引。<br /><br /> SQL_INDEX_CLUSTERED 指示聚集的索引。<br /><br /> SQL_INDEX_CONTENT 指示内容索引。<br /><br /> SQL_INDEX_HASHED 指示哈希的索引。<br /><br /> SQL_INDEX_OTHER 指示索引的另一种类型。|  
|ORDINAL_POSITION (ODBC 1.0)|8|Smallint|列序列号的索引 （从 1 开始）;如果类型为 SQL_TABLE_STAT，则返回 NULL。|  
|COLUMN_NAME (ODBC 1.0)|9|Varchar|列名称。 如果列基于一个表达式，如薪金 + 优势，返回的表达式;如果无法确定该表达式，则返回空字符串。 如果类型为 SQL_TABLE_STAT，则返回 NULL。|  
|ASC_OR_DESC (ODBC 1.0)|10|Char(1)|列的排序顺序："A"升序;"D"表示降序;如果数据源不支持列排序顺序或类型是否为 SQL_TABLE_STAT，则返回 NULL。|  
|基数 (ODBC 1.0)|11|Integer|基数的表或索引;如果类型是 SQL_TABLE_STAT; 在表中的行数如果类型不是 SQL_TABLE_STAT; 在索引中的唯一值的数量如果值从数据源不可用，则返回 NULL。|  
|页 (ODBC 1.0)|12|Integer|用于存储索引或表; 的页面数表类型是否为 SQL_TABLE_STAT; 的页面数如果类型不是 SQL_TABLE_STAT; 索引的页面数如果值从数据源不可用或不可能适用于数据源，则返回 NULL。|  
|FILTER_CONDITION (ODBC 2.0)|13|Varchar|如果索引是筛选的索引，这是筛选条件，如薪金 > 30000;如果不能确定筛选条件，，则为空字符串。<br /><br /> 如果索引不是筛选的索引，则为 NULL，不能确定是否索引为筛选的索引，或类型是 SQL_TABLE_STAT。|  
  
 如果结果集中的一行对应于一个表，该驱动程序类型设置为 SQL_TABLE_STAT 并 NON_UNIQUE、 INDEX_QUALIFIER、 INDEX_NAME、 ORDINAL_POSITION、 COLUMN_NAME 和 ASC_OR_DESC 设置为 NULL。 如果基数或页从数据源不可用，驱动程序会将它们设置为 NULL。  
  
## <a name="code-example"></a>代码示例  
 有关类似函数的代码示例，请参阅[SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|正在提取单个行或仅向前方向中的数据块。|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取的数据块或滚动浏览结果集|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|返回外键的列|[SQLForeignKeys 函数](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|  
|返回主键的列|[SQLPrimaryKeys 函数](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
