---
title: SQL 特殊列函数 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 826630e1d344322268a2f2638310b3a1e182de6d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287167"
---
# <a name="sqlspecialcolumns-function"></a>SQLSpecialColumns 函数
**一致性**  
 版本介绍： ODBC 1.0 标准合规性： 开放组  
  
 **摘要**  
 **SQL特别列**检索有关指定表中列的以下信息：  
  
-   唯一标识表中行的最佳列集。  
  
-   当行中的任何值由事务更新时自动更新的列。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
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
 *语句句柄*  
 [输入]语句句柄。  
  
 *标识符类型*  
 [输入]要返回的列的类型。 必须是以下值之一：  
  
 SQL_BEST_ROWID：返回最佳列或列集，通过从列或列检索值，允许唯一标识指定表中的任何行。 列可以是专门为此设计的伪列（如 Oracle ROWID 或 Inres TID 中），也可以是表任何唯一索引的列或列。  
  
 SQL_ROWVER：返回指定表中的列或列（如果有），当行中的任何值由任何事务更新时（如 SQLBase ROWID 或 Sybase TIMESTAMP 中），数据源会自动更新的列（  
  
 *CatalogName*  
 [输入]表的目录名称。 如果驱动程序支持某些表的目录，但不支持其他表的目录（例如当驱动程序从不同的 DBMS 检索数据时），空字符串（""）表示那些没有目录的表。 *目录名称*不能包含字符串搜索模式。  
  
 如果SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，则*目录名称*将被视为标识符，其大小写不重要。 如果SQL_FALSE，目录名称是普通参数;如果为"*目录名称"，则为"目录名称"，* 但为"目录名称"，但为"目录名称"，但它被从字面上处理，它的情况很重要。 有关详细信息，请参阅[目录函数 中的参数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [输入]长度在 **目录名称*的字符中。  
  
 *架构名称*  
 [输入]表的架构名称。 如果驱动程序支持某些表的架构，但不支持其他表的架构（例如当驱动程序从不同的 DBMS 检索数据时），则空字符串（""）表示那些没有架构的表。 *架构名称*不能包含字符串搜索模式。  
  
 如果SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，*则 SchemaName*被视为标识符，其大小写不重要。 如果SQL_FALSE，SchemaName 是一个普通的参数;如果是SQL_FALSE，则 *"架构名称"* 是普通参数。它被从字面上处理，它的情况很重要。  
  
 *名称长度2*  
 [输入]长度在 **架构名称*的字符中。  
  
 *表名称*  
 [输入]表名称。 此参数不能为空指针。 *表名称*不能包含字符串搜索模式。  
  
 如果SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，*则表Name*被视为标识符，其大小写不重要。 如果SQL_FALSE，*则表名*是普通参数;如果为 SQL_FALSE，则表名称为普通参数。它被从字面上处理，它的情况很重要。  
  
 *名称长度3*  
 [输入]=*表名*的字符的长度。  
  
 *范围*  
 [输入]排 ID 的最小所需范围。 返回的划线可能具有更大的范围。 必须是下列选项之一：  
  
 SQL_SCOPE_CURROW：保证行 id 仅在定位该行时有效。 如果行已更新或删除另一个事务，则稍后使用行重新选择可能不会返回该行。  
  
 SQL_SCOPE_TRANSACTION： 保证行 id 在当前事务期间有效。  
  
 SQL_SCOPE_SESSION：保证行 id 在会话期间（跨事务边界）有效。  
  
 *可以为 Null*  
 [输入]确定是否返回具有 NULL 值的特殊列。 必须是下列选项之一：  
  
 SQL_NO_NULLS：排除具有 NULL 值的特殊列。 某些驱动程序不支持SQL_NO_NULLS，如果指定了SQL_NO_NULLS，这些驱动程序将返回空结果集。 申请应为本案例做好准备，只有在绝对需要的情况下才SQL_NO_NULLS请求。  
  
 SQL_NULLABLE：返回特殊列，即使它们可以具有 NULL 值。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQL 特别列**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_STMT的*句柄类型*和*语句句柄*的*句柄*。 下表列出了**SQLSpecialColumns**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|24000|无效的游标状态|语句*处理*上打开了一个游标，并且调用了**SQLFetch**或**SQLFetchScroll。** 如果**SQLFetch**或**SQLFetchScroll**未返回SQL_NO_DATA，则驱动程序管理器将返回此错误，如果**SQLFetch**或**SQLFetchScroll**已返回SQL_NO_DATA，则驱动程序将返回此错误。<br /><br /> *语句句柄*上打开了一个游标，但**SQLFetch**或**SQLFetchScroll**尚未调用。|  
|40001|序列化失败|由于与另一个事务的资源死锁，事务已回滚。|  
|40003|报表完成未知|执行此函数期间，关联的连接失败，无法确定事务的状态。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY008|操作已取消|异步处理已启用*语句句柄*。 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**调用了*语句句柄*。 然后在*语句处理*上再次调用该函数。<br /><br /> 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**是从多线程应用程序中的不同线程调用*的语句句柄*。|  
|HY009|无效使用空指针|*表名称*参数是空指针。<br /><br /> SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，*目录名称*参数为空指针，SQL_CATALOG_NAME *InfoType*返回目录名称受支持。<br /><br /> （DM） SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，*而 SchemaName*参数是空指针。|  
|HY010|函数序列错误|（DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用**SQL 特殊列时**，此函数仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用语句*句柄*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。<br /><br /> （DM） 为*语句句柄*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY090|无效的字符串或缓冲区长度|（DM） 长度参数之一的值小于 0，但不等于SQL_NTS。<br /><br /> 其中一个长度参数的值超过了相应名称的最大长度值。 使用*InfoType*值调用**SQLGetInfo，** 可以获取每个名称的最大长度：SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN 或SQL_MAX_TABLE_NAME_LEN。|  
|HY097|列类型范围外|（DM） 指定了无效的*标识符类型*值。|  
|HY098|范围类型范围外|（DM） 指定了无效*的范围*值。|  
|HY099|空类型范围外|（DM） 指定了无效*的空值*。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现可选功能|指定了目录，驱动程序或数据源不支持目录。<br /><br /> 已指定架构，驱动程序或数据源不支持架构。<br /><br /> 驱动程序或数据源不支持SQL_ATTR_CONCURRENCY和SQL_ATTR_CURSOR_TYPE语句属性的当前设置的组合。<br /><br /> SQL_ATTR_USE_BOOKMARKS语句属性设置为SQL_UB_VARIABLE，SQL_ATTR_CURSOR_TYPE语句属性设置为驱动程序不支持书签的游标类型。|  
|HYT00|超时时间已到|查询超时期限在数据源返回请求的结果集之前已过期。 超时期间通过**sqlSetStmtAttr**SQL_ATTR_QUERY_TIMEOUT设置。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*关联的驱动程序不支持该函数。|  
|IM017|在异步通知模式下禁用轮询|每当使用通知模型时，都会禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**以完成对此句柄的先前异步操作。|如果句柄上的上一个函数调用返回SQL_STILL_EXECUTING，并且启用了通知模式，则必须在句柄上调用**SQLCompleteAsync**以执行后处理并完成操作。|  
  
## <a name="comments"></a>注释  
 当*标识符类型*参数SQL_BEST_ROWID时 **，SQL特别列**将返回唯一标识表中每一行的列。 这些列始终可用于*选择列表*或**WHERE**子句。 **SQLColumns**用于返回表列上的各种信息，但不一定返回唯一标识每行的列，也不一定返回在事务更新行中的任何值时自动更新的列。 例如 **，SQLColumn**可能不会返回 Oracle 伪列 ROWID。 这就是为什么**SQL 特殊列**用于返回这些列的原因。 有关详细信息，请参阅[目录数据的使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
> [!NOTE]  
>  有关 ODBC 目录函数的一般使用、参数和返回数据的详细信息，请参阅[目录函数](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 如果没有唯一标识表中每行的列 **，SQLSpecialColumns**将返回一个没有行的行集;如果列表将返回一行。语句上的**SQLFetch**或**SQLFetchScroll**的后续调用返回SQL_NO_DATA。  
  
 如果*标识符类型*、*作用域*或*空参数*指定数据源不支持的特征 **，SQL特别列**将返回一个空的结果集。  
  
 如果SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，则*目录名称*、*架构名称*和*表名称*参数将被视为标识符，因此在某些情况下无法将其设置为空指针。 （有关详细信息，请参阅[目录函数中的参数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 **SQL特别列**将结果作为标准结果集返回，由 SCOPE 排序。  
  
 以下列已重命名为 ODBC *3.x*。 列名称更改不会影响向后兼容性，因为应用程序按列号绑定。  
  
|ODBC 2.0 列|ODBC *3.x*列|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
  
 要确定COLUMN_NAME列的实际长度，应用程序可以使用SQL_MAX_COLUMN_NAME_LEN选项调用**SQLGetInfo。**  
  
 下表列出了结果集中的列。 驱动程序可以定义第 8 列（PSEUDO_COLUMN）以外的其他列。 应用程序应通过从结果集的末尾倒计时而不是指定显式单位位置来获得对特定于驱动程序的列的访问权限。 有关详细信息，请参阅[目录函数返回的数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|列名称|列号|数据类型|注释|  
|-----------------|-------------------|---------------|--------------|  
|范围（ODBC 1.0）|1|Smallint|行 ID 的实际范围。 包含以下值之一：<br /><br /> SQL_SCOPE_CURROWSQL_SCOPE_TRANSACTIONSQL_SCOPE_SESSION<br /><br /> 当*标识符类型*SQL_ROWVER时，将返回 NULL。 有关每个值的说明，请参阅本节前面"语法"中*的范围*说明。|  
|COLUMN_NAME （ODBC 1.0）|2|瓦尔查尔不是 NULL|列名称。 驱动程序返回没有名称的列的空字符串。|  
|DATA_TYPE （ODBC 1.0）|3|Smallint（非 NULL）|SQL 数据类型。 这可以是 ODBC SQL 数据类型或特定于驱动程序的 SQL 数据类型。 有关有效的 ODBC SQL 数据类型的列表，请参阅[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)。 有关特定于驱动程序的 SQL 数据类型的信息，请参阅驱动程序的文档。|  
|TYPE_NAME （ODBC 1.0）|4|瓦尔查尔不是 NULL|与数据源相关的数据类型名称;例如，"CHAR"，"VARCHAR"，"金钱"，"长VARBINARY"，或"CHAR （ ） BIT 数据"。|  
|COLUMN_SIZE （ODBC 1.0）|5|Integer|数据源上的列的大小。 有关列大小的详细信息，请参阅[列大小、十进制数字、传输八点长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|BUFFER_LENGTH （ODBC 1.0）|6|Integer|如果指定了SQL_C_DEFAULT，则在**SQLGetData**或**SQLFetch**操作上传输的数据的长度（以字节为单位）。 对于数字数据，此大小可能与存储在数据源上的数据的大小不同。 此值与字符或二进制数据的COLUMN_SIZE列相同。 有关详细信息，请参阅[列大小、十进制数字、传输八点长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|DECIMAL_DIGITS （ODBC 1.0）|7|Smallint|数据源上列的小数位数。 对于不适用十进制数字的数据类型，返回 NULL。 有关十进制数字的详细信息，请参阅[列大小、十进制数字、传输八点长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|PSEUDO_COLUMN （ODBC 2.0）|8|Smallint|指示列是否是伪列，例如 Oracle ROWID：<br /><br /> SQL_PC_UNKNOWNSQL_PC_NOT_PSEUDOSQL_PC_PSEUDO**注意：** 为了最大的互操作性，不应引用**SQLGetInfo**返回的标识符引号字符。|  
  
 应用程序检索SQL_BEST_ROWID的值后，应用程序可以使用这些值在定义的作用域中重新选择该行。 **SELECT**语句保证不返回任何行或一行。  
  
 如果应用程序根据行 id 列或列重新选择行，但找不到该行，则应用程序可以假定该行已被删除或已修改行。 相反的不是：即使行 ID 未更改，行中的其他列也可能已更改。  
  
 为列类型返回的列SQL_BEST_ROWID对于需要在结果集中向前和向后滚动以从一组行中检索最新数据的应用程序很有用。 行 id 的列或列保证在定位该行时不会更改。  
  
 即使光标未放置在行上，划线器的列也可能保持有效;应用程序可以通过检查结果集中的 SCOPE 列来确定这一点。  
  
 为列类型返回的列SQL_ROWVER对于需要能够检查给定行中的任何列是否已更新，而使用行重新选择行的应用程序非常有用。 例如，使用 rowid 重新选择行后，应用程序可以将SQL_ROWVER列中以前的值与刚刚提取的值进行比较。 如果SQL_ROWVER列中的值与前一个值不同，应用程序可以提醒用户显示上的数据已更改。  
  
## <a name="code-example"></a>代码示例  
 有关类似函数的代码示例，请参阅[SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|返回表或表中的列|[SQLColumns 函数](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|以仅转发方向获取单个行或数据块|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|获取数据块或滚动浏览结果集|[SQLFetchScroll Function（SQLFetchScroll 函数）](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|返回主键的列|[SQLPrimaryKeys 函数](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
