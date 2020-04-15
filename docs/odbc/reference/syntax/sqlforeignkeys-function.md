---
title: SQL 外键功能 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5f2769fb378a5ee989fb6a0351537edb3de03469
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285857"
---
# <a name="sqlforeignkeys-function"></a>SQLForeignKeys 函数
**一致性**  
 版本介绍： ODBC 1.0 标准合规性： ODBC  
  
 **摘要**  
 **SQL 外键**可以返回：  
  
-   指定表中的外键列表（指定表中引用其他表中主键的列）。  
  
-   引用指定表中的主键的其他表中的外键的列表。  
  
 驱动程序返回每个列表作为指定语句上的结果集。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
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
 *语句句柄*  
 [输入]语句句柄。  
  
 *PK目录名称*  
 [输入]主键表目录名称。 如果驱动程序支持某些表的目录，但不支持其他表的目录（例如当驱动程序从不同的 DBMS 检索数据时），空字符串（""）表示那些没有目录的表。 *PK目录名称*不能包含字符串搜索模式。  
  
 如果SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，*则 PKCatalogName*被视为标识符，其大小写不重要。 如果*SQL_FALSE，PKCatalogName*是一个普通的参数;如果是SQL_FALSE，则 PKCatalogName 是一个普通参数。它被从字面上处理，它的情况很重要。 有关详细信息，请参阅[目录函数 中的参数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [输入]长度 =*PK目录名称*，以字符表示。  
  
 *PKSchema 名称*  
 [输入]主键表架构名称。 如果驱动程序支持某些表的架构，但不支持其他表的架构（例如当驱动程序从不同的 DBMS 检索数据时），则空字符串（""）表示那些没有架构的表。 *PKSchemaName*不能包含字符串搜索模式。  
  
 如果SQL_ATTR_METADATA_ID语句属性设置为*SQL_TRUE，PKSchemaName*将被视为标识符，其大小写不重要。 如果*SQL_FALSE，PKSchemaName*是一个普通的参数;如果是SQL_FALSE，则 PKSchemaName 是一个普通参数。它被从字面上处理，它的情况很重要。  
  
 *名称长度2*  
 [输入]长度 =*PKSchema 名称*，以字符表示。  
  
 *PKTable 名称*  
 [输入]主键表名称。 *PKTableName*不能包含字符串搜索模式。  
  
 如果SQL_ATTR_METADATA_ID语句属性设置为*SQL_TRUE，PKTableName*将被视为标识符，其大小写不重要。 如果是SQL_FALSE，PKTableName 是一个普通的参数;如果是，*则 PKTableName*是一个普通参数。它被从字面上处理，它的情况很重要。  
  
 *名称长度3*  
 [输入]长度 =*PKTableName*，以字符表示。  
  
 *FK目录名称*  
 [输入]外键表目录名称。 如果驱动程序支持某些表的目录，但不支持其他表的目录（例如当驱动程序从不同的 DBMS 检索数据时），空字符串（""）表示那些没有目录的表。 *FKCatalogName*不能包含字符串搜索模式。  
  
 如果将SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，*则 FKCatalogName*将被视为标识符，其大小写不重要。 如果SQL_FALSE，FKCatalogName 是一个普通的参数;如果是，*则为"FKCatalogName"，* 它是一个普通参数。它被从字面上处理，它的情况很重要。  
  
 *名称长度4*  
 [输入]长度 =*FKCatalog 名称*，以字符表示。  
  
 *FKSchema 名称*  
 [输入]外键表架构名称。 如果驱动程序支持某些表的架构，但不支持其他表的架构（例如当驱动程序从不同的 DBMS 检索数据时），则空字符串（""）表示那些没有架构的表。 *FKSchemaName*不能包含字符串搜索模式。  
  
 如果SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，*则 FKSchemaName*将被视为标识符，其大小写不重要。 如果SQL_FALSE，FKSchemaName 是一个普通的参数;如果是SQL_FALSE，*则 FKSchemaName*是一个普通参数。它被从字面上处理，它的情况很重要。  
  
 *名称长度5*  
 [输入]长度 =*FKSchema 名称*，以字符表示。  
  
 *FKTable 名称*  
 [输入]外键表名称。 *FKTableName*不能包含字符串搜索模式。  
  
 如果SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，*则 FKTableName*被视为标识符，其大小写不重要。 如果是SQL_FALSE，FKTableName 是一个普通的参数;如果是SQL_FALSE，*则 FKTableName*是一个普通参数。它被从字面上处理，它的情况很重要。  
  
 *名称长度6*  
 [输入]长度 =*FKTableName*，以字符表示。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQL 外键**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_STMT的*句柄类型*和*语句句柄*的*句柄*。 下表列出了**SQLOfKeys**通常返回的 SQLSTATE 值，并在此函数的上下文中解释每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|24000|无效的游标状态|语句*处理*上打开了一个游标，并且调用了**SQLFetch**或**SQLFetchScroll。** 如果**SQLFetch**或**SQLFetchScroll**未返回SQL_NO_DATA，则驱动程序管理器将返回此错误，如果**SQLFetch**或**SQLFetchScroll**已返回SQL_NO_DATA，则驱动程序将返回此错误。<br /><br /> *语句句柄*上打开了一个游标，但**SQLFetch**或**SQLFetchScroll**尚未调用。|  
|40001|序列化失败|由于资源与另一个事务死锁，事务被回滚。|  
|40003|报表完成未知|执行此函数期间，关联的连接失败，无法确定事务的状态。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY008|操作已取消|异步处理已启用*语句句柄*。 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**在*语句句柄*上调用 ，然后在*语句句柄*上再次调用该函数。<br /><br /> 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**是从多线程应用程序中的不同线程调用*的语句句柄*。|  
|HY009|无效使用空指针|（DM） 参数*PKTableName*和*FKTableName*都是空指针。<br /><br /> SQL_ATTR_METADATA_ID语句属性设置为*SQL_TRUE，FKCatalogName*或*PKCatalogName*参数为空指针，SQL_CATALOG_NAME *InfoType*返回目录名称受支持。<br /><br /> （DM） SQL_ATTR_METADATA_ID语句属性设置为*SQL_TRUE，FKSchema名称**、PKSchema名称**、FKTableName*或*PKTableName*参数为空指针。|  
|HY010|函数序列错误|（DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用 SQL 外键函数时，此异步函数仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用语句*句柄*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。<br /><br /> （DM） 为*语句句柄*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY090|无效的字符串或缓冲区长度|（DM） 其中一个名称长度参数的值小于 0，但不等于SQL_NTS。|  
|||其中一个名称长度参数的值超过相应名称的最大长度值。 （请参阅"注释"。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现可选功能|指定了目录名称，并且驱动程序或数据源不支持目录。<br /><br /> 指定了架构名称，驱动程序或数据源不支持架构。|  
|||驱动程序或数据源不支持SQL_ATTR_CONCURRENCY和SQL_ATTR_CURSOR_TYPE语句属性的当前设置的组合。<br /><br /> SQL_ATTR_USE_BOOKMARKS语句属性设置为SQL_UB_VARIABLE，SQL_ATTR_CURSOR_TYPE语句属性设置为驱动程序不支持书签的游标类型。|  
|HYT00|超时时间已到|查询超时期限在数据源返回结果集之前已过期。 超时期间通过**sqlSetStmtAttr**SQL_ATTR_QUERY_TIMEOUT设置。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*关联的驱动程序不支持该函数。|  
|IM017|在异步通知模式下禁用轮询|每当使用通知模型时，都会禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**以完成对此句柄的先前异步操作。|如果句柄上的上一个函数调用返回SQL_STILL_EXECUTING，并且启用了通知模式，则必须在句柄上调用**SQLCompleteAsync**以执行后处理并完成操作。|  
  
## <a name="comments"></a>注释  
 有关如何使用此函数返回的信息的信息，请参阅[目录数据的使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
 如果\* *PKTableName*包含表名 **，SQLOfKey**将返回一个结果集，其中包含指定表的主键和引用它的所有外键。 其他表中的外键列表不包括指向指定表中的唯一约束的外键。  
  
 如果\* *FKTableName*包含表名 **，SQL外键**将返回一个结果集，其中包含指定表中指向其他表中的主键的所有外键及其引用的其他表中的主键。 指定表中的外键列表不包含引用其他表中的唯一约束的外键。  
  
 如果\**PKTableName* \*和*FKTableName*都包含表名 **，SQLOfkey**将返回\**FKTableName*中指定的表中指定的外键，该键引用 #*PKTableName*中指定的表的主键。 这最多应该是一个关键。  
  
> [!NOTE]  
>  有关 ODBC 目录函数的一般使用、参数和返回数据的详细信息，请参阅[目录函数](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 **SQL 外键**将结果作为标准结果集返回。 如果请求与主键关联的外键，则结果集按FKTABLE_CAT、FKTABLE_SCHEM、FKTABLE_NAME和KEY_SEQ排序。 如果请求与外键关联的主键，则结果集按PKTABLE_CAT、PKTABLE_SCHEM、PKTABLE_NAME和KEY_SEQ排序。 下表列出了结果集中的列。  
  
 VARCHAR 列的长度不显示在表中;因此，VARCHAR 列的长度不显示在表中。实际长度取决于数据源。 要确定PKTABLE_CAT或FKTABLE_CAT、PKTABLE_SCHEM或FKTABLE_SCHEM、PKTABLE_NAME或FKTABLE_NAME以及PKCOLUMN_NAME或FKCOLUMN_NAME列的实际长度，应用程序可以使用SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、SQL_MAX_TABLE_NAME_LEN和SQL_MAX_COLUMN_NAME_LEN选项调用**SQLGetInfo。**  
  
 以下列已重命名为 ODBC 3 *.x。* 列名称更改不会影响向后兼容性，因为应用程序按列号绑定。  
  
|ODBC 2.0 列|ODBC 3 *.x*列|  
|---------------------|-----------------------|  
|PKTABLE_QUALIFIER|PKTABLE_CAT|  
|PKTABLE_OWNER|PKTABLE_SCHEM|  
|FKTABLE_QUALIFIER|FK_TABLE_CAT|  
|FKTABLE_OWNER|FKTABLE_SCHEM|  
  
 下表列出了结果集中的列。 驱动程序可以定义第 14 列 （注释）以外的其他列。 应用程序应通过从结果集的末尾倒计时而不是指定显式单位位置来获得对特定于驱动程序的列的访问权限。 有关详细信息，请参阅[目录函数返回的数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|列名称|列号|数据类型|注释|  
|-----------------|-------------------|---------------|--------------|  
|PKTABLE_CAT （ODBC 1.0）|1|Varchar|主键表目录名称;如果不适用于数据源，则为 NULL。 如果驱动程序支持某些表的目录，但不支持其他表的目录（例如当驱动程序从不同的 DBMS 检索数据时），它将返回一个空字符串（""），用于那些没有目录的表。|  
|PKTABLE_SCHEM （ODBC 1.0）|2|Varchar|主键表架构名称;如果不适用于数据源，则为 NULL。 如果驱动程序支持某些表的架构，但不支持其他表的架构（例如当驱动程序从不同的 DBMS 检索数据时），它将返回一个空字符串（""），用于那些没有架构的表。|  
|PKTABLE_NAME （ODBC 1.0）|3|瓦尔查尔不是 NULL|主键表名称。|  
|PKCOLUMN_NAME （ODBC 1.0）|4|瓦尔查尔不是 NULL|主键列名称。 驱动程序返回没有名称的列的空字符串。|  
|FKTABLE_CAT （ODBC 1.0）|5|Varchar|外键表目录名称;如果不适用于数据源，则为 NULL。 如果驱动程序支持某些表的目录，但不支持其他表的目录（例如当驱动程序从不同的 DBMS 检索数据时），它将返回一个空字符串（""），用于那些没有目录的表。|  
|FKTABLE_SCHEM （ODBC 1.0）|6|Varchar|外键表架构名称;如果不适用于数据源，则为 NULL。 如果驱动程序支持某些表的架构，但不支持其他表的架构（例如当驱动程序从不同的 DBMS 检索数据时），它将返回一个空字符串（""），用于那些没有架构的表。|  
|FKTABLE_NAME （ODBC 1.0）|7|瓦尔查尔不是 NULL|外键表名称。|  
|FKCOLUMN_NAME （ODBC 1.0）|8|瓦尔查尔不是 NULL|外键列名称。 驱动程序返回没有名称的列的空字符串。|  
|KEY_SEQ （ODBC 1.0）|9|Smallint（非 NULL）|键中的列序列号（以 1 开头）。|  
|UPDATE_RULE （ODBC 1.0）|10|Smallint|SQL 操作为**UPDATE**时要应用于外键的操作。 可以具有以下值之一。 （引用的表是具有主键的表;引用表是具有外键的表。<br /><br /> SQL_CASCADE：更新引用表的主键时，引用表的外键也会更新。<br /><br /> SQL_NO_ACTION：如果更新引用表的主键会导致引用表中的"悬空引用"（即引用表中的行在引用的表中没有对应项），则更新将被拒绝。 如果引用表的外键更新将引入作为引用表的主键的值不存在的值，则拒绝更新。 （此操作与 ODBC 2 *.x 中的*SQL_RESTRICT操作相同。<br /><br /> SQL_SET_NULL：当引用表中的一个或多个行以更改主键的一个或多个组件的方式更新时，引用表中对应于主键更改组件的外键的组件将设置为引用表的所有匹配行中的 NULL。<br /><br /> SQL_SET_DEFAULT：当引用表中的一个或多个行以更改主键的一个或多个组件的方式更新时，引用表中对应于主键已更改组件的外键的组件将设置为引用表所有匹配行中的适用默认值。<br /><br /> 如果不适用于数据源，则为 NULL。|  
|DELETE_RULE （ODBC 1.0）|11|Smallint|SQL 操作为**DELETE**时要应用于外键的操作。 可以具有以下值之一。 （引用的表是具有主键的表;引用表是具有外键的表。<br /><br /> SQL_CASCADE：删除引用表中的行时，引用表中的所有匹配行也将被删除。<br /><br /> SQL_NO_ACTION：如果删除引用表中的行会导致引用表中的"悬空引用"（即引用表中的行在引用的表中没有对应项），则更新将被拒绝。 （此操作与 ODBC 2 *.x 中的*SQL_RESTRICT操作相同。<br /><br /> SQL_SET_NULL：删除引用表中的一个或多个行时，引用表的外键的每个组件都设置为引用表的所有匹配行中的 NULL。<br /><br /> SQL_SET_DEFAULT：删除引用表中的一个或多个行时，引用表的外键的每个组件都设置为引用表所有匹配行中的适用默认值。<br /><br /> 如果不适用于数据源，则为 NULL。|  
|FK_NAME （ODBC 2.0）|12|Varchar|外键名称。 如果不适用于数据源，则为 NULL。|  
|PK_NAME （ODBC 2.0）|13|Varchar|主键名称。 如果不适用于数据源，则为 NULL。|  
|可延迟性（ODBC 3.0）|14|Smallint|SQL_INITIALLY_DEFERRED，SQL_INITIALLY_IMMEDIATE，SQL_NOT_DEFERRABLE|  
  
## <a name="code-example"></a>代码示例  
 如下表所示，此示例使用三个表，名为 ORDERS、LINES 和客户。  
  
|ORDERS|线|客户|  
|------------|-----------|---------------|  
|订单ID|订单ID|CUSTID|  
|CUSTID|线|名称|  
|开放日期|零件ID|地址|  
|售货员|数量|电话|  
|状态|||  
  
 在 ORDERS 表中，CUSTID 标识向其销售的客户。 它是在 CUSTOMERS 表中引用 CUSTID 的外键。  
  
 在 LINES 表中，ORDERID 标识与行物料关联的销售订单。 它是在 ORDERS 表中引用 ORDERID 的外键。  
  
 此示例调用**SQL 主要密钥**来获取 ORDERS 表的主键。 结果集将有一行;结果集将具有一行。下表显示了重要的列。  
  
|TABLE_NAME|COLUMN_NAME|KEY_SEQ|  
|-----------------|------------------|--------------|  
|ORDERS|订单ID|1|  
  
 接下来，该示例调用**SQLOfKey**来获取引用 ORDERS 表主键的其他表中的外键。 结果集将有一行;结果集将具有一行。下表显示了重要的列。  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|ORDERS|CUSTID|线|CUSTID|1|  
  
 最后，该示例调用**SQLOfKey**来获取 ORDERS 表中引用其他表的主键的外键。 结果集将有一行;结果集将具有一行。下表显示了重要的列。  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|客户|CUSTID|ORDERS|CUSTID|1|  
  
```cpp  
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
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|以仅转发方向获取单个行或数据块|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|获取数据块或滚动浏览结果集|[SQLFetchScroll Function（SQLFetchScroll 函数）](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|返回主键的列|[SQLPrimaryKeys 函数](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
|返回表统计信息和索引|[SQLStatistics 函数](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
