---
title: SQLSpecialColumns 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSpecialColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSpecialColumns
helpviewer_keywords:
- SQLSpecialColumns function [ODBC]
ms.assetid: bb2d9f21-bda0-4e50-a8be-f710db660034
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f44ae90a82e778bf8e8564b719aa6b9f0157a05a
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53204366"
---
# <a name="sqlspecialcolumns-function"></a>SQLSpecialColumns 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：打开组  
  
 **摘要**  
 **SQLSpecialColumns**检索有关指定表中的列的以下信息：  
  
-   最佳列集的唯一标识表中的行。  
  
-   当通过事务更新的行中的任何值时，会自动更新的列。  
  
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
 [输入]要返回列的类型。 必须是以下值之一：  
  
 SQL_BEST_ROWID:返回最优列集，通过检索的列或列，允许的任意行中指定的表可以唯一标识。 列可以是专为此目的 （如 Oracle ROWID 或 Ingres TID） 或列或表的任何唯一索引的列是伪列。  
  
 SQL_ROWVER:如果有任何事务 （如 SQLBase ROWID 或 Sybase 时间戳） 更新的行中的任何值时自动更新数据源，返回指定表中的列。  
  
 *CatalogName*  
 [输入]表的目录名称。 如果驱动程序支持目录有关的某些表而不是其他人，例如当驱动程序检索数据从不同 Dbms，空字符串 ("") 表示没有目录的那些表。 *CatalogName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *CatalogName*视为标识符和其大小写并不重要。 SQL_FALSE，若是*CatalogName*是普通参数; 按字面意思，处理和其大小写很重要。 有关详细信息，请参阅[中目录函数的自变量](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [输入]以字符为单位的长度 **CatalogName*。  
  
 *SchemaName*  
 [输入]表的架构名称。 如果驱动程序支持架构有关的某些表而不是其他人，例如当驱动程序检索数据从不同 Dbms，空字符串 ("") 表示没有架构的那些表。 *SchemaName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *SchemaName*视为标识符和其大小写并不重要。 SQL_FALSE，若是*SchemaName*是普通参数; 按字面意思，处理和其大小写很重要。  
  
 *NameLength2*  
 [输入]以字符为单位的长度 **SchemaName*。  
  
 *TableName*  
 [输入]表名称。 此参数不能为 null 指针。 *TableName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *TableName*视为标识符和其大小写并不重要。 SQL_FALSE，若是*TableName*是普通参数; 按字面意思，处理和其大小写很重要。  
  
 *NameLength3*  
 [输入]以字符为单位的长度 **TableName*。  
  
 *范围*  
 [输入]最小所需 rowid 作用的域。 返回的 rowid 可能会更大范围。 必须是下列选项之一：  
  
 SQL_SCOPE_CURROW 之外：保证 rowid 只有位于该行上时才有效。 如果行已更新或删除由另一个事务，请使用 rowid 中更高版本重新选择可能不返回行。  
  
 SQL_SCOPE_TRANSACTION:Rowid 保证可为当前事务的持续时间内有效。  
  
 SQL_SCOPE_SESSION:Rowid 保证在有效的会话的持续时间 （跨事务边界）。  
  
 *可以为 Null*  
 [输入]确定是否返回可以具有 NULL 值的特殊列。 必须是下列选项之一：  
  
 SQL_NO_NULLS:排除可以具有 NULL 值的特殊列。 某些驱动程序不能支持 SQL_NO_NULLS，并且这些驱动程序将返回空结果集如果 SQL_NO_NULLS 已指定。 仅当绝对必要时，应为此用例和请求 SQL_NO_NULLS 准备应用程序。  
  
 SQL_NULLABLE:返回特殊列，即使它们可以具有 NULL 值。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLSpecialColumns**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可能会通过调用来获取**SQLGetDiagRec**与*HandleType*的SQL_HANDLE_STMT 和一个*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLSpecialColumns** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|24000|游标状态无效|在打开游标的*StatementHandle*，并**SQLFetch**或**SQLFetchScroll**已调用一样。 如果此错误返回由驱动程序管理器**SQLFetch**或**SQLFetchScroll**未返回 SQL_NO_DATA 和时，返回的驱动程序**SQLFetch**或**SQLFetchScroll**已返回 sql_no_data 为止。<br /><br /> 在打开游标的*StatementHandle*，但**SQLFetch**或**SQLFetchScroll**尚未调用。|  
|40001|序列化失败|事务已回滚，由于其他事务与资源死锁。|  
|40003|语句完成情况未知|此函数中，在执行期间失败关联的连接，无法确定事务的状态。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY008|操作已取消|异步处理的已启用*StatementHandle*。 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*。 然后在再次调用该函数*StatementHandle*。<br /><br /> 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自不同线程中多线程应用程序。|  
|HY009|使用空指针无效|*TableName*参数是空指针。<br /><br /> SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *CatalogName*参数为 null 指针和 SQL_CATALOG_NAME*信息类型*支持目录名称返回。<br /><br /> (DM) SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE，并*SchemaName*参数是空指针。|  
|HY010|函数序列错误|(DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此函数仍在执行时**SQLSpecialColumns**调用。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*和返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 的调用以异步方式执行的函数 （不是此类似） *StatementHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 之一的长度参数值小于 0 但不是等于 SQL_NTS。<br /><br /> 长度参数之一的值超出相应名称的最大长度值。 可以通过调用获取每个名称的最大长度**SQLGetInfo**与*信息类型*值：SQL_MAX_CATALOG_NAME_LEN、 SQL_MAX_SCHEMA_NAME_LEN 或 SQL_MAX_TABLE_NAME_LEN。|  
|HY097|列类型超出了范围|(DM) 无效*IdentifierType*指定的值。|  
|HY098|作用域类型超出了范围|(DM) 无效*作用域*指定的值。|  
|HY099|可以为 null 类型超出了范围|(DM) 无效*Nullable*指定的值。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|指定一个目录，并在驱动程序或数据源不支持目录。<br /><br /> 指定了架构，并且在驱动程序或数据源不支持架构。<br /><br /> 驱动程序或数据源不支持 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 语句属性的当前设置的组合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_VARIABLE，并且 SQL_ATTR_CURSOR_TYPE 语句属性设置为游标类型，该驱动程序不支持书签。|  
|HYT00|超时时间已到|查询超时期限过期之前请求的结果集返回的数据源。 通过设置超时期限**SQLSetStmtAttr**，SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*StatementHandle*不支持该函数。|  
|IM017|轮询异步通知模式中禁用|只要使用通知模型，将禁用轮询。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上以前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用通知模式，则**SQLCompleteAsync**必须要对其进行后期处理并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 当*IdentifierType*自变量是 SQL_BEST_ROWID， **SQLSpecialColumns**返回唯一标识表中的每一行的列。 这些列始终可在*选择列表*或**其中**子句。 **SQLColumns**、 用于对表的列返回的各种信息不一定返回的列的唯一地标识每个行，或通过更新的行中的任何值时将自动更新的列事务。 例如， **SQLColumns**可能不会返回 Oracle 伪列 ROWID。 这就是为什么**SQLSpecialColumns**用于返回这些列。 有关详细信息，请参阅[使用的目录数据](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
> [!NOTE]  
>  有关常规使用、 参数以及 ODBC 目录函数返回的数据的详细信息，请参阅[目录函数](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 如果没有唯一地标识表中的每一行的列**SQLSpecialColumns**返回一个行集并且没有行; 的后续调用**SQLFetch**或**SQLFetchScroll**语句返回 sql_no_data 为止。  
  
 如果*IdentifierType*，*作用域*，或*Nullable*参数指定数据源不支持的特征**SQLSpecialColumns**返回空结果集。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *CatalogName*， *SchemaName*，并*TableName*参数被视为用作标识符，因此它们不能设置为在某些情况下是 null 指针。 (有关详细信息，请参阅[中目录函数的自变量](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。)  
  
 **SQLSpecialColumns**以按 SCOPE 排序标准结果集的形式返回结果。  
  
 以下各列已重命名为 ODBC 3 *.x*。 列名称更改不会影响后向兼容性，因为应用程序将绑定的列号。  
  
|ODBC 2.0 列|ODBC 3 *.x*列|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
  
 若要确定 COLUMN_NAME 列的实际长度，应用程序可以调用**SQLGetInfo** SQL_MAX_COLUMN_NAME_LEN 选项。  
  
 下表列出了在结果集中的列。 列 8 (PSEUDO_COLUMN) 之外的其他列可以定义由驱动程序。 应用程序应获得访问驱动程序特定列的结果集末尾的倒计时，而不是指定显式的序号位置。 有关详细信息，请参阅[目录函数返回数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|列名|列号|数据类型|注释|  
|-----------------|-------------------|---------------|--------------|  
|作用域 (ODBC 1.0)|1|Smallint|Rowid 的实际作用域。 包含以下值之一：<br /><br /> SQL_SCOPE_CURROW 之外 SQL_SCOPE_TRANSACTION SQL_SCOPE_SESSION<br /><br /> 则返回 NULL *IdentifierType*是 SQL_ROWVER。 有关每个值的说明，请参阅的说明*作用域*"语法"，前面在本部分中。|  
|COLUMN_NAME (ODBC 1.0)|2|Varchar 不为 NULL|列名称。 该驱动程序返回空字符串不具有名称的列。|  
|DATA_TYPE (ODBC 1.0)|3|Smallint（非 NULL）|SQL 数据类型。 这可以是 ODBC SQL 数据类型或特定于驱动程序的 SQL 数据类型。 有关有效的 ODBC SQL 数据类型的列表，请参阅[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)。 有关特定于驱动程序的 SQL 数据类型的信息，请参阅驱动程序的文档。|  
|TYPE_NAME (ODBC 1.0)|4|Varchar 不为 NULL|数据源相关的数据类型名称;"例如，CHAR"、"VARCHAR"、"MONEY"、"长 VARBINARY"或者"CHAR FOR BIT DATA （）"。|  
|COLUMN_SIZE (ODBC 1.0)|5|Integer|数据源中的列的大小。 有关列大小的详细信息，请参阅[列的大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|BUFFER_LENGTH (ODBC 1.0)|6|Integer|上传输的数据的字节长度**SQLGetData**或**SQLFetch**如果 SQL_C_DEFAULT 指定的操作。 对于数值数据，此大小可能不同于数据源上存储的数据量。 此值是为字符或二进制数据的 COLUMN_SIZE 列相同。 有关详细信息，请参阅[列的大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|DECIMAL_DIGITS (ODBC 1.0)|7|Smallint|数据源中的列小数位数。 不适用小数位数为数据类型则返回 NULL。 有关十进制数字的详细信息，请参阅[列的大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|PSEUDO_COLUMN (ODBC 2.0)|8|Smallint|指示列是否为伪列，如 Oracle ROWID:<br /><br /> SQL_PC_UNKNOWN SQL_PC_NOT_PSEUDO SQL_PC_PSEUDO**注意：** 最大互操作性，伪列不应引用与返回的引号字符的标识符**SQLGetInfo**。|  
  
 应用程序的 SQL_BEST_ROWID 检索值后，应用程序可以使用这些值来重新选择该定义的作用域内的行。 **选择**保证语句返回任何行或一行。  
  
 如果应用程序会重新选择基于行 id 列或列的行，并且找不到行，该行已删除或修改 rowid 列可以假定该应用程序。 反过来则不适用： 即使 rowid 不发生了更改，可能已更改行中的其他列。  
  
 为 SQL_BEST_ROWID 非常有用的应用程序的需要进行向前滚动和要从一组行中检索最新数据的结果集内返回的列类型返回的列。 列或列 rowid 保证不位于该行上时更改。  
  
 Rowid 的列可能会保持有效即使游标未定位在该行，则上应用程序可以通过检查中的结果集的作用域列来确定。  
  
 为列类型 SQL_ROWVER 非常有用的应用程序需要能够检查某一给定行中的任何列是否已更新行时看到使用 rowid 时返回的列。 例如，重新选择行使用 rowid 之后, 应用程序可以比较于只是提取的 SQL_ROWVER 列中的上一个值。 如果 SQL_ROWVER 列中的值不同于以前的值，该应用程序可以提醒用户上显示的数据已更改。  
  
## <a name="code-example"></a>代码示例  
 有关类似函数的代码示例，请参阅[SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|返回一个表或表中的列|[SQLColumns 函数](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|提取单个行或仅向前方向中的数据块|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取的数据块或滚动浏览结果集|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|返回主键的列|[SQLPrimaryKeys 函数](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
