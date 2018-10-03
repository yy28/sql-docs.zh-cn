---
title: SQLForeignKeys 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLForeignKeys
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLForeignKeys
helpviewer_keywords:
- SQLForeignKeys function [ODBC]
ms.assetid: 07f3f645-f643-4d39-9a10-70a72f24e608
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5901a2c3e126674b1157177a6c7937c58058764
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47601045"
---
# <a name="sqlforeignkeys-function"></a>SQLForeignKeys 函数
**符合性**  
 版本引入了： ODBC 1.0 标准符合性： ODBC  
  
 **摘要**  
 **SQLForeignKeys**可以返回：  
  
-   指定的表 （列指定的表中引用其他表中的主键） 中的外键的列表。  
  
-   中到指定的表中的主键，请参阅其他表的外键列表。  
  
 驱动程序将返回每个列表作为结果集上指定的语句。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLForeignKeys(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      PKCatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      PKSchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      PKTableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      FKCatalogName,  
     SQLSMALLINT    NameLength4,  
     SQLCHAR *      FKSchemaName,  
     SQLSMALLINT    NameLength5,  
     SQLCHAR *      FKTableName,  
     SQLSMALLINT    NameLength6);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *PKCatalogName*  
 [输入]主键表目录名称。 如果驱动程序支持目录有关的某些表而不是其他人，例如当驱动程序检索数据从不同 Dbms，空字符串 ("") 表示没有目录的那些表。 *PKCatalogName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *PKCatalogName*视为标识符和其大小写并不重要。 SQL_FALSE，若是*PKCatalogName*是普通参数; 按字面意思，处理和其大小写很重要。 有关详细信息，请参阅[中目录函数的自变量](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [输入]长度 **PKCatalogName*，以字符为单位。  
  
 *PKSchemaName*  
 [输入]主键表架构名称。 如果驱动程序支持架构有关的某些表而不是其他人，例如当驱动程序检索数据从不同 Dbms，空字符串 ("") 表示没有架构的那些表。 *PKSchemaName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *PKSchemaName*视为标识符和其大小写并不重要。 SQL_FALSE，若是*PKSchemaName*是普通参数; 按字面意思，处理和其大小写很重要。  
  
 *NameLength2*  
 [输入]长度 **PKSchemaName*，以字符为单位。  
  
 *PKTableName*  
 [输入]主键表名。 *PKTableName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *PKTableName*视为标识符和其大小写并不重要。 SQL_FALSE，若是*PKTableName*是普通参数; 按字面意思，处理和其大小写很重要。  
  
 *NameLength3*  
 [输入]长度 **PKTableName*，以字符为单位。  
  
 *FKCatalogName*  
 [输入]外键表目录名称。 如果驱动程序支持目录有关的某些表而不是其他人，例如当驱动程序检索数据从不同 Dbms，空字符串 ("") 表示没有目录的那些表。 *FKCatalogName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *FKCatalogName*视为标识符和其大小写并不重要。 SQL_FALSE，若是*FKCatalogName*是普通参数; 按字面意思，处理和其大小写很重要。  
  
 *NameLength4*  
 [输入]长度 **FKCatalogName*，以字符为单位。  
  
 *FKSchemaName*  
 [输入]外键表架构名称。 如果驱动程序支持架构有关的某些表而不是其他人，例如当驱动程序检索数据从不同 Dbms，空字符串 ("") 表示没有架构的那些表。 *FKSchemaName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *FKSchemaName*视为标识符和其大小写并不重要。 SQL_FALSE，若是*FKSchemaName*是普通参数; 按字面意思，处理和其大小写很重要。  
  
 *NameLength5*  
 [输入]长度 **FKSchemaName*，以字符为单位。  
  
 *FKTableName*  
 [输入]外键表名。 *FKTableName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *FKTableName*视为标识符和其大小写并不重要。 SQL_FALSE，若是*FKTableName*是普通参数; 按字面意思，处理和其大小写很重要。  
  
 *NameLength6*  
 [输入]长度 **FKTableName*，以字符为单位。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLForeignKeys**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用来获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和一个*处理*的*StatementHandle*。 下表列出了通常由返回的 SQLSTATE 值**SQLForeignKeys** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|24000|游标状态无效|在打开游标的*StatementHandle*，并**SQLFetch**或**SQLFetchScroll**已调用一样。 如果此错误返回由驱动程序管理器**SQLFetch**或**SQLFetchScroll**未返回 SQL_NO_DATA，和如果驱动程序返回**SQLFetch**或**SQLFetchScroll**已返回 sql_no_data 为止。<br /><br /> 在打开游标的*StatementHandle*，但**SQLFetch**或**SQLFetchScroll**尚未调用。|  
|40001|序列化失败|事务已回滚，由于其他事务与资源死锁。|  
|40003|语句完成情况未知|此函数中，在执行期间失败关联的连接，无法确定事务的状态。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY008|操作已取消|异步处理的已启用*StatementHandle*。 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*，然后调用该函数是在上再次*StatementHandle*。<br /><br /> 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自不同线程中多线程应用程序。|  
|HY009|使用空指针无效|(DM) 参数*PKTableName*并*FKTableName*了两个 null 指针。<br /><br /> SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *FKCatalogName*或*PKCatalogName*参数为 null 指针和 SQL_CATALOG_NAME*信息类型*支持目录名称返回。<br /><br /> (DM) SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE，并*FKSchemaName*， *PKSchemaName*， *FKTableName*，或*PKTableName*参数是空指针。|  
|HY010|函数序列错误|(DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行调用 SQLForeignKeys 函数时。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*和返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 的调用以异步方式执行的函数 （不是此类似） *StatementHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 之一的名称长度参数值小于 0 但不是等于 SQL_NTS。|  
|||名称长度参数之一的值超出相应名称的最大长度值。 （请参阅"注释"。）|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|指定的目录名称，并在驱动程序或数据源不支持目录。<br /><br /> 指定的架构名称，并在驱动程序或数据源不支持架构。|  
|||驱动程序或数据源不支持 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 语句属性的当前设置的组合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_VARIABLE，并且 SQL_ATTR_CURSOR_TYPE 语句属性设置为游标类型，该驱动程序不支持书签。|  
|HYT00|超时时间已到|查询超时期限过期之前的数据源返回的结果集。 通过设置超时期限**SQLSetStmtAttr**，SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*StatementHandle*不支持该函数。|  
|IM017|轮询异步通知模式中禁用|只要使用通知模型，将禁用轮询。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上以前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用通知模式，则**SQLCompleteAsync**必须要对其进行后期处理并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 了解可以如何使用此函数返回的信息，请参阅[使用的目录数据](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
 如果\* *PKTableName*包含一个表名称， **SQLForeignKeys**返回包含指定的表的主键和对其进行引用的所有外键的结果集。 其他表中的外键的列表不包括指向 unique 约束指定表中的外键。  
  
 如果\* *FKTableName*包含一个表名称， **SQLForeignKeys**返回结果集包含指定的表中指向其他表中主键的所有外键和引用的其他表中的主键。 指定表中的外键的列表不包含外键引用其他表中的唯一约束。  
  
 如果这两个\* *PKTableName*并\* *FKTableName*包含表名称**SQLForeignKeys**返回指定的表中的外键在中\* *FKTableName*到指定的表中的主键，请参阅 **PKTableName*。 这应该最多是一个键。  
  
> [!NOTE]  
>  有关常规使用、 参数以及 ODBC 目录函数返回的数据的详细信息，请参阅[目录函数](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 **SQLForeignKeys**作为标准的结果集返回结果。 如果请求与主键相关联的外键，结果集是按 FKTABLE_CAT、 FKTABLE_SCHEM、 FKTABLE_NAME 以及 KEY_SEQ 排序。 如果请求的主键与外键关联，结果集是按 PKTABLE_CAT、 PKTABLE_SCHEM、 PKTABLE_NAME 和 KEY_SEQ 排序。 下表列出了在结果集中的列。  
  
 VARCHAR 列的长度未显示在表;实际长度取决于数据源。 若要确定 PKTABLE_CAT 或 FKTABLE_CAT、 PKTABLE_SCHEM 或 FKTABLE_SCHEM 的实际长度，PKTABLE_NAME 或 FKTABLE_NAME 和 PKCOLUMN_NAME 或 FKCOLUMN_NAME 列，应用程序可以调用**SQLGetInfo**与 SQL_MAX_CATALOG_NAME_LEN、 SQL_MAX_SCHEMA_NAME_LEN、 SQL_MAX_TABLE_NAME_LEN 和 SQL_MAX_COLUMN_NAME_LEN 选项。  
  
 以下各列已重命名为 ODBC 3 *。 x。* 列名称更改不会影响后向兼容性，因为应用程序将绑定的列号。  
  
|ODBC 2.0 列|ODBC 3 *.x*列|  
|---------------------|-----------------------|  
|PKTABLE_QUALIFIER|PKTABLE_CAT|  
|PKTABLE_OWNER|PKTABLE_SCHEM|  
|FKTABLE_QUALIFIER|FK_TABLE_CAT|  
|FKTABLE_OWNER|FKTABLE_SCHEM|  
  
 下表列出了在结果集中的列。 列 14 （备注) 之外的其他列可以定义由驱动程序。 应用程序应获得访问驱动程序特定列的倒计时从结果集而不是指定显式的序号位置的末尾。 有关详细信息，请参阅[目录函数返回数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|列名|列号|数据类型|注释|  
|-----------------|-------------------|---------------|--------------|  
|PKTABLE_CAT (ODBC 1.0)|1|Varchar|主键表目录名称;如果不适用于数据源为 NULL。 如果驱动程序支持目录有关的某些表而不是其他人，如当驱动程序检索数据时从不同 Dbms，它返回空字符串 ("") 不具有目录这些表。|  
|PKTABLE_SCHEM (ODBC 1.0)|2|Varchar|主键表架构名称;如果不适用于数据源为 NULL。 如果驱动程序支持架构有关的某些表而不是其他人，如当驱动程序检索数据时从不同 Dbms，它返回空字符串 ("") 不具有架构的这些表。|  
|PKTABLE_NAME (ODBC 1.0)|3|Varchar 不为 NULL|主键表名。|  
|PKCOLUMN_NAME (ODBC 1.0)|4|Varchar 不为 NULL|主键列名称。 该驱动程序返回空字符串不具有名称的列。|  
|FKTABLE_CAT (ODBC 1.0)|5|Varchar|外键表目录名称;如果不适用于数据源为 NULL。 如果驱动程序支持目录有关的某些表而不是其他人，如当驱动程序检索数据时从不同 Dbms，它返回空字符串 ("") 不具有目录这些表。|  
|FKTABLE_SCHEM (ODBC 1.0)|6|Varchar|外键表架构名称;如果不适用于数据源为 NULL。 如果驱动程序支持架构有关的某些表而不是其他人，如当驱动程序检索数据时从不同 Dbms，它返回空字符串 ("") 不具有架构的这些表。|  
|FKTABLE_NAME (ODBC 1.0)|7|Varchar 不为 NULL|外键表名。|  
|FKCOLUMN_NAME (ODBC 1.0)|8|Varchar 不为 NULL|外键列名称。 该驱动程序返回空字符串不具有名称的列。|  
|KEY_SEQ (ODBC 1.0)|9|Smallint（非 NULL）|密钥 （从 1 开始） 中的列序号。|  
|UPDATE_RULE (ODBC 1.0)|10|Smallint|当 SQL 操作时要应用于外键的操作**更新**。 可以具有以下值之一。 （引用的表是具有主键的表; 引用表具有外键的表。）<br /><br /> SQL_CASCADE： 当更新所引用的表的主键时，引用表的外键也会更新。<br /><br /> SQL_NO_ACTION： 如果主键的更新所引用的表将导致"无关联引用"中引用的表 （即，引用表中的行必须没有对等引用表中），更新将被拒绝。 如果引用表的外键的更新中引入一个值，为被引用表的主键的值不存在，更新将被拒绝。 (此操作等同于 ODBC 2 中的 SQL_RESTRICT 操作 *.x*。)<br /><br /> SQL_SET_NULL： 时，更改一个或多个组件的主键值的方式更新引用表中的一个或多个行，对应于已更改的组件的主键值的引用表中的外键的组件设置为 NULL 的引用表的所有匹配行中。<br /><br /> SQL_SET_DEFAULT： 时，更改一个或多个组件的主键值的方式更新引用表中的一个或多个行，引用表中的外键对应的主键已更改的组件的组件是将设置为在引用表的所有匹配行中的适用的默认值。<br /><br /> 如果不适用于数据源为 NULL。|  
|DELETE_RULE (ODBC 1.0)|11|Smallint|当 SQL 操作时要应用于外键的操作**删除**。 可以具有以下值之一。 （引用的表是具有主键的表; 引用表具有外键的表。）<br /><br /> SQL_CASCADE： 删除所引用的表中的行时，引用表中的所有匹配行也会删除。<br /><br /> SQL_NO_ACTION： 如果删除行中引用的表将导致"无关联引用"中引用的表 （即，引用表中的行必须没有对等引用表中），更新将被拒绝。 (此操作等同于 ODBC 2 中的 SQL_RESTRICT 操作 *.x*。)<br /><br /> SQL_SET_NULL： 被引用表中的一个或多个行中删除时外, 键引用表的每个组件设置为 NULL 的引用表的所有匹配行中。<br /><br /> SQL_SET_DEFAULT： 时删除引用表中的一个或多个行时外, 键引用表的每个组件设置为在引用表的所有匹配行中适用的默认值。<br /><br /> 如果不适用于数据源为 NULL。|  
|FK_NAME (ODBC 2.0)|12|Varchar|外键的名称。 如果不适用于数据源为 NULL。|  
|PK_NAME (ODBC 2.0)|13|Varchar|主键名称。 如果不适用于数据源为 NULL。|  
|延迟 (ODBC 3.0)|14|Smallint|SQL_INITIALLY_DEFERRED，SQL_INITIALLY_IMMEDIATE，SQL_NOT_DEFERRABLE。|  
  
## <a name="code-example"></a>代码示例  
 下表中所示，此示例使用三个表，名为 ORDERS、 线条和客户。  
  
|ORDERS|行|客户|  
|------------|-----------|---------------|  
|订单 ID|订单 ID|CUSTID|  
|CUSTID|行|NAME|  
|OPENDATE|PARTID|地址|  
|销售人员|数量|电话|  
|STATUS|||  
  
 在订单表中，CUSTID 标识的客户已对其进行销售。 它是指 CUSTID CUSTOMERS 表中的外键。  
  
 在行表中，ORDERID 标识销售订单行项与之关联。 它是指订单 id 中订单表的外键。  
  
 此示例调用**SQLPrimaryKeys**获取 ORDERS 表的主键。 结果集将具有一个行;下表中显示重要的列。  
  
|TABLE_NAME|COLUMN_NAME|KEY_SEQ|  
|-----------------|------------------|--------------|  
|ORDERS|订单 ID|1|  
  
 接下来，该示例将调用**SQLForeignKeys**以获取其他引用的订单表的主键的表中的外键。 结果集将具有一个行;下表中显示重要的列。  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|ORDERS|CUSTID|行|CUSTID|1|  
  
 最后，该示例将调用**SQLForeignKeys**获取订单表中的外键引用的其他表的主键。 结果集将具有一个行;下表中显示重要的列。  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|客户|CUSTID|ORDERS|CUSTID|1|  
  
```  
#define TAB_LEN SQL_MAX_TABLE_NAME_LEN + 1  
#define COL_LEN SQL_MAX_COLUMN_NAME_LEN + 1  
  
LPSTR   szTable;              /* Table to display */  
  
UCHAR szPkTable[TAB_LEN];   /* Primary key table name */  
UCHAR szFkTable[TAB_LEN];   /* Foreign key table name */  
UCHAR szPkCol[COL_LEN];     /* Primary key column */  
UCHAR szFkCol[COL_LEN];     /* Foreign key column */  
  
SQLHSTMT      hstmt;  
SQLINTEGER    cbPkTable, cbPkCol, cbFkTable, cbFkCol, cbKeySeq;  
SQLSMALLINT   iKeySeq;  
SQLRETURN     retcode;  
  
// Bind the columns that describe the primary and foreign keys.  
// Ignore the table schema, name, and catalog for this example.  
  
SQLBindCol(hstmt, 3, SQL_C_CHAR, szPkTable, TAB_LEN, &cbPkTable);  
SQLBindCol(hstmt, 4, SQL_C_CHAR, szPkCol, COL_LEN, &cbPkCol);  
SQLBindCol(hstmt, 5, SQL_C_SSHORT, &iKeySeq, TAB_LEN, &cbKeySeq);  
SQLBindCol(hstmt, 7, SQL_C_CHAR, szFkTable, TAB_LEN, &cbFkTable);  
SQLBindCol(hstmt, 8, SQL_C_CHAR, szFkCol, COL_LEN, &cbFkCol);  
  
strcpy_s(szTable, sizeof(szTable), "ORDERS");  
  
/* Get the names of the columns in the primary key. */  
  
retcode = SQLPrimaryKeys(hstmt,  
         NULL, 0,             /* Catalog name */  
         NULL, 0,             /* Schema name */  
         szTable, SQL_NTS);   /* Table name */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL SUCCESS_WITH_INFO)) {  
  
   /* Fetch and display the result set. This will be a list of the */  
   /* columns in the primary key of the ORDERS table. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "Table: %s Column: %s Key Seq: %hd \n", szPkTable, szPkCol,  
      iKeySeq);  
}  
  
/* Close the cursor (the hstmt is still allocated). */  
  
SQLFreeStmt(hstmt, SQL_CLOSE);  
  
/* Get all the foreign keys that refer to ORDERS primary key.*/   
  
retcode = SQLForeignKeys(hstmt,  
         NULL, 0,            /* Primary catalog */  
         NULL, 0,            /* Primary schema */  
         szTable, SQL_NTS,   /* Primary table */  
         NULL, 0,            /* Foreign catalog */  
         NULL, 0,            /* Foreign schema */  
         NULL, 0);           /* Foreign table */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL_SUCCESS_WITH_INFO)) {  
  
/* Fetch and display the result set. This will be all of the */  
/* foreign keys in other tables that refer to the ORDERS */  
/* primary key. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "%-s ( %-s ) <-- %-s ( %-s )\n", szPkTable,  
               szPkCol, szFkTable, szFkCol);  
}  
  
/* Close the cursor (the hstmt is still allocated). */  
  
SQLFreeStmt(hstmt, SQL_CLOSE);  
  
/* Get all the foreign keys in the ORDERS table. */  
  
retcode = SQLForeignKeys(hstmt,  
         NULL, 0,             /* Primary catalog */  
         NULL, 0,             /* Primary schema */  
         NULL, 0,             /* Primary table */  
         NULL, 0,             /* Foreign catalog */  
         NULL, 0,             /* Foreign schema */  
         szTable, SQL_NTS);   /* Foreign table */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL_SUCCESS_WITH_INFO)) {  
  
/* Fetch and display the result set. This will be all of the */  
/* primary keys in other tables that are referred to by foreign */  
/* keys in the ORDERS table. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "%-s ( %-s )--> %-s ( %-s )\n", szFkTable, szFkCol, szPkTable, szPkCol);  
}  
  
/* Free the hstmt. */  
SQLFreeStmt(hstmt, SQL_DROP);  
```  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|提取单个行或仅向前方向中的数据块|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取的数据块或滚动浏览结果集|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|返回主键的列|[SQLPrimaryKeys 函数](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
|返回表统计信息和索引|[SQLStatistics 函数](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
