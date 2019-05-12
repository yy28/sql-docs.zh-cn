---
title: SQLColumnPrivileges 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLColumnPrivileges
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColumnPrivileges
helpviewer_keywords:
- SQLColumnPrivileges function [ODBC]
ms.assetid: ef233d9a-6ed5-4986-9d42-5e0b1a79fb6e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10d05310f7d9580b652f24bffa0896e32b23a40a
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537712"
---
# <a name="sqlcolumnprivileges-function"></a>SQLColumnPrivileges 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：ODBC  
  
 **摘要**  
 **SQLColumnPrivileges**返回的列和指定表关联的特权的列表。 驱动程序将返回作为结果集对指定的信息*StatementHandle*。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLColumnPrivileges(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3,  
     SQLCHAR *     ColumnName,  
     SQLSMALLINT   NameLength4);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *CatalogName*  
 [输入]目录名称。 如果驱动程序支持名称为某些目录而不是其他人，例如当驱动程序检索数据从不同 Dbms，空字符串 ("") 表示没有名称的目录。 *CatalogName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *CatalogName*视为标识符和其大小写并不重要。 SQL_FALSE，若是*CatalogName*是普通参数; 按字面意思，处理和其大小写很重要。 有关详细信息，请参阅[中目录函数的自变量](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [输入]以字符为单位的长度 **CatalogName*。  
  
 *SchemaName*  
 [输入]架构名称。 如果驱动程序支持架构有关的某些表而不是其他人，例如当驱动程序检索数据从不同 Dbms，空字符串 ("") 表示没有架构的那些表。 *SchemaName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *SchemaName*视为标识符。 SQL_FALSE，若是*SchemaName*是普通参数; 按字面意思，处理和其大小写很重要。  
  
 *NameLength2*  
 [输入]以字符为单位的长度 **SchemaName*。  
  
 *TableName*  
 [输入]表名称。 此参数不能为 null 指针。 *TableName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *TableName*视为标识符和其大小写并不重要。 SQL_FALSE，若是*TableName*是普通参数; 按字面意思，处理和其大小写很重要。  
  
 *NameLength3*  
 [输入]以字符为单位的长度 **TableName*。  
  
 *ColumnName*  
 [输入]列名称的字符串搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *ColumnName*视为标识符和其大小写并不重要。 SQL_FALSE，若是*ColumnName*是模式值自变量; 按字面意思，处理和其大小写很重要。  
  
 *NameLength4*  
 [输入]以字符为单位的长度 **ColumnName*。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLColumnPrivileges**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可能会通过调用来获取**SQLGetDiagRec**与*HandleType*设置为 SQL_HANDLE_STMT，和一个*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLColumnPrivileges** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前的驱动程序返回 SQLSTATEs 说明管理器。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|24000|游标状态无效|在打开游标的*StatementHandle，* 并**SQLFetch**或**SQLFetchScroll**已调用一样。 如果此错误返回由驱动程序管理器**SQLFetch**或**SQLFetchScroll**未返回 SQL_NO_DATA，和如果驱动程序返回**SQLFetch**或**SQLFetchScroll**已返回 sql_no_data 为止。<br /><br /> 在打开游标的*StatementHandle*，但**SQLFetch**或**SQLFetchScroll**尚未调用。|  
|40001|序列化失败|事务已回滚，由于其他事务与资源死锁。|  
|40003|语句完成情况未知|此函数中，在执行期间失败关联的连接，无法确定事务的状态。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY008|操作已取消|异步处理的已启用*StatementHandle*。 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*。 然后在再次调用该函数*StatementHandle*。<br /><br /> 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自不同线程中多线程应用程序。|  
|HY009|使用空指针无效|*TableName*参数是空指针。<br /><br /> SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *CatalogName*参数为 null 指针和 SQL_CATALOG_NAME*信息类型*支持目录名称返回。<br /><br /> (DM) SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE，并*SchemaName*或*ColumnName*参数是空指针。|  
|HY010|函数序列错误|(DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*和返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 的调用以异步方式执行的函数 （不是此类似） *StatementHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 之一的名称长度参数值小于 0 但不是等于 SQL_NTS。|  
|||名称长度参数之一的值超出相应名称的最大长度值。 （请参阅"注释"。）|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|指定的目录名称，并在驱动程序或数据源不支持目录。<br /><br /> 指定的架构名称，并在驱动程序或数据源不支持架构。<br /><br /> 列名称，为指定的字符串搜索模式和数据源不支持该自变量的搜索模式。<br /><br /> 驱动程序或数据源不支持 SQL_CONCURRENCY 和 SQL_CURSOR_TYPE 语句属性的当前设置的组合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_VARIABLE，并且 SQL_ATTR_CURSOR_TYPE 语句属性设置为游标类型，该驱动程序不支持书签。|  
|HYT00|超时时间已到|查询超时期限过期之前的数据源返回的结果集。 通过设置超时期限**SQLSetStmtAttr**，SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*StatementHandle*不支持该函数。|  
|IM017|轮询异步通知模式中禁用|只要使用通知模型，将禁用轮询。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上以前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用通知模式，则**SQLCompleteAsync**必须要对其进行后期处理并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 **SQLColumnPrivileges**以标准的结果集，TABLE_CAT、 按 TABLE_SCHEM、 TABLE_NAME、 COLUMN_NAME 和特权按排序格式返回结果。  
  
> [!NOTE]  
>  **SQLColumnPrivileges**可能不会返回所有列的权限。 例如，驱动程序可能不返回伪列，如 Oracle ROWID 的特权的信息。 应用程序可以使用任何有效的列，而不管是否返回由**SQLColumnPrivileges**。  
  
 VARCHAR 列的长度未显示在表;实际长度取决于数据源。 若要确定 CATALOG_NAME、 SCHEMA_NAME、 TABLE_NAME 和 COLUMN_NAME 列的实际长度，应用程序可以调用**SQLGetInfo**与 SQL_MAX_CATALOG_NAME_LEN，SQL_MAX_SCHEMA_NAME_LEN，SQL_MAX_TABLE_NAME_LEN、 和 SQL_MAX_COLUMN_NAME_LEN 选项。  
  
> [!NOTE]  
>  有关常规使用、 参数以及 ODBC 目录函数返回的数据的详细信息，请参阅[目录函数](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 对于 ODBC 3 重命名为以下各列。*x*。 列名称更改不会影响后向兼容性，因为应用程序将绑定的列号。  
  
|ODBC 2.0 列|ODBC 3。*x*列|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 下表列出了在结果集中的列。 列 8 (IS_GRANTABLE) 之外的其他列可以定义由驱动程序。 应用程序应获得访问驱动程序特定列的结果集末尾的倒计时，而不是指定显式的序号位置。 有关详细信息，请参阅[目录函数返回数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|列名|列号|数据类型|注释|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|目录的标识符;如果不适用于数据源为 NULL。 如果驱动程序支持目录有关的某些表而不是其他人，如当驱动程序检索数据时从不同 Dbms，它返回空字符串 ("") 不具有目录这些表。|  
|按 TABLE_SCHEM (ODBC 1.0)|2|Varchar|架构标识符;如果不适用于数据源为 NULL。 如果驱动程序支持架构有关的某些表而不是其他人，如当驱动程序检索数据时从不同 Dbms，它返回空字符串 ("") 不具有架构的这些表。|  
|TABLE_NAME (ODBC 1.0)|3|Varchar 不为 NULL|表标识符。|  
|COLUMN_NAME (ODBC 1.0)|4|Varchar 不为 NULL|列名称。 该驱动程序返回空字符串不具有名称的列。|  
|授权者 (ODBC 1.0)|5|Varchar|授予权限; 用户的名称如果不适用于数据源为 NULL。<br /><br /> 对于被授权者列中的值与对象的所有者的所有行，GRANTOR 列将为"（_s）"。|  
|被授权者 (ODBC 1.0)|6|Varchar 不为 NULL|向其授予权限的用户的名称。|  
|特权 (ODBC 1.0)|7|Varchar 不为 NULL|标识列权限。 可能是以下值之一 (或其他支持的数据源时实现定义):<br /><br /> 选择：允许被授权者检索数据的列。<br /><br /> 插入：允许被授权者提供新行插入到关联的表中的列的数据。<br /><br /> 更新：允许被授权者更新的列中的数据。<br /><br /> 引用：允许被授权者引用约束中的列 (例如，唯一、 引用，或检查约束的表)。|  
|IS_GRANTABLE (ODBC 1.0)|8|Varchar|指示是否允许被授权者向其他用户; 授予权限"是"、"否"，或"NULL"如果未知或不适用于数据源。<br /><br /> 权限是可授予或没有可授予，而不是两者。 返回的结果集**SQLColumnPrivileges**将永远不会包含除 IS_GRANTABLE 列的所有列都包含相同的值的两个行。|  
  
## <a name="code-example"></a>代码示例  
 有关类似函数的代码示例，请参阅[SQLColumns 函数](../../../odbc/reference/syntax/sqlcolumns-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|返回一个表或表中的列|[SQLColumns 函数](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|提取的数据块或滚动浏览结果集|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|正在提取多行数据|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|返回一个表或表的权限|[SQLTablePrivileges 函数](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
|数据源中返回的表的列表|[SQLTables 函数](../../../odbc/reference/syntax/sqltables-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
