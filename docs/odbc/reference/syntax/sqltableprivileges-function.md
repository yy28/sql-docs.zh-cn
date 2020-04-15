---
title: SQLTable 特权函数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2d8260dd285fb3f5bbb9fcdaeaaebf1586090179
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282917"
---
# <a name="sqltableprivileges-function"></a>SQLTablePrivileges Function（SQLTablePrivileges 函数）
**一致性**  
 版本介绍： ODBC 1.0 标准合规性： ODBC  
  
 **摘要**  
 **SQLTable 特权**返回表列表以及与每个表关联的权限。 驱动程序将返回信息作为指定语句上的结果集。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
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
 *语句句柄*  
 [输入]语句句柄。  
  
 *CatalogName*  
 [输入]表目录。 如果驱动程序支持某些表的目录，但不支持其他表的目录（例如当驱动程序从不同的 DBMS 检索数据时），空字符串（""）表示那些没有目录的表。 *目录名称*不能包含字符串搜索模式。  
  
 如果SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，则*目录名称*将被视为标识符，其大小写不重要。 如果SQL_FALSE，目录名称是普通参数;如果为"*目录名称"，则为"目录名称"，* 但为"目录名称"，但为"目录名称"，但它被从字面上处理，它的情况很重要。 有关详细信息，请参阅[目录函数 中的参数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [输入]长度在 **目录名称*的字符中。  
  
 *架构名称*  
 [输入]架构名称的字符串搜索模式。 如果驱动程序支持某些表的架构，但不支持其他表的架构（例如当驱动程序从不同的 DBMS 检索数据时），则空字符串（""）表示那些没有架构的表。  
  
 如果SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，*则 SchemaName*被视为标识符，其大小写不重要。 如果SQL_FALSE，则 SchemaName 是模式值参数;如果为 SQL_FALSE，则 *"架构名称"* 是模式值参数。它被从字面上处理，它的情况很重要。  
  
 *名称长度2*  
 [输入]长度在 **架构名称*的字符中。  
  
 *表名称*  
 [输入]表名称的字符串搜索模式。  
  
 如果SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，*则表Name*被视为标识符，其大小写不重要。 如果SQL_FALSE，*则表名称*是模式值参数;如果为"表名称"，则表名称是模式值参数。它被从字面上处理，它的情况很重要。  
  
 *名称长度3*  
 [输入]=*表名*的字符的长度。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLTable 特权**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_STMT*Handle*的*句柄类型*和*语句句柄*。 下表列出了 SQLTable 特权通常返回的**SQLSTATE**值，并解释了此函数上下文中的每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|24000|无效的游标状态|语句*处理*上打开了一个游标，并且调用了**SQLFetch**或**SQLFetchScroll。** 如果**SQLFetch**或**SQLFetchScroll**未返回SQL_NO_DATA，则驱动程序管理器将返回此错误，如果**SQLFetch**或**SQLFetchScroll**已返回SQL_NO_DATA，则驱动程序将返回此错误。<br /><br /> *语句句柄*上打开了一个游标，但**SQLFetch**或**SQLFetchScroll**尚未调用。|  
|40001|序列化失败|由于与另一个事务的资源死锁，事务已回滚。|  
|40003|报表完成未知|执行此函数期间，关联的连接失败，无法确定事务的状态。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY008|操作已取消|异步处理已启用*语句句柄*。 **SQLTable特权**函数被调用，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**调用了*语句句柄*。 然后，在*语句句柄*上再次调用**SQLTable 特权**函数。<br /><br /> **SQLTable特权**函数被调用，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**是从多线程应用程序中的不同线程调用*的语句句柄*。|  
|HY009|无效使用空指针|SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，*目录名称*参数为空指针，SQL_CATALOG_NAME *InfoType*返回目录名称受支持。<br /><br /> （DM） SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，*而 SchemaName*或*TableName*参数是空指针。|  
|HY010|函数序列错误|（DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用**SQLTable 特权**函数时，此异步函数仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用语句*句柄*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。<br /><br /> （DM） 为*语句句柄*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY090|无效的字符串或缓冲区长度|（DM） 其中一个名称长度参数的值小于 0，但不等于SQL_NTS。<br /><br /> 其中一个名称长度参数的值超过相应限定符或名称的最大长度值。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现可选功能|指定了目录，驱动程序或数据源不支持目录。<br /><br /> 已指定架构，驱动程序或数据源不支持架构。<br /><br /> 为表架构、表名称或列名称指定了字符串搜索模式，数据源不支持一个或多个这些参数的搜索模式。<br /><br /> 驱动程序或数据源不支持SQL_ATTR_CONCURRENCY和SQL_ATTR_CURSOR_TYPE语句属性的当前设置的组合。<br /><br /> SQL_ATTR_USE_BOOKMARKS语句属性设置为SQL_UB_VARIABLE，SQL_ATTR_CURSOR_TYPE语句属性设置为驱动程序不支持书签的游标类型。|  
|HYT00|超时时间已到|查询超时期限在数据源返回结果集之前已过期。 超时期间通过**sqlSetStmtAttr**SQL_ATTR_QUERY_TIMEOUT设置。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*关联的驱动程序不支持该函数。|  
|IM017|在异步通知模式下禁用轮询|每当使用通知模型时，都会禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**以完成对此句柄的先前异步操作。|如果句柄上的上一个函数调用返回SQL_STILL_EXECUTING，并且启用了通知模式，则必须在句柄上调用**SQLCompleteAsync**以执行后处理并完成操作。|  
  
## <a name="comments"></a>注释  
 *架构名称*和*表名称*参数接受搜索模式。 有关有效搜索模式的详细信息，请参阅[模式值参数](../../../odbc/reference/develop-app/pattern-value-arguments.md)。  
  
 **SQLTable特权**将结果作为标准结果集返回，该结果由TABLE_CAT、TABLE_SCHEM、TABLE_NAME、特权和 GRANTEE 排序。  
  
 要确定TABLE_CAT、TABLE_SCHEM和TABLE_NAME列的实际长度，应用程序可以使用SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN和SQL_MAX_TABLE_NAME_LEN选项调用**SQLGetInfo。**  
  
> [!NOTE]  
>  有关 ODBC 目录函数的一般使用、参数和返回数据的详细信息，请参阅[目录函数](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 以下列已重命名为 ODBC *3.x*。 列名称更改不会影响向后兼容性，因为应用程序按列号绑定。  
  
|ODBC 2.0 列|ODBC *3.x*列|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 下表列出了结果集中的列。 驱动程序可以定义第 7 列（IS_GRANTABLE）以外的其他列。 应用程序应通过从结果集的末尾倒计时而不是指定显式单位位置来获得对特定于驱动程序的列的访问权限。 有关详细信息，请参阅[目录函数返回的数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|列名称|列号|数据类型|注释|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT （ODBC 1.0）|1|Varchar|目录名称;如果不适用于数据源，则为 NULL。 如果驱动程序支持某些表的目录，但不支持其他表的目录（例如当驱动程序从不同的 DBMS 检索数据时），它将返回一个空字符串（""），用于那些没有目录的表。|  
|TABLE_SCHEM （ODBC 1.0）|2|Varchar|架构名称;如果不适用于数据源，则为 NULL。 如果驱动程序支持某些表的架构，但不支持其他表的架构（例如当驱动程序从不同的 DBMS 检索数据时），它将返回一个空字符串（""），用于那些没有架构的表。|  
|TABLE_NAME （ODBC 1.0）|3|瓦尔查尔不是 NULL|表名。|  
|格兰特（ODBC 1.0）|4|Varchar|授予该权限的用户的名称;如果不适用于数据源，则为 NULL。<br /><br /> 对于"GRANTEE"列中的值是对象所有者的所有行，GRANTOR 列将为"_SYSTEM"。|  
|格兰特 （ODBC 1.0）|5|瓦尔查尔不是 NULL|授予特权的用户的名称。|  
|特权 （ODBC 1.0）|6|瓦尔查尔不是 NULL|表权限。 可以是以下权限之一或特定于数据源的权限。<br /><br /> 选择：允许受让人检索表的一个或多个列的数据。<br /><br /> INSERT：允许受让人将包含一个或多个列的数据的新行插入到表中。<br /><br /> 更新：允许受让人更新表的一个或多个列中的数据。<br /><br /> 删除：允许受让人从表中删除数据行。<br /><br /> 参考：允许受让人引用约束中的表的一个或多个列（例如，唯一、引用或表检查约束）。<br /><br /> 允许受让人具有给定表特权的操作范围取决于数据源。 例如，UPDATE 权限可能允许受让人更新一个数据源表中的所有列，并且仅更新设保人在另一个数据源上具有 UPDATE 权限的列。|  
|IS_GRANTABLE （ODBC 1.0）|7|Varchar|指示是否允许受赠方向其他用户授予该权限;因此，是否允许受赠方授予该权限。"是"、"否"或 NULL（未知或不适用于数据源）。<br /><br /> 特权可以是可授予的，也可以是不可授予的，但不能同时授予这两种特权。 **SQLColumn特权**返回的结果集永远不会包含除IS_GRANTABLE列之外所有列都包含相同值的两行。|  
  
## <a name="code-example"></a>代码示例  
 有关类似函数的代码示例，请参阅[SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|返回列或列的权限|[SQLColumnPrivileges 函数](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|返回表或表中的列|[SQLColumns 函数](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|以仅转发方向获取单个行或数据块|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|获取数据块或滚动浏览结果集|[SQLFetchScroll Function（SQLFetchScroll 函数）](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|返回表统计信息和索引|[SQLStatistics 函数](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|返回数据源中的表列表|[SQLTables 函数](../../../odbc/reference/syntax/sqltables-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
