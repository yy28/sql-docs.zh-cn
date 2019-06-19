---
title: SQLPrimaryKeys 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLPrimaryKeys
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPrimaryKeys
helpviewer_keywords:
- SQLPrimaryKeys function [ODBC]
ms.assetid: 3f809b09-3c1b-415e-80c5-a603e8e25d5b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d213b0bfb108eec38fc524eece6626fd302d4267
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65536645"
---
# <a name="sqlprimarykeys-function"></a>SQLPrimaryKeys 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：ODBC  
  
 **摘要**  
 **SQLPrimaryKeys**返回表的键构成了主数据库的列名称。 驱动程序返回的信息作为结果集。 此函数不支持从单个调用中的多个表返回主键。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLPrimaryKeys(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      TableName,  
     SQLSMALLINT    NameLength3);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *CatalogName*  
 [输入]目录名称。 如果驱动程序支持目录有关的某些表而不是其他人，例如当驱动程序检索数据从不同 Dbms，空字符串 ("") 表示没有目录的那些表。 *CatalogName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *CatalogName*视为标识符和其大小写并不重要。 SQL_FALSE，若是*CatalogName*是普通参数; 按字面意思，处理和其大小写很重要。 有关详细信息，请参阅[中目录函数的自变量](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [输入]以字符为单位的长度 **CatalogName*。  
  
 *SchemaName*  
 [输入]架构名称。 如果驱动程序支持架构有关的某些表而不是其他人，例如当驱动程序检索数据从不同 Dbms，空字符串 ("") 表示没有架构的那些表。 *SchemaName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *SchemaName*视为标识符和其大小写并不重要。 SQL_FALSE，若是*SchemaName*是普通参数; 它按字面意思视为和其大小写并不重要。  
  
 *NameLength2*  
 [输入]以字符为单位的长度 **SchemaName*。  
  
 *TableName*  
 [输入]表名称。 此参数不能为 null 指针。 *TableName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *TableName*视为标识符和其大小写并不重要。 SQL_FALSE，若是*TableName*是普通参数; 它按字面意思视为和其大小写并不重要。  
  
 *NameLength3*  
 [输入]以字符为单位的长度 **TableName*。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLPrimaryKeys**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用来获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和一个*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLPrimaryKeys** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|24000|游标状态无效|(DM) 上打开了游标*StatementHandle*，并**SQLFetch**或**SQLFetchScroll**已调用一样。<br /><br /> 在打开游标的*StatementHandle*，但**SQLFetch**或**SQLFetchScroll**尚未调用。|  
|40001|序列化失败|事务已回滚，由于其他事务与资源死锁。|  
|40003|语句完成情况未知|此函数中，在执行期间失败关联的连接，无法确定事务的状态。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY008|操作已取消|异步处理的已启用*StatementHandle*。 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*。 然后在再次调用该函数*StatementHandle*。<br /><br /> 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自不同线程中多线程应用程序。|  
|HY009|使用空指针无效|（数据挖掘） *TableName*参数是空指针。<br /><br /> SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *CatalogName*参数为 null 指针，并**SQLGetInfo** SQL_CATALOG_NAME 信息类型返回该目录支持名称。<br /><br /> (DM) SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE，并*SchemaName*参数是空指针。|  
|HY010|函数序列错误|(DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLPrimaryKeys**调用函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*和返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 的调用以异步方式执行的函数 （不是此类似） *StatementHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 之一的名称长度参数值小于 0，但不是等于 SQL_NTS，且关联的名称自变量不是 null 指针。<br /><br /> 名称长度参数之一的值超出相应名称的最大长度值。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|指定一个目录，并在驱动程序或数据源不支持目录。<br /><br /> 指定架构和驱动程序或数据源不支持架构。<br /><br /> 驱动程序或数据源不支持 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 语句属性的当前设置的组合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_VARIABLE，并且 SQL_ATTR_CURSOR_TYPE 语句属性设置为游标类型，该驱动程序不支持书签。|  
|HYT00|超时时间已到|超时期限过期之前请求的结果集返回的数据源。 通过设置超时期限**SQLSetStmtAttr**，SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*StatementHandle*不支持该函数。|  
|IM017|轮询异步通知模式中禁用|只要使用通知模型，将禁用轮询。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上以前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用通知模式，则**SQLCompleteAsync**必须要对其进行后期处理并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 **SQLPrimaryKeys**以按 TABLE_CAT、 按 TABLE_SCHEM、 TABLE_NAME 和 KEY_SEQ 排序标准结果集的形式返回结果。 有关可以如何使用此信息的信息，请参阅[使用的目录数据](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
 对于 ODBC 3 重命名为以下各列。*x*。 列名称更改不会影响后向兼容性，因为应用程序将绑定的列号。  
  
|ODBC 2.0 列|ODBC 3。*x*列|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 若要确定 TABLE_CAT、 按 TABLE_SCHEM、 TABLE_NAME 和 COLUMN_NAME 列的实际长度，请调用**SQLGetInfo**与 SQL_MAX_CATALOG_NAME_LEN、 SQL_MAX_SCHEMA_NAME_LEN、 SQL_MAX_TABLE_NAME_LEN 和 SQL_MAX_COLUMN_NAME_LEN 选项。  
  
> [!NOTE]  
>  有关常规使用、 参数以及 ODBC 目录函数返回的数据的详细信息，请参阅[目录函数](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 下表列出了在结果集中的列。 列 6 (PK_NAME) 之外的其他列可以定义由驱动程序。 应用程序应获得访问驱动程序特定列的结果集末尾的倒计时，而不是指定显式的序号位置。 有关详细信息，请参阅[目录函数返回数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|列名|列号|数据类型|注释|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|主键表目录名称;如果不适用于数据源为 NULL。 如果驱动程序支持目录有关的某些表而不是其他人，如当驱动程序检索数据时从不同 Dbms，它返回空字符串 ("") 不具有目录这些表。|  
|按 TABLE_SCHEM (ODBC 1.0)|2|Varchar|主键表架构名称;如果不适用于数据源为 NULL。 如果驱动程序支持架构有关的某些表而不是其他人，如当驱动程序检索数据时从不同 Dbms，它返回空字符串 ("") 不具有架构的这些表。|  
|TABLE_NAME (ODBC 1.0)|3|Varchar 不为 NULL|主键表名。|  
|COLUMN_NAME (ODBC 1.0)|4|Varchar 不为 NULL|主键列名称。 该驱动程序返回空字符串不具有名称的列。|  
|KEY_SEQ (ODBC 1.0)|5|Smallint（非 NULL）|密钥 （从 1 开始） 中的列序号。|  
|PK_NAME (ODBC 2.0)|6|Varchar|主键名称。 如果不适用于数据源为 NULL。|  
  
## <a name="code-example"></a>代码示例  
 请参阅[SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|提取的数据块或滚动浏览结果集|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|提取单个行或仅向前方向中的数据块|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|返回外键的列|[SQLForeignKeys 函数](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|  
|返回表统计信息和索引|[SQLStatistics 函数](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
