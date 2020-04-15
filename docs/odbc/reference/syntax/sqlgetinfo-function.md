---
title: SQLGetInfo 功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetInfo
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetInfo
helpviewer_keywords:
- SQLGetInfo function [ODBC]
ms.assetid: 49dceccc-d816-4ada-808c-4c6138dccb64
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 514922fd085cfd2ba19eb5c07dd844db82d55202
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303339"
---
# <a name="sqlgetinfo-function"></a>SQLGetInfo 函数
**一致性**  
 推出版本： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLGetInfo**返回有关与连接关联的驱动程序和数据源的一般信息。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLGetInfo(  
     SQLHDBC         ConnectionHandle,  
     SQLUSMALLINT    InfoType,  
     SQLPOINTER      InfoValuePtr,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>参数  
 *连接句柄*  
 [输入] 连接句柄。  
  
 *信息类型*  
 [输入]信息类型。  
  
 *信息价值Ptr*  
 [输出]指向要返回信息的缓冲区的指针。 根据请求*的信息类型*，返回的信息将如下：空端字符字符串、SQLUSMALLINT 值、SQLUINTEGER 位掩码、SQLUINTEGER 标志、SQLUINTEGER 二进制值或 SQLULEN 值。  
  
 如果*InfoType*参数是SQL_DRIVER_HDESC或SQL_DRIVER_HSTMT，*则 InfoValuePtr*参数既是输入参数，也是输出参数。 （有关详细信息，请参阅此函数说明中的SQL_DRIVER_HDESC或SQL_DRIVER_HSTMT描述符。  
  
 如果*InfoValuePtr*为 NULL，*则 StringLengthPtr*仍将返回可用在*InfoValuePtr*指向的缓冲区中返回的字节总数（不包括字符数据的空终止字符）。  
  
 *缓冲区长度*  
 [输入]\**信息值Ptr*缓冲区的长度。 如果*\*InfoValuePtr*中的值不是字符串，或者如果*InfoValuePtr*是空指针，则忽略*缓冲区长度*参数。 驱动程序假定*\*InfoValuePtr*的大小是 SQLUSMALLINT 或 SQLUINTEGER，具体取决于*信息类型*。 如果*\*InfoValuePtr*是 Unicode 字符串（在调用**SQLGetInfoW**时），*则缓冲区长度*参数必须是偶数;否则，将返回 SQLSTATE HY090（无效字符串或缓冲区长度）。  
  
 *字符串长度 Ptr*  
 [输出]指向一个缓冲区的指针，用于返回可在 #*InfoValuePtr*中返回的字节总数（不包括字符数据的空终止字符）。  
  
 对于字符数据，如果可供返回的字节数大于或等于*BufferLength，*\**则 InfoValuePtr*中的信息将被截断为*BufferLength*字节减去空终止字符的长度，并且由驱动程序终止。  
  
 对于所有其他类型的数据，*将忽略缓冲区长度*的值，并且驱动程序假定\**InfoValuePtr*的大小为 SQLUSMALLINT 或 SQLUINTEGER，具体取决于*InfoType*。  
  
## <a name="return-value"></a>返回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetInfo**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_DBC的*句柄类型*和*连接句柄*的*句柄*。 下表列出了**SQLGetInfo**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01004|字符串数据，右截断|缓冲区\* *InfoValuePtr*不够大，无法返回所有请求的信息。 因此，信息被截断。 在其未压缩形式中请求的信息的长度在 #*StringLengthPtr*中返回。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|08003|连接未打开|（DM）*信息类型*中请求的信息类型需要打开的连接。 在 ODBC 保留的信息类型中，只有SQL_ODBC_VER无需打开的连接即可返回。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY010|函数序列错误|（DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用语句*句柄*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY024|无效属性值|（DM）*信息类型*参数*SQL_DRIVER_HSTMT，InfoValuePtr*指向的值不是有效的语句句柄。<br /><br /> （DM） *infoType*参数*SQL_DRIVER_HDESC，InfoValuePtr*指向的值不是有效的描述符句柄。|  
|HY090|无效的字符串或缓冲区长度|（DM） 为参数*BufferLength*指定的值小于 0。<br /><br /> （DM） 为*BufferLength*指定的值是奇数*\*，InfoValuePtr*为 Unicode 数据类型。|  
|HY096|信息类型范围外|为参数*InfoType*指定的值对驱动程序支持的 ODBC 版本无效。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现可选字段|为参数*InfoType*指定的值是驱动程序不支持的特定于驱动程序的值。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 对应于*连接句柄*的驱动程序不支持该功能。|  
  
## <a name="comments"></a>注释  
 当前定义的信息类型显示在"信息类型"中，本节后面的部分将显示这些类型;预计将定义更多，以利用不同的数据源。 ODBC 保留一系列信息类型;驱动程序开发人员必须从 Open Group 为其特定于驱动程序使用保留值。 **SQLGetInfo**不执行用于驱动程序定义的*InfoType 的*Unicode 转换或*分项*（参见[附录 A：ODBC](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md) *程序员参考的*ODBC 错误代码）。 有关详细信息，请参阅[特定于驱动程序的数据类型、描述符类型、信息类型、诊断类型和属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。 \**在 InfoValuePtr*中返回的信息格式取决于请求*的信息类型*。 **SQLGetInfo**将以五种不同格式之一返回信息：  
  
-   空终止字符串  
  
-   SQLUSMALLINT 值  
  
-   SQLUINTEGER 位掩码  
  
-   SQLUinTEGER 值  
  
-   SQLUinTEGER 二进制值  
  
 以下每种信息类型的格式都记录在类型的描述中。 应用程序必须相应地在 #*InfoValuePtr*中转换返回的值。 有关应用程序如何从 SQLUINTEGER 位掩码检索数据的示例，请参阅"代码示例"。  
  
 驱动程序必须为下表中定义的每种信息类型返回一个值。 如果信息类型不适用于驱动程序或数据源，则驱动程序将返回下表中列出的值之一。  
  
 字符串（"Y"或"N"）  
 "N"  
  
 字符串（不是"Y"或"N"）  
 空字符串  
  
 SQLUSMALLINT  
 0  
  
 SQLUinteGER 位掩码或 SQLUINTEGER 二进制值  
 0L  
  
 例如，如果数据源不支持过程 **，SQLGetInfo**将返回下表中列出的与过程相关的*InfoType*值的值。  
  
 SQL_PROCEDURES  
 "N"  
  
 SQL_ACCESSIBLE_PROCEDURES  
 "N"  
  
 SQL_MAX_PROCEDURE_NAME_LEN  
 0  
  
 SQL_PROCEDURE_TERM  
 空字符串  
  
 **SQLGetInfo**返回 SQLSTATE HY096（无效参数值），用于*InfoType*的值，这些值位于为 ODBC 保留以供使用的信息类型范围内，但不受驱动程序支持的 ODBC 版本定义。 要确定驱动程序符合的 ODBC 版本，应用程序使用SQL_DRIVER_ODBC_VER信息类型调用**SQLGetInfo。** **SQLGetInfo**返回 SQLSTATE HYC00（未实现可选功能）*的信息类型*值，这些值在为特定于驱动程序使用而保留的信息类型范围内，但驱动程序不支持。  
  
 对**SQLGetInfo**的所有调用都需要打开的连接，除非*信息类型*SQL_ODBC_VER，这将返回驱动程序管理器的版本。  
  
## <a name="information-types"></a>信息类型  
 本节列出了**SQLGetInfo**支持的信息类型。 信息类型按分类和按字母顺序列出。 还列出了为 ODBC 3 *.x*添加或重命名的信息类型。  
  
## <a name="driver-information"></a>驱动程序信息  
 *InfoType*参数的以下值返回有关 ODBC 驱动程序的信息，例如活动语句的数量、数据源名称和接口标准符合性级别：  
  
|||  
|-|-|  
|SQL_ACTIVE_ENVIRONMENTS|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
|SQL_ASYNC_DBC_FUNCTIONS|SQL_FILE_USAGE|  
|SQL_ASYNC_MODE|SQL_GETDATA_EXTENSIONS|  
|SQL_ASYNC_NOTIFICATION|SQL_INFO_SCHEMA_VIEWS|  
|SQL_BATCH_ROW_COUNT|SQL_KEYSET_CURSOR_ATTRIBUTES1|  
|SQL_BATCH_SUPPORT|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
|SQL_DATA_SOURCE_NAME|SQL_MAX_ASYNC_CONCURRENT_STATEMENTS|  
|SQL_DRIVER_AWARE_POOLING_SUPPORTED|SQL_MAX_CONCURRENT_ACTIVITIES|  
|SQL_DRIVER_HDBC|SQL_MAX_DRIVER_CONNECTIONS|  
|SQL_DRIVER_HDESC|SQL_ODBC_INTERFACE_CONFORMANCE|  
|SQL_DRIVER_HENV|SQL_ODBC_STANDARD_CLI_CONFORMANCE|  
|SQL_DRIVER_HLIB|SQL_ODBC_VER|  
|SQL_DRIVER_HSTMT|SQL_PARAM_ARRAY_ROW_COUNTS|  
|SQL_DRIVER_NAME|SQL_PARAM_ARRAY_SELECTS|  
|SQL_DRIVER_ODBC_VER|SQL_ROW_UPDATES|  
|SQL_DRIVER_VER|SQL_SEARCH_PATTERN_ESCAPE|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES1|SQL_SERVER_NAME|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|SQL_STATIC_CURSOR_ATTRIBUTES1|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|SQL_STATIC_CURSOR_ATTRIBUTES2|  
  
> [!NOTE]  
>  实现**SQLGetInfo**时，驱动程序可以通过最小化从服务器发送或请求信息的次数来提高性能。  
  
## <a name="dbms-product-information"></a>DBMS 产品信息  
 *InfoType*参数的以下值返回有关 DBMS 产品的信息，例如 DBMS 名称和版本：  
  
 SQL_DATABASE_NAMESQL_DBMS_NAMESQL_DBMS_VER  
  
## <a name="data-source-information"></a>数据源信息  
 *InfoType*参数的以下值返回有关数据源的信息，例如游标特征和事务功能：  
  
|||  
|-|-|  
|SQL_ACCESSIBLE_PROCEDURES|SQL_MULT_RESULT_SETS|  
|SQL_ACCESSIBLE_TABLES|SQL_MULTIPLE_ACTIVE_TXN|  
|SQL_BOOKMARK_PERSISTENCE|SQL_NEED_LONG_DATA_LEN|  
|SQL_CATALOG_TERM|SQL_NULL_COLLATION|  
|SQL_COLLATION_SEQ|SQL_PROCEDURE_TERM|  
|SQL_CONCAT_NULL_BEHAVIOR|SQL_SCHEMA_TERM|  
|SQL_CURSOR_COMMIT_BEHAVIOR|SQL_SCROLL_OPTIONS|  
|SQL_CURSOR_ROLLBACK_BEHAVIOR|SQL_TABLE_TERM|  
|SQL_CURSOR_SENSITIVITY|SQL_TXN_CAPABLE|  
|SQL_DATA_SOURCE_READ_ONLY|SQL_TXN_ISOLATION_OPTION|  
|SQL_DEFAULT_TXN_ISOLATION|SQL_USER_NAME|  
|SQL_DESCRIBE_PARAMETER||  
  
## <a name="supported-sql"></a>支持的 SQL  
 *InfoType*参数的以下值返回有关数据源支持的 SQL 语句的信息。 这些信息类型描述的每个功能的 SQL 语法是 SQL-92 语法。 这些信息类型不能详尽地描述整个 SQL-92 语法。 相反，它们描述了数据源通常为其提供不同级别的支持的语法部分。 具体来说，SQL-92 中的大多数 DDL 语句都包括在内。  
  
 应用程序应从SQL_SQL_CONFORMANCE信息类型确定支持的语法的一般级别，并使用其他信息类型来确定与规定标准合规性级别的变体。  
  
|||  
|-|-|  
|SQL_AGGREGATE_FUNCTIONS|SQL_DROP_TABLE|  
|SQL_ALTER_DOMAIN|SQL_DROP_TRANSLATION|  
|SQL_ALTER_SCHEMA|SQL_DROP_VIEW|  
|SQL_ALTER_TABLE|SQL_EXPRESSIONS_IN_ORDERBY|  
|SQL_ANSI_SQL_DATETIME_LITERALS|SQL_GROUP_BY|  
|SQL_CATALOG_LOCATION|SQL_IDENTIFIER_CASE|  
|SQL_CATALOG_NAME|SQL_IDENTIFIER_QUOTE_CHAR|  
|SQL_CATALOG_NAME_SEPARATOR|SQL_INDEX_KEYWORDS|  
|SQL_CATALOG_USAGE|SQL_INSERT_STATEMENT|  
|SQL_COLUMN_ALIAS|SQL_INTEGRITY|  
|SQL_CORRELATION_NAME|SQL_KEYWORDS|  
|SQL_CREATE_ASSERTION|SQL_LIKE_ESCAPE_CLAUSE|  
|SQL_CREATE_CHARACTER_SET|SQL_NON_NULLABLE_COLUMNS|  
|SQL_CREATE_COLLATION|SQL_SQL_CONFORMANCE|  
|SQL_CREATE_DOMAIN|SQL_OJ_CAPABILITIES|  
|SQL_CREATE_SCHEMA|SQL_ORDER_BY_COLUMNS_IN_SELECT|  
|SQL_CREATE_TABLE|SQL_OUTER_JOINS|  
|SQL_CREATE_TRANSLATION|SQL_PROCEDURES|  
|SQL_DDL_INDEX|SQL_QUOTED_IDENTIFIER_CASE|  
|SQL_DROP_ASSERTION|SQL_SCHEMA_USAGE|  
|SQL_DROP_CHARACTER_SET|SQL_SPECIAL_CHARACTERS|  
|SQL_DROP_COLLATION|SQL_SUBQUERIES|  
|SQL_DROP_DOMAIN|SQL_UNION|  
|SQL_DROP_SCHEMA||  
  
## <a name="sql-limits"></a>SQL 限制  
 *InfoType*参数的以下值返回有关应用于 SQL 语句中的标识符和子句的限制的信息，例如标识符的最大长度和选择列表中的最大列数。 驱动程序或数据源都可以施加限制。  
  
|||  
|-|-|  
|SQL_MAX_BINARY_LITERAL_LEN|SQL_MAX_IDENTIFIER_LEN|  
|SQL_MAX_CATALOG_NAME_LEN|SQL_MAX_INDEX_SIZE|  
|SQL_MAX_CHAR_LITERAL_LEN|SQL_MAX_PROCEDURE_NAME_LEN|  
|SQL_MAX_COLUMN_NAME_LEN|SQL_MAX_ROW_SIZE|  
|SQL_MAX_COLUMNS_IN_GROUP_BY|SQL_MAX_ROW_SIZE_INCLUDES_LONG|  
|SQL_MAX_COLUMNS_IN_INDEX|SQL_MAX_SCHEMA_NAME_LEN|  
|SQL_MAX_COLUMNS_IN_ORDER_BY|SQL_MAX_STATEMENT_LEN|  
|SQL_MAX_COLUMNS_IN_SELECT|SQL_MAX_TABLE_NAME_LEN|  
|SQL_MAX_COLUMNS_IN_TABLE|SQL_MAX_TABLES_IN_SELECT|  
|SQL_MAX_CURSOR_NAME_LEN|SQL_MAX_USER_NAME_LEN|  
  
## <a name="scalar-function-information"></a>标点函数信息  
 *InfoType*参数的以下值返回有关数据源和驱动程序支持的标量函数的信息。 有关标量函数的详细信息，请参阅附录[E：标点函数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)。  
  
|||  
|-|-|  
|SQL_CONVERT_FUNCTIONS|SQL_TIMEDATE_ADD_INTERVALS|  
|SQL_NUMERIC_FUNCTIONS|SQL_TIMEDATE_DIFF_INTERVALS|  
|SQL_STRING_FUNCTIONS|SQL_TIMEDATE_FUNCTIONS|  
|SQL_SYSTEM_FUNCTIONS||  
  
## <a name="conversion-information"></a>转换信息  
 *InfoType*参数的以下值返回 SQL 数据类型的列表，数据源可以使用**CONVERT**标量函数将指定的 SQL 数据类型转换为这些类型：  
  
|||  
|-|-|  
|SQL_CONVERT_BIGINT|SQL_CONVERT_LONGVARBINARY|  
|SQL_CONVERT_BINARY|SQL_CONVERT_LONGVARCHAR|  
|SQL_CONVERT_BIT|SQL_CONVERT_NUMERIC|  
|SQL_CONVERT_CHAR|SQL_CONVERT_REAL|  
|SQL_CONVERT_DATE|SQL_CONVERT_SMALLINT|  
|SQL_CONVERT_DECIMAL|SQL_CONVERT_TIME|  
|SQL_CONVERT_DOUBLE|SQL_CONVERT_TIMESTAMP|  
|SQL_CONVERT_FLOAT|SQL_CONVERT_TINYINT|  
|SQL_CONVERT_INTEGER|SQL_CONVERT_VARBINARY|  
|SQL_CONVERT_INTERVAL_YEAR_MONTH|SQL_CONVERT_VARCHAR|  
|SQL_CONVERT_INTERVAL_DAY_TIME||  
  
## <a name="information-types-added-for-odbc-3x"></a>为 ODBC 3.x 添加的信息类型  
 为 ODBC 3 *.x*添加了*InfoType*参数的以下值：  
  
|||  
|-|-|  
|SQL_ACTIVE_ENVIRONMENTS|SQL_DRIVER_AWARE_POOLING_SUPPORTED|  
|SQL_AGGREGATE_FUNCTIONS|SQL_DRIVER_HDESC|  
|SQL_ALTER_DOMAIN|SQL_DROP_ASSERTION|  
|SQL_ALTER_SCHEMA|SQL_DROP_CHARACTER_SET|  
|SQL_ANSI_SQL_DATETIME_LITERALS|SQL_DROP_COLLATION|  
|SQL_ASYNC_DBC_FUNCTIONS|SQL_DROP_DOMAIN|  
|SQL_ASYNC_MODE|SQL_DROP_SCHEMA|  
|SQL_ASYNC_NOTIFICATION|SQL_DROP_TABLE|  
|SQL_BATCH_ROW_COUNT|SQL_DROP_TRANSLATION|  
|SQL_BATCH_SUPPORT|SQL_DROP_VIEW|  
|SQL_CATALOG_NAME|SQL_DYNAMIC_CURSOR_ATTRIBUTES1|  
|SQL_COLLATION_SEQ|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
|SQL_CONVERT_INTERVAL_YEAR_MONTH|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|  
|SQL_CONVERT_INTERVAL_DAY_TIME|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
|SQL_CREATE_ASSERTION|SQL_INFO_SCHEMA_VIEWS|  
|SQL_CREATE_CHARACTER_SET|SQL_INSERT_STATEMENT|  
|SQL_CREATE_COLLATION|SQL_KEYSET_CURSOR_ATTRIBUTES1|  
|SQL_CREATE_DOMAIN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
|SQL_CREATE_SCHEMA|SQL_MAX_ASYNC_CONCURRENT_STATEMENTS|  
|SQL_CREATE_TABLE|SQL_MAX_IDENTIFIER_LEN|  
|SQL_CREATE_TRANSLATION|SQL_PARAM_ARRAY_ROW_COUNTS|  
|SQL_CURSOR_SENSITIVITY|SQL_PARAM_ARRAY_SELECTS|  
|SQL_DDL_INDEX|SQL_STATIC_CURSOR_ATTRIBUTES1|  
|SQL_DESCRIBE_PARAMETER|SQL_STATIC_CURSOR_ATTRIBUTES2|  
|SQL_DM_VER|SQL_XOPEN_CLI_YEAR|  
  
## <a name="information-types-renamed-for-odbc-3x"></a>为 ODBC 3.x 重命名的信息类型  
 *InfoType*参数的以下值已重命名为 ODBC 3 *.x*。  
  
 SQL_ACTIVE_CONNECTIONS  
 SQL_MAX_DRIVER_CONNECTIONS  
  
 SQL_ACTIVE_STATEMENTS  
 SQL_MAX_CONCURRENT_ACTIVITIES  
  
 SQL_MAX_OWNER_NAME_LEN  
 SQL_MAX_SCHEMA_NAME_LEN  
  
 SQL_MAX_QUALIFIER_NAME_LEN  
 SQL_MAX_CATALOG_NAME_LEN  
  
 SQL_ODBC_SQL_OPT_IEF  
 SQL_INTEGRITY  
  
 SQL_OWNER_TERM  
 SQL_SCHEMA_TERM  
  
 SQL_OWNER_USAGE  
 SQL_SCHEMA_USAGE  
  
 SQL_QUALIFIER_LOCATION  
 SQL_CATALOG_LOCATION  
  
 SQL_QUALIFIER_NAME_SEPARATOR  
 SQL_CATALOG_NAME_SEPARATOR  
  
 SQL_QUALIFIER_TERM  
 SQL_CATALOG_TERM  
  
 SQL_QUALIFIER_USAGE  
 SQL_CATALOG_USAGE  
  
## <a name="information-types-deprecated-in-odbc-3x"></a>在 ODBC 3.x 中弃用的信息类型  
 在 ODBC 3 *.x*中，已弃用*InfoType*参数的以下值。 ODBC 3 *.x*驱动程序必须继续支持这些信息类型，以便与 ODBC 2 *.x*应用程序向后兼容。 （有关这些类型的的详细信息，请参阅附录 G 中的[SQLGetInfo 支持](../../../odbc/reference/appendixes/sqlgetinfo-support.md)：向后兼容性的驱动程序指南。  
  
|||  
|-|-|  
|SQL_FETCH_DIRECTION|SQL_POS_OPERATIONS|  
|SQL_LOCK_TYPES|SQL_POSITIONED_STATEMENTS|  
|SQL_ODBC_API_CONFORMANCE|SQL_SCROLL_CONCURRENCY|  
|SQL_ODBC_SQL_CONFORMANCE|SQL_STATIC_SENSITIVITY|  
  
## <a name="information-type-descriptions"></a>信息类型描述  
 下表按字母顺序列出了每种信息类型、介绍其内容的 ODBC 版本及其说明。  
  
 SQL_ACCESSIBLE_PROCEDURES（ODBC 1.0）  
 字符串字符串："Y"，如果用户可以执行**SQL 程序**返回的所有过程;如果返回过程时可能返回用户无法执行，则为"N"。  
  
 SQL_ACCESSIBLE_TABLES（ODBC 1.0）  
 字符串字符串："Y"，**如果用户保证选择** **SQLTables**返回的所有表的权限;如果返回的表是用户无法访问的表，则为"N"。  
  
 SQL_ACTIVE_ENVIRONMENTS（ODBC 3.0）  
 指定驱动程序可以支持的最大活动环境数的 SQLUSMALLINT 值。 如果没有指定限制或限制未知，则此值设置为零。  
  
 SQL_AGGREGATE_FUNCTIONS（ODBC 3.0）  
 SQLUINTEGER 位掩码枚举对聚合函数的支持：  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 SQL-92 符合入门级的驱动程序将始终返回所有这些选项（如支持）。  
  
 SQL_ALTER_DOMAIN（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举**了在**SQL-92 中定义的 ALTER DOMAIN 语句中子句，数据源支持。 SQL-92 完全符合级别的驱动程序将始终返回所有位掩码。 返回值"0"表示不支持 ALTER **DOMAIN**语句。  
  
 必须支持此功能的 SQL-92 或 FIPS 一致性级别显示在每个位掩码旁边的括号中。  
  
 以下位掩码用于确定哪些子句受支持：  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = 支持添加域约束（完整级别）  
  
 SQL_AD_ADD_DOMAIN_DEFAULT \<= 更改\<域>>受支持的域默认子句（完整级别）  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION \<=>为命名域约束（中间级别）支持约束名称定义子句  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT \<= 支持>删除域约束子句（全级别）  
  
 SQL_AD_DROP_DOMAIN_DEFAULT \<= 更改\<域>删除域默认子句>支持（完整级别）  
  
 如果\<支持>添加域约束\<（设置SQL_AD_ADD_DOMAIN_CONSTRAINT位），以下位指定支持的约束属性>：  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE（全级别）SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE（全级别）SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED（全级别）SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE（全级别）  
  
 SQL_ALTER_TABLE（ODBC 2.0）  
 SQLUINTEGER 位掩码，枚举数据源支持的**ALTER TABLE**语句中子句。  
  
 必须支持此功能的 SQL-92 或 FIPS 一致性级别显示在每个位掩码旁边的括号中。  
  
 以下位掩码用于确定哪些子句受支持：  
  
 SQL_AT_ADD_COLUMN_COLLATION \<= 支持添加列>子句，具有指定列排序规则（完整级别）（ODBC 3.0）的功能  
  
 SQL_AT_ADD_COLUMN_DEFAULT \<= 支持添加列>子句，具有指定列默认值（FIPS 过渡级别）（ODBC 3.0）的功能  
  
 SQL_AT_ADD_COLUMN_SINGLE \<= 支持添加列>（FIPS 过渡级别）（ODBC 3.0）  
  
 SQL_AT_ADD_CONSTRAINT \<= 支持添加列>子句，具有指定列约束（FIPS 过渡级别）（ODBC 3.0）的功能  
  
 SQL_AT_ADD_TABLE_CONSTRAINT \<= 支持>项（FIPS过渡级别）（ODBC 3.0）添加表约束  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION \<=>为命名列和表约束（中间级别）（ODBC 3.0）支持约束名称定义  
  
 支持SQL_AT_DROP_COLUMN_CASCADE \<= 丢弃列> CASCADE（FIPS 过渡级别）（ODBC 3.0）  
  
 SQL_AT_DROP_COLUMN_DEFAULT \<= 更改\<列>删除列默认子句>支持（中级级别）（ODBC 3.0）  
  
 支持SQL_AT_DROP_COLUMN_RESTRICT \<= 下拉列>限制（FIPS 过渡级别）（ODBC 3.0）  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE （ODBC 3.0）  
  
 支持SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT \<=>约束的放置列（FIPS 过渡级别）（ODBC 3.0）  
  
 SQL_AT_SET_COLUMN_DEFAULT \<= 更改\<列>设置列默认子句>支持（中级级别）（ODBC 3.0）  
  
 如果支持指定列或表\<约束（设置SQL_AT_ADD_CONSTRAINT位），以下位将指定支持约束属性>：  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED（全级） （ODBC 3.0） SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE （全级别） （ODBC 3.0）SQL_AT_CONSTRAINT_DEFERRABLE（完整级别）（ODBC 3.0）SQL_AT_CONSTRAINT_NON_DEFERRABLE（全级）（ODBC 3.0）  
  
 SQL_ASYNC_DBC_FUNCTIONS （ODBC 3.8）  
 SQLUINTEGER 值，指示驱动程序是否可以在连接句柄上异步执行函数。  
  
 SQL_ASYNC_DBC_CAPABLE = 驱动程序可以异步执行连接函数。  
  
 SQL_ASYNC_DBC_NOT_CAPABLE = 驱动程序无法异步执行连接函数。  
  
 SQL_ASYNC_MODE（ODBC 3.0）  
 指示驱动程序中异步支持级别的 SQLUINTEGER 值：  
  
 SQL_AM_CONNECTION = 支持连接级异步执行。 与给定连接句柄关联的所有语句句柄都处于异步模式，或者所有语句句柄都处于同步模式。 连接上的语句句柄不能处于异步模式，而同一连接上的另一个语句句柄处于同步模式，反之亦然。  
  
 SQL_AM_STATEMENT = 支持语句级异步执行。 与连接句柄关联的某些语句句柄可能处于异步模式，而同一连接上的其他语句句柄处于同步模式。  
  
 不支持SQL_AM_NONE = 不支持异步模式。  
  
 SQL_ASYNC_NOTIFICATION  
 指示驱动程序是否支持异步通知的 SQLUINTEGER 值：  
  
-   **SQL_ASYNC_NOTIFICATION_CAPABLE**驱动程序支持异步执行通知。  
  
-   **SQL_ASYNC_NOTIFICATION_NOT_CAPABLE**驱动程序不支持异步执行通知。  
  
 ODBC 异步操作分为两类：连接级异步操作和语句级异步操作。  如果驱动程序返回SQL_ASYNC_NOTIFICATION_CAPABLE，它必须支持它可以通过异步执行的所有 API 的通知。  
  
 SQL_BATCH_ROW_COUNT （ODBC 3.0）  
 SQLUINTEGER 位掩码，用于枚举驱动程序相对于行计数的可用性的行为。 以下位掩码与信息类型一起使用：  
  
 SQL_BRC_ROLLED_UP = 连续插入、删除或更新语句的行计数汇总为一个。 如果未设置此位，则行计数可用于每个语句。  
  
 SQL_BRC_PROCEDURES = 在存储过程中执行批处理时，行计数（如果有）可用。 如果行计数可用，则它们可以汇总或单独可用，具体取决于SQL_BRC_ROLLED_UP位。  
  
 SQL_BRC_EXPLICIT = 当通过调用 SQLExecute 或**SQLExecDirect**直接执行批处理时**SQLExecDirect**，行计数（如果有）可用。 如果行计数可用，则它们可以汇总或单独可用，具体取决于SQL_BRC_ROLLED_UP位。  
  
 SQL_BATCH_SUPPORT （ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举驱动程序对批处理的支持。 以下位掩码用于确定支持哪个级别：  
  
 SQL_BS_SELECT_EXPLICIT = 驱动程序支持具有结果集生成语句的显式批处理。  
  
 SQL_BS_ROW_COUNT_EXPLICIT = 驱动程序支持具有行计数生成语句的显式批处理。  
  
 SQL_BS_SELECT_PROC = 驱动程序支持具有结果集生成语句的显式过程。  
  
 SQL_BS_ROW_COUNT_PROC = 驱动程序支持具有行计数生成语句的显式过程。  
  
 SQL_BOOKMARK_PERSISTENCE（ODBC 2.0）  
 SQLUINTEGER 位掩码，枚举书签持续存在的操作。  
  
 以下位掩码与标志一起使用，以确定书签保留的选项：  
  
 SQL_BP_CLOSE = 书签在应用程序使用SQL_CLOSE选项调用**SQLFreeStmt**后有效，或者**SQLCloseCursor**关闭与语句关联的游标。  
  
 SQL_BP_DELETE = 删除该行后，行的书签有效。  
  
 SQL_BP_DROP = 书签在应用程序调用**SQLFreeHandle**且*具有SQL_HANDLE_STMT的句柄类型*以删除语句后有效。  
  
 SQL_BP_TRANSACTION = 书签在应用程序提交或回滚事务后有效。  
  
 SQL_BP_UPDATE = 该行的书签在该行中的任何列（包括键列）更新后有效。  
  
 SQL_BP_OTHER_HSTMT = 与一个语句关联的书签可以与另一个语句一起使用。 除非指定SQL_BP_CLOSE或SQL_BP_DROP，否则第一个语句上的光标必须打开。  
  
 SQL_CATALOG_LOCATION（ODBC 2.0）  
 指示目录在限定表名称中的位置的 SQLUSMALLINT 值：  
  
 SQL_CL_STARTSQL_CL_END  
  
 例如，Xbase 驱动程序返回SQL_CL_START因为目录（目录）名称位于表名称的开头，如 [EMPDATA_EMP] 中所示。Dbf。 ORACLE 服务器驱动程序返回SQL_CL_END因为目录位于表名称的末尾，如 中ADMIN.EMP@EMPDATA。  
  
 SQL-92 完全符合级别的驱动程序将始终返回SQL_CL_START。 如果数据源不支持目录，则返回值 0。 要确定是否支持目录，应用程序使用SQL_CATALOG_NAME信息类型调用**SQLGetInfo。**  
  
 此*信息类型*已重命名为 ODBC 3.0 从 ODBC 2.0*信息类型*SQL_QUALIFIER_LOCATION。  
  
 SQL_CATALOG_NAME（ODBC 3.0）  
 字符串字符串："Y"，如果服务器支持目录名称，则不支持"N"。  
  
 SQL-92 完全符合级别的驱动程序将始终返回"Y"。  
  
 SQL_CATALOG_NAME_SEPARATOR（ODBC 1.0）  
 字符串：数据源定义为目录名称与目录名称之后或其后面的限定名称元素之间的分隔符的字符或字符。  
  
 如果数据源不支持目录，则返回空字符串。 要确定是否支持目录，应用程序使用SQL_CATALOG_NAME信息类型调用**SQLGetInfo。** SQL-92 完全符合级别的驱动程序将始终返回。  
  
 此*信息类型*已从 ODBC 2.0*信息类型*SQL_QUALIFIER_NAME_SEPARATOR重命名为 ODBC 3.0。  
  
 SQL_CATALOG_TERM（ODBC 1.0）  
 具有目录数据源供应商名称的字符串;例如，"数据库"或"目录"。 此字符串可以是上部、下部或混合大小写。  
  
 如果数据源不支持目录，则返回空字符串。 要确定是否支持目录，应用程序使用SQL_CATALOG_NAME信息类型调用**SQLGetInfo。** SQL-92 符合电平的驱动程序将始终返回"目录"。  
  
 此*信息类型*已从 ODBC 2.0*信息类型*SQL_QUALIFIER_TERM重命名为 ODBC 3.0。  
  
 SQL_CATALOG_USAGE（ODBC 2.0）  
 SQLUINTEGER 位掩码，枚举了可以使用目录的语句。  
  
 以下位掩码用于确定目录的使用位置：  
  
 SQL_CU_DML_STATEMENTS = 所有数据操作语言语句都支持目录：**选择**、**插入**、**更新**、**删除**等，如果支持，**请选择更新**并定位更新和删除语句。  
  
 SQL_CU_PROCEDURE_INVOCATION = ODBC 过程调用语句中支持目录。  
  
 SQL_CU_TABLE_DEFINITION = 所有表定义语句都支持目录：**创建表**、**创建视图**、**更改表****、DROP TABLE**和 DROP**视图**。  
  
 SQL_CU_INDEX_DEFINITION = 所有索引定义语句都支持目录：**创建索引**和**DROP INDEX**。  
  
 SQL_CU_PRIVILEGE_DEFINITION = 所有权限定义语句都支持目录 **：GRANT**和**REVOKE**。  
  
 如果数据源不支持目录，则返回值 0。 要确定是否支持目录，应用程序使用SQL_CATALOG_NAME信息类型调用**SQLGetInfo。** SQL-92 符合电平的驱动程序将始终返回具有所有这些位集的位掩码。  
  
 此*信息类型*已从 ODBC 2.0*信息类型*SQL_QUALIFIER_USAGE重命名为 ODBC 3.0。  
  
 SQL_COLLATION_SEQ（ODBC 3.0）  
 排序规则序列的名称。 这是一个字符串，指示此服务器的默认字符集的默认排序规则的名称（例如，ISO 8859-1'或 EBCDIC）。 如果未知，将返回一个空字符串。 SQL-92 符合电平的驱动程序将始终返回非空字符串。  
  
 SQL_COLUMN_ALIAS（ODBC 2.0）  
 字符串字符串："Y"，如果数据源支持列别名;如果数据源支持列别名，则为"Y";否则，"N"。  
  
 列别名是可以使用 AS 子句为选择列表中的列指定的替代名称。 SQL-92 符合入门级的驱动程序将始终返回"Y"。  
  
 SQL_CONCAT_NULL_BEHAVIOR（ODBC 1.0）  
 SQLUSMALLINT 值，指示数据源如何处理 NULL 值字符数据类型列与非 NULL 值字符数据类型列的串联：  
  
 SQL_CB_NULL = 结果为 NULL 值。  
  
 SQL_CB_NON_NULL = 结果是非 NULL 值列或列的串联。  
  
 SQL-92 符合入门级的驱动程序将始终返回SQL_CB_NULL。  
  
 SQL_CONVERT_BIGINTSQL_CONVERT_BINARYSQL_CONVERT_BITSQL_CONVERT_CHARSQL_CONVERT_GUIDSQL_CONVERT_DATESQL_CONVERT_DECIMALSQL_CONVERT_DOUBLESQL_CONVERT_FLOATSQL_CONVERT_INTEGERSQL_CONVERT_INTERVAL_YEAR_MONTHSQL_CONVERT_INTERVAL_DAY_TIMESQL_CONVERT_LONGVARBINARYSQL_CONVERT_LONGVARCHARSQL_CONVERT_NUMERICSQL_CONVERT_REALSQL_CONVERT_SMALLINTSQL_CONVERT_TIMESQL_CONVERT_TIMESTAMPSQL_CONVERT_TINYINTSQL_CONVERT_VARBINARYSQL_CONVERT_VARCHAR（ODBC 1.0）  
 SQLUINTEGER 位掩码。 位掩码指示数据源支持的转换，该函数具有**CONVERT**标量函数，用于*在 InfoType*中命名的类型的数据。 如果位掩码等于零，数据源不支持从命名类型的数据进行任何转换，包括转换为相同的数据类型。  
  
 例如，要确定数据源是否支持将SQL_INTEGER数据转换为SQL_BIGINT数据类型，应用程序使用SQL_CONVERT_INTEGER*的信息类型*调用**SQLGetInfo。** 应用程序对返回的位掩码和SQL_CVT_BIGINT执行**AND**操作。 如果生成的值为非零，则支持转换。  
  
 以下位掩码用于确定支持哪些转换：  
  
 SQL_CVT_BIGINT （ODBC 1.0） SQL_CVT_BINARY （ODBC 1.0） SQL_CVT_BIT （ODBC 1.0） SQL_CVT_GUID （ODBC 3.5） SQL_CVT_CHAR （ODBC 1.0） SQL_CVT_DATE （ODBC 1.0）SQL_CVT_DECIMAL （ODBC 1.0）SQL_CVT_DOUBLE （ODBC 1.0）SQL_CVT_FLOAT （ODBC 1.0）SQL_CVT_INTEGER （ODBC 1.0）SQL_CVT_INTERVAL_YEAR_MONTH （ODBC 3.0）SQL_CVT_INTERVAL_DAY_TIME （ODBC 3.0）SQL_CVT_LONGVARBINARY （ODBC 1.0）SQL_CVT_LONGVARCHAR （ODBC 1.0）SQL_CVT_NUMERIC （ODBC 1.0）SQL_CVT_REAL ODBC 1.0）SQL_CVT_SMALLINT （ODBC 1.0）SQL_CVT_TIME （ODBC 1.0）SQL_CVT_TIMESTAMP （ODBC 1.0）SQL_CVT_TINYINT （ODBC 1.0）SQL_CVT_VARBINARY （ODBC 1.0）SQL_CVT_VARCHAR （ODBC 1.0）  
  
 SQL_CONVERT_FUNCTIONS（ODBC 1.0）  
 SQLUINTEGER 位掩码，枚举驱动程序和相关数据源支持的标量转换函数。  
  
 以下位掩码用于确定支持哪些转换函数：  
  
 SQL_FN_CVT_CASTSQL_FN_CVT_CONVERT  
  
 SQL_CORRELATION_NAME（ODBC 1.0）  
 指示是否支持表关联名称的 SQLUSMALLINT 值：  
  
 SQL_CN_NONE = 不支持关联名称。  
  
 SQL_CN_DIFFERENT = 关联名称受支持，但必须不同于它们表示的表的名称。  
  
 SQL_CN_ANY = 关联名称受支持，可以是任何有效的用户定义的名称。  
  
 SQL-92 符合入门级的驱动程序将始终返回SQL_CN_ANY。  
  
 SQL_CREATE_ASSERTION（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举了**创建 ASSERTION**语句中子句，如 SQL-92 中定义，由数据源支持。  
  
 以下位掩码用于确定哪些子句受支持：  
  
 SQL_CA_CREATE_ASSERTION  
  
 如果支持显式指定约束属性的能力（请参阅SQL_ALTER_TABLE和SQL_CREATE_TABLE信息类型），则以下位指定受支持的约束属性：  
  
 SQL_CA_CONSTRAINT_INITIALLY_DEFERREDSQL_CA_CONSTRAINT_INITIALLY_IMMEDIATESQL_CA_CONSTRAINT_DEFERRABLESQL_CA_CONSTRAINT_NON_DEFERRABLE  
  
 SQL-92 完全符合级别的驱动程序将始终返回所有这些选项（如支持）。 返回值"0"表示不支持 CREATE **ASSERTION**语句。  
  
 SQL_CREATE_CHARACTER_SET（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举了在 SQL-92 中定义的**CREATE 字符集**语句中子句，数据源支持。  
  
 以下位掩码用于确定哪些子句受支持：  
  
 SQL_CCS_CREATE_CHARACTER_SETSQL_CCS_COLLATE_CLAUSESQL_CCS_LIMITED_COLLATION  
  
 SQL-92 完全符合级别的驱动程序将始终返回所有这些选项（如支持）。 返回值"0"表示不支持 CREATE**字符集**语句。  
  
 SQL_CREATE_COLLATION（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举了**创建拼贴**语句中子句，如 SQL-92 中定义，由数据源支持。  
  
 以下位掩码用于确定哪些子句受支持：  
  
 SQL_CCOL_CREATE_COLLATION  
  
 SQL-92 完全符合级别的驱动程序将始终返回此选项作为支持。 返回值"0"表示不支持 CREATE**拼贴**语句。  
  
 SQL_CREATE_DOMAIN（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举了 CREATE **DOMAIN**语句中的条款，如 SQL-92 中定义，由数据源支持。  
  
 以下位掩码用于确定哪些子句受支持：  
  
 SQL_CDO_CREATE_DOMAIN = 支持 CREATE DOMAIN 语句（中级级别）。  
  
 SQL_CDO_CONSTRAINT_NAME_DEFINITION \<= 命名域约束（中间级别）>支持约束名称定义。  
  
 以下位指定创建列约束的能力：SQL_CDO_DEFAULT = 支持指定域约束（中间级别）SQL_CDO_CONSTRAINT = 指定域默认值（中间级别）SQL_CDO_COLLATION = 支持指定域排序规则（完整级别）  
  
 如果支持指定域约束（SQL_CDO_DEFAULT设置），则以下位指定受支持的约束属性：  
  
 SQL_CDO_CONSTRAINT_INITIALLY_DEFERRED（全级别）SQL_CDO_CONSTRAINT_INITIALLY_IMMEDIATE（全级别）SQL_CDO_CONSTRAINT_DEFERRABLE（全级别）SQL_CDO_CONSTRAINT_NON_DEFERRABLE（全级）  
  
 返回值"0"表示不支持 CREATE **DOMAIN**语句。  
  
 SQL_CREATE_SCHEMA（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举了**创建 SCHEMA**语句中子句，如 SQL-92 中定义，由数据源支持。  
  
 以下位掩码用于确定哪些子句受支持：  
  
 SQL_CS_CREATE_SCHEMASQL_CS_AUTHORIZATIONSQL_CS_DEFAULT_CHARACTER_SET  
  
 SQL-92 符合级别的中间驱动程序将始终返回SQL_CS_CREATE_SCHEMA，并SQL_CS_AUTHORIZATION选项。 在 SQL-92 条目级别也必须支持这些语句，但不一定作为 SQL 语句。 SQL-92 完全符合级别的驱动程序将始终返回所有这些选项（如支持）。  
  
 SQL_CREATE_TABLE（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举了**创建表**语句中子句，如 SQL-92 中定义，由数据源支持。  
  
 必须支持此功能的 SQL-92 或 FIPS 一致性级别显示在每个位掩码旁边的括号中。  
  
 以下位掩码用于确定哪些子句受支持：  
  
 SQL_CT_CREATE_TABLE = 支持创建表语句。 （入门级）  
  
 SQL_CT_TABLE_CONSTRAINT = 支持指定表约束（FIPS 过渡级别）  
  
 SQL_CT_CONSTRAINT_NAME_DEFINITION =\<命名列和表约束（中间级别）支持约束名称定义>子句  
  
 以下位指定创建临时表的能力：  
  
 SQL_CT_COMMIT_PRESERVE = 删除的行在提交时保留。 （全级别）SQL_CT_COMMIT_DELETE = 删除的行在提交时被删除。 （全级别）SQL_CT_GLOBAL_TEMPORARY = 可以创建全局临时表。 （全级别）SQL_CT_LOCAL_TEMPORARY = 可以创建本地临时表。 （全级别）  
  
 以下位指定创建列约束的能力：  
  
 SQL_CT_COLUMN_CONSTRAINT = 支持指定列约束（FIPS 过渡级别）SQL_CT_COLUMN_DEFAULT = 支持指定列默认值（FIPS 过渡级别）SQL_CT_COLUMN_COLLATION = 支持指定列排序规则（完整级别）  
  
 如果支持指定列或表约束，则以下位指定受支持的约束属性：  
  
 SQL_CT_CONSTRAINT_INITIALLY_DEFERRED（全级别）SQL_CT_CONSTRAINT_INITIALLY_IMMEDIATE（全级别）SQL_CT_CONSTRAINT_DEFERRABLE（全级别）SQL_CT_CONSTRAINT_NON_DEFERRABLE（全级）  
  
 SQL_CREATE_TRANSLATION（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举了**创建转换**语句中子句，如 SQL-92 中定义，由数据源支持。  
  
 以下位掩码用于确定哪些子句受支持：  
  
 SQL_CTR_CREATE_TRANSLATION  
  
 SQL-92 完全符合级别的驱动程序将始终返回这些选项（如支持）。 返回值"0"表示不支持 CREATE**转换**语句。  
  
 SQL_CREATE_VIEW（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举了**创建视图**语句中子句，如 SQL-92 中定义，由数据源支持。  
  
 以下位掩码用于确定哪些子句受支持：  
  
 SQL_CV_CREATE_VIEWSQL_CV_CHECK_OPTIONSQL_CV_CASCADEDSQL_CV_LOCAL  
  
 返回值"0"表示不支持 CREATE **VIEW**语句。  
  
 SQL-92 符合入门级的驱动程序将始终返回SQL_CV_CREATE_VIEW，并SQL_CV_CHECK_OPTION选项（  
  
 SQL-92 完全符合级别的驱动程序将始终返回所有这些选项（如支持）。  
  
 SQL_CURSOR_COMMIT_BEHAVIOR（ODBC 1.0）  
 SQLUSMALLINT 值，指示**COMMIT**操作如何影响数据源中的游标和已准备的语句（提交事务时数据源的行为）。  
  
 此属性的值将反映下一个设置的当前状态：SQL_COPT_SS_PRESERVE_CURSORS。  
  
 SQL_CB_DELETE = 关闭游标并删除准备好的语句。 要再次使用游标，应用程序必须重新准备并重新执行语句。  
  
 SQL_CB_CLOSE = 关闭光标。 对于准备好的语句，应用程序可以在语句上调用**SQLExecute，** 而无需再次调用**SQLPrepare。** SQL ODBC 驱动程序的默认值为SQL_CB_CLOSE。 这意味着 SQL ODBC 驱动程序将在提交事务时关闭游标。  
  
 SQL_CB_PRESERVE = 将光标保留在与**COMMIT**操作之前相同的位置。 应用程序可以继续提取数据，也可以关闭游标并重新执行语句，而无需重新准备它。  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR（ODBC 1.0）  
 SQLUSMALLINT 值，指示**ROLLBACK**操作如何影响数据源中的游标和已准备的语句：  
  
 SQL_CB_DELETE = 关闭游标并删除准备好的语句。 要再次使用游标，应用程序必须重新准备并重新执行语句。  
  
 SQL_CB_CLOSE = 关闭光标。 对于准备好的语句，应用程序可以在语句上调用**SQLExecute，** 而无需再次调用**SQLPrepare。**  
  
 SQL_CB_PRESERVE = 将光标保留在与**ROLLBACK**操作之前相同的位置。 应用程序可以继续提取数据，也可以关闭游标并重新执行语句，而无需重新准备它。  
  
 SQL_CURSOR_SENSITIVITY （ODBC 3.0）  
 指示对游标敏感度的支持的 SQLUINTEGER 值：  
  
 SQL_INSENSITIVE = 语句句柄上的所有游标都显示结果集，而不反映同一事务中任何其他游标对它所做的任何更改。  
  
 SQL_UNSPECIFIED = 未指定语句句柄上的游标是否使同一事务中另一个游标对结果集所做的更改可见。 语句句柄上的光标可能使任何、某些或所有此类更改都变得可见。  
  
 SQL_SENSITIVE = 游标对同一事务中其他游标所做的更改很敏感。  
  
 SQL-92 符合入门级的驱动程序将始终返回支持SQL_UNSPECIFIED选项。  
  
 SQL-92 完全符合级别的驱动程序将始终返回支持SQL_INSENSITIVE选项。  
  
 SQL_DATA_SOURCE_NAME（ODBC 1.0）  
 连接期间使用的具有数据源名称的字符串。 如果应用程序称为**SQLConnect**，则这是*szDSN*参数的值。 如果应用程序称为**SQLDriverConnect**或**SQLBrowseConnect，** 则这是传递给驱动程序的连接字符串中的 DSN 关键字的值。 如果连接字符串不包含**DSN**关键字（例如，当它包含**DRIVER**关键字时），则这是一个空字符串。  
  
 SQL_DATA_SOURCE_READ_ONLY（ODBC 1.0）  
 字符串。 如果数据源设置为"只读"模式，"N"（如果是否则）。  
  
 此特性仅与数据源本身有关;它不是启用对数据源的驱动程序的特征。 读/写驱动程序可与只读的数据源一起使用。 如果驱动程序是只读的，则其所有数据源都必须为只读，并且必须返回SQL_DATA_SOURCE_READ_ONLY。  
  
 SQL_DATABASE_NAME（ODBC 1.0）  
 如果数据源定义了名为"数据库"的命名对象，则具有当前数据库名称的字符串。  
  
> [!NOTE]
>  在 ODBC 3 *.x*中，还可以通过调用**SQLGetConnectAttr**返回此*InfoType*返回的值，该*参数的属性*参数为SQL_ATTR_CURRENT_CATALOG。  
  
 SQL_DATETIME_LITERALS（ODBC 3.0）  
 一个 SQLUINTEGER 位掩码，枚举数据源支持的 SQL-92 约会时间文本。 请注意，这些是 SQL-92 规范中列出的日期时间文本，与 ODBC 定义的日期时间文本转义子句是分开的。 有关 ODBC 日期时间文本转义子句的详细信息，请参阅[日期、时间和时间戳文本](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)。  
  
 FIPS 过渡电平一致性驱动程序将始终返回位掩码中以下列表中位的"1"值。 值"0"表示不支持 SQL-92 约会时间文本。  
  
 以下位掩码用于确定支持哪些文本：  
  
 SQL_DL_SQL92_DATESQL_DL_SQL92_TIMESQL_DL_SQL92_TIMESTAMPSQL_DL_SQL92_INTERVAL_YEARSQL_DL_SQL92_INTERVAL_MONTHSQL_DL_SQL92_INTERVAL_DAYSQL_DL_SQL92_INTERVAL_HOURSQL_DL_SQL92_INTERVAL_MINUTESQL_DL_SQL92_INTERVAL_SECONDSQL_DL_SQL92_INTERVAL_YEAR_TO_MONTHSQL_DL_SQL92_INTERVAL_DAY_TO_HOUR  
  
 SQL_DL_SQL92_INTERVAL_DAY_TO_MINUTESQL_DL_SQL92_INTERVAL_DAY_TO_SECONDSQL_DL_SQL92_INTERVAL_HOUR_TO_MINUTESQL_DL_SQL92_INTERVAL_HOUR_TO_SECONDSQL_DL_SQL92_INTERVAL_MINUTE_TO_SECOND  
  
 SQL_DBMS_NAME（ODBC 1.0）  
 驱动程序访问的带有 DBMS 产品名称的字符串。  
  
 SQL_DBMS_VER（ODBC 1.0）  
 指示驱动程序访问的 DBMS 产品版本的字符串。 版本是窗体 [.]*，其中前两位数字是主要版本，后两位数字是次要版本，最后四位数字是发布版本。 驱动程序必须在此窗体中呈现 DBMS 产品版本，但还可以追加特定于 DBMS 的产品版本。 例如，"04.01.0000 Rdb 4.1"。  
  
 SQL_DDL_INDEX（ODBC 3.0）  
 指示对索引创建和删除的支持的 SQLUINTEGER 值：  
  
 SQL_DI_CREATE_INDEXSQL_DI_DROP_INDEX  
  
 SQL_DEFAULT_TXN_ISOLATION（ODBC 1.0）  
 一个 SQLUINTEGER 值，指示驱动程序或数据源支持的默认事务隔离级别，如果数据源不支持事务，则为零。 以下术语用于定义事务隔离级别：  
  
 **脏读**事务 1 更改一行。 事务 2 在事务 1 提交更改之前读取已更改的行。 如果事务 1 回滚更改，事务 2 将读取被认为从未存在的行。  
  
 **不可重复读取**事务 1 读取一行。 事务 2 更新或删除该行并提交此更改。 如果事务 1 尝试重读该行，它将接收不同的行值或发现该行已被删除。  
  
 **幻影**事务 1 读取一组满足某些搜索条件的行。 事务 2 生成一个或多个行（通过插入或更新）与搜索条件匹配。 如果事务 1 重新执行读取行的语句，它将接收一组不同的行。  
  
 如果数据源支持事务，驱动程序将返回以下位掩码之一：  
  
 SQL_TXN_READ_UNCOMMITTED = 脏读、不可重复读取和幻像是可能的。  
  
 SQL_TXN_READ_COMMITTED = 无法进行脏读。 不可重复读取和幻像是可能的。  
  
 SQL_TXN_REPEATABLE_READ = 无法进行脏读和不可重复读取。 幻影是可能的。  
  
 SQL_TXN_SERIALIZABLE = 事务是可序列化的。 可序列化事务不允许脏读、不可重复读取或幻象。  
  
 SQL_DESCRIBE_PARAMETER（ODBC 3.0）  
 字符字符串："Y"，如果参数可以描述;"N"，如果不是。  
  
 SQL-92 完全符合电平的驱动程序通常会返回"Y"，因为它将支持 DESCRIBE **INPUT**语句。 但是，由于这不能直接指定基础 SQL 支持，因此即使在 SQL-92 完全符合级别的驱动程序中，也不支持描述参数。  
  
 SQL_DM_VER（ODBC 3.0）  
 具有驱动程序管理器版本的字符串。 版本是表单 [.]*，其中：  
  
 第一组两位数字是主要 ODBC 版本，由常量SQL_SPEC_MAJOR给出。  
  
 第二组两位数字是次要 ODBC 版本，由常量SQL_SPEC_MINOR给出。  
  
 第三组四位数字是驱动程序管理器的主要内部版本号。  
  
 最后一组四位数字是驱动程序管理器的次要内部版本号。  
  
 Windows 7 驱动程序管理器版本是 03.80。 Windows 8 驱动程序管理器版本是 03.81。  
  
 SQL_DRIVER_AWARE_POOLING_SUPPORTED （ODBC 3.8）  
 一个 SQLUINTEGER 值，指示驱动程序是否支持驱动程序感知池。 （有关详细信息，请参阅[驱动程序感知连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。  
  
 SQL_DRIVER_AWARE_POOLING_CAPABLE表示驱动程序可以支持驱动程序感知池机制。  
  
 SQL_DRIVER_AWARE_POOLING_NOT_CAPABLE表示驱动程序不支持驱动程序感知池机制。  
  
 驱动程序不需要实现SQL_DRIVER_AWARE_POOLING_SUPPORTED，驾驶员管理器将不尊重驱动程序的返回值。  
  
 SQL_DRIVER_HDBCSQL_DRIVER_HENV（ODBC 1.0）  
 SQLULEN 值，驱动程序的环境句柄或连接句柄，由参数*InfoType*确定。  
  
 这些信息类型仅由驱动程序管理器实现。  
  
 SQL_DRIVER_HDESC（ODBC 3.0）  
 SQLULEN 值，驱动程序的描述符句柄由驱动程序管理器的描述符句柄确定，必须在\**应用程序中的 InfoValuePtr*中的输入传递该值。 在这种情况下 *，InfoValuePtr*既是输入参数，也是输出参数。 在\**InfoValuePtr*中传递的输入描述符句柄必须在*ConnectHandle*上显式或隐式分配。  
  
 应用程序应在使用此信息类型调用**SQLGetInfo**之前复制驱动程序管理器的描述符句柄，以确保该句柄不会在输出时覆盖。  
  
 此信息类型仅由驱动程序管理器实现。  
  
 SQL_DRIVER_HLIB（ODBC 2.0）  
 SQLULEN 值，加载库中*的 hinst*在 Microsoft Windows 操作系统上加载驱动程序 DLL 或在另一个操作系统上加载驱动程序 DLL 时返回到驱动程序管理器。 该句柄仅对**SQLGetInfo**调用中指定的连接句柄有效。  
  
 此信息类型仅由驱动程序管理器实现。  
  
 SQL_DRIVER_HSTMT（ODBC 1.0）  
 SQLULEN 值，驱动程序语句句柄由驱动程序管理器语句句柄确定，必须在\**应用程序中的 InfoValuePtr*中的输入传递该值。 在这种情况下 *，InfoValuePtr*既是输入参数，也是输出参数。 \**在 InfoValuePtr*中传递的输入语句句柄必须在参数*ConnectHandle*上分配。  
  
 应用程序应在使用此信息类型调用**SQLGetInfo**之前复制驱动程序管理器的语句句柄，以确保该句柄不会在输出时被覆盖。  
  
 此信息类型仅由驱动程序管理器实现。  
  
 SQL_DRIVER_NAME（ODBC 1.0）  
 具有用于访问数据源的驱动程序的文件名的字符串。  
  
 SQL_DRIVER_ODBC_VER（ODBC 2.0）  
 具有驱动程序支持的 ODBC 版本的字符串。 版本是窗体 #.#，其中前两位数字是主要版本，后两位数字是次要版本。 SQL_SPEC_MAJOR和SQL_SPEC_MINOR定义主要版本号和次要版本号。 对于本手册中描述的 ODBC 版本，这些版本为 3 和 0，驱动程序应返回"03.00"。  
  
 ODBC 驱动程序管理器不会修改 SQLGetInfo（SQL_DRIVER_ODBC_VER） 的返回值，以保持现有应用程序的向后兼容性。 驱动程序指定将返回的值。 但是，当应用程序调用**SQLSetEnvAttr**将SQL_ATTR_ODBC_VERSION设置为 3.8 时，支持 C 数据类型扩展性的驱动程序必须返回 3.8（或更高）。 有关详细信息，请参阅[ODBC 中的 C 数据类型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
 SQL_DRIVER_VER（ODBC 1.0）  
 具有驱动程序版本和可选的驱动程序说明的字符串。 至少，版本是窗体 [.]*，其中前两位数字是主要版本，接下来的两位数字是次要版本，最后四位数字是发布版本。  
  
 SQL_DROP_ASSERTION（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举在 SQL-92 中定义的**DROP ASSERTION**语句中子句，数据源支持。  
  
 以下位掩码用于确定哪些子句受支持：  
  
 SQL_DA_DROP_ASSERTION  
  
 SQL-92 完全符合级别的驱动程序将始终返回此选项作为支持。  
  
 SQL_DROP_CHARACTER_SET（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举在 SQL-92 中定义的**DROP 字符集**语句中子句，数据源支持。  
  
 以下位掩码用于确定哪些子句受支持：  
  
 SQL_DCS_DROP_CHARACTER_SET  
  
 SQL-92 完全符合级别的驱动程序将始终返回此选项作为支持。  
  
 SQL_DROP_COLLATION（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举在 SQL-92 中定义的**DROP COLLATION**语句中子句，数据源支持。  
  
 以下位掩码用于确定哪些子句受支持：  
  
 SQL_DC_DROP_COLLATION  
  
 SQL-92 完全符合级别的驱动程序将始终返回此选项作为支持。  
  
 SQL_DROP_DOMAIN（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举**DROP DOMAIN**语句中子句，如 SQL-92 中定义，由数据源支持。  
  
 以下位掩码用于确定哪些子句受支持：  
  
 SQL_DD_DROP_DOMAINSQL_DD_CASCADESQL_DD_RESTRICT  
  
 SQL-92 中间级别一致性驱动程序将始终返回所有这些选项（如支持）。  
  
 SQL_DROP_SCHEMA（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举**DROP SCHEMA**语句中子句，如 SQL-92 中定义，由数据源支持。  
  
 以下位掩码用于确定哪些子句受支持：  
  
 SQL_DS_DROP_SCHEMASQL_DS_CASCADESQL_DS_RESTRICT  
  
 SQL-92 中间级别一致性驱动程序将始终返回所有这些选项（如支持）。  
  
 SQL_DROP_TABLE（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举**DROP TABLE**语句中子句，如 SQL-92 中定义，由数据源支持。  
  
 以下位掩码用于确定哪些子句受支持：  
  
 SQL_DT_DROP_TABLESQL_DT_CASCADESQL_DT_RESTRICT  
  
 FIPS 过渡电平符合性驱动程序将始终返回支持的所有这些选项。  
  
 SQL_DROP_TRANSLATION（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举**DROP 转换**语句中子句，如 SQL-92 中定义，由数据源支持。  
  
 以下位掩码用于确定哪些子句受支持：  
  
 SQL_DTR_DROP_TRANSLATION  
  
 SQL-92 完全符合级别的驱动程序将始终返回此选项作为支持。  
  
 SQL_DROP_VIEW（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举**DROP VIEW**语句中子句，如 SQL-92 中定义，由数据源支持。  
  
 以下位掩码用于确定哪些子句受支持：  
  
 SQL_DV_DROP_VIEWSQL_DV_CASCADESQL_DV_RESTRICT  
  
 FIPS 过渡电平符合性驱动程序将始终返回支持的所有这些选项。  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES1（ODBC 3.0）  
 一个 SQLUINTEGER 位掩码，用于描述驱动程序支持的动态游标的属性。 此位掩码包含属性的第一个子集;对于第二个子集，请参阅SQL_DYNAMIC_CURSOR_ATTRIBUTES2。  
  
 以下位掩码用于确定哪些属性受支持：  
  
 SQL_CA1_NEXT = 当游标是动态游标时，对**SQLFetchScroll**的调用中支持SQL_FETCH_NEXT的*提取方向*参数。  
  
 SQL_CA1_ABSOLUTE = 当游标是动态游标时，对**SQLFetchScroll**的调用中支持 SQL_FETCH_FIRST、SQL_FETCH_LAST和SQL_FETCH_ABSOLUTE的*Fetch 方向*参数。 （要提取的行集与当前游标位置无关。  
  
 SQL_CA1_RELATIVE = 当游标是动态游标时，对**SQLFetchScroll**的调用中支持SQL_FETCH_PRIOR和SQL_FETCH_RELATIVE的*Fetch 方向*参数。 （要提取的行集取决于当前光标位置。 请注意，这与SQL_FETCH_NEXT分开，因为在仅转发游标中，仅支持SQL_FETCH_NEXT。  
  
 SQL_CA1_BOOKMARK = 当游标是动态游标时，对**SQLFetchScroll**的调用中支持SQL_FETCH_BOOKMARK的*提取方向*参数。  
  
 SQL_CA1_LOCK_EXCLUSIVE = 当游标是动态游标时，对**SQLSetPos**的调用中支持 SQL_LOCK_EXCLUSIVE的*LockType*参数。  
  
 SQL_CA1_LOCK_NO_CHANGE = 当游标是动态游标时，对**SQLSetPos**的调用中支持 SQL_LOCK_NO_CHANGE的*LockType*参数。  
  
 SQL_CA1_LOCK_UNLOCK = 当游标是动态游标时，对**SQLSetPos**的调用中支持 SQL_LOCK_UNLOCK的*LockType*参数。  
  
 SQL_CA1_POS_POSITION = 当游标是动态游标时，对**SQLSetPos**的调用中支持SQL_POSITION*的操作*参数。  
  
 SQL_CA1_POS_UPDATE = 当游标是动态游标时，对**SQLSetPos**的调用中支持SQL_UPDATE*的操作*参数。  
  
 SQL_CA1_POS_DELETE = 当游标是动态游标时，对**SQLSetPos**的调用中支持SQL_DELETE*的操作*参数。  
  
 SQL_CA1_POS_REFRESH = 当游标是动态游标时，对**SQLSetPos**的调用中支持SQL_REFRESH*的操作*参数。  
  
 SQL_CA1_POSITIONED_UPDATE = 当游标是动态游标时，支持 SQL 语句的更新。 （SQL-92 符合入门级的驱动程序将始终返回此选项作为支持。  
  
 SQL_CA1_POSITIONED_DELETE = 当游标是动态游标时，支持 SQL 语句的删除。 （SQL-92 符合入门级的驱动程序将始终返回此选项作为支持。  
  
 SQL_CA1_SELECT_FOR_UPDATE = 当游标是动态游标时，支持选择更新 SQL 语句。 （SQL-92 符合入门级的驱动程序将始终返回此选项作为支持。  
  
 SQL_CA1_BULK_ADD = 当游标是动态游标时，对**SQLBulk 操作**的调用中支持SQL_ADD*的操作*参数。  
  
 SQL_CA1_BULK_UPDATE_BY_BOOKMARK = 当游标是动态游标时，对**SQLBulk 操作**的调用支持SQL_UPDATE_BY_BOOKMARK*的操作*参数。  
  
 SQL_CA1_BULK_DELETE_BY_BOOKMARK = 当游标是动态游标时，对**SQLBulk 操作**的调用中支持SQL_DELETE_BY_BOOKMARK*的操作*参数。  
  
 SQL_CA1_BULK_FETCH_BY_BOOKMARK = 当游标是动态游标时，对**SQLBulk 操作**的调用中支持SQL_FETCH_BY_BOOKMARK*的操作*参数。  
  
 SQL-92 中间级别一致性驱动程序通常会返回支持SQL_CA1_NEXT、SQL_CA1_ABSOLUTE 和SQL_CA1_RELATIVE选项，因为它支持通过嵌入式 SQL FETCH 语句滚动游标。 但是，由于这不能直接确定基础 SQL 支持，因此即使对于 SQL-92 符合级别的驱动程序，也不支持可滚动游标。  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES2（ODBC 3.0）  
 一个 SQLUINTEGER 位掩码，用于描述驱动程序支持的动态游标的属性。 此位掩码包含属性的第二个子集;有关第一个子集，请参阅SQL_DYNAMIC_CURSOR_ATTRIBUTES1。  
  
 以下位掩码用于确定哪些属性受支持：  
  
 SQL_CA2_READ_ONLY_CONCURRENCY = 支持只读动态游标，不允许更新。 （可以SQL_CONCUR_READ_ONLY动态游标SQL_ATTR_CONCURRENCY语句属性）。  
  
 SQL_CA2_LOCK_CONCURRENCY = 支持使用足够确保可以更新行的最低水平的动态游标。 （可以SQL_CONCUR_LOCK动态游标SQL_ATTR_CONCURRENCY语句属性。这些锁必须与SQL_ATTR_TXN_ISOLATION连接属性设置的事务隔离级别一致。  
  
 SQL_CA2_OPT_ROWVER_CONCURRENCY = 支持使用比较行版本的乐观并发控件的动态游标。 （可以SQL_CONCUR_ROWVERSQL_ATTR_CONCURRENCY语句属性。  
  
 SQL_CA2_OPT_VALUES_CONCURRENCY = 支持使用乐观并发控件比较值的动态游标。 （可以SQL_CONCUR_VALUESSQL_ATTR_CONCURRENCY语句属性。  
  
 SQL_CA2_SENSITIVITY_ADDITIONS = 添加的行对动态游标可见;光标可以滚动到这些行。 （将这些行添加到游标的位置与驱动程序相关。  
  
 SQL_CA2_SENSITIVITY_DELETIONS = 已删除的行不再可用于动态游标，并且不会在结果集中留下"孔";动态光标从已删除的行滚动后，无法返回到该行。  
  
 SQL_CA2_SENSITIVITY_UPDATES = 对行的更新对动态游标可见;如果动态游标从中滚动并返回到更新的行，则游标返回的数据是更新的数据，而不是原始数据。  
  
 SQL_CA2_MAX_ROWS_SELECT = 当游标是动态游标时，SQL_ATTR_MAX_ROWS语句属性会影响**SELECT**语句。  
  
 SQL_CA2_MAX_ROWS_INSERT = 当游标是动态游标时，SQL_ATTR_MAX_ROWS语句属性会影响**INSERT**语句。  
  
 SQL_CA2_MAX_ROWS_DELETE = 当游标是动态游标时，SQL_ATTR_MAX_ROWS语句属性会影响**DELETE**语句。  
  
 SQL_CA2_MAX_ROWS_UPDATE = 当游标是动态游标时，SQL_ATTR_MAX_ROWS语句属性会影响**UPDATE**语句。  
  
 SQL_CA2_MAX_ROWS_CATALOG = 当游标是动态游标时，SQL_ATTR_MAX_ROWS语句属性会影响**CATALOG**结果集。  
  
 SQL_CA2_MAX_ROWS_AFFECTS_ALL = 当游标是动态游标时，SQL_ATTR_MAX_ROWS语句属性会影响**CATALOG****SELECT****SELECT、INSERT、DELETE**和**UPDATE**语句以及 CATALOG 结果集。 **DELETE**  
  
 SQL_CA2_CRC_EXACT = 当光标是动态光标时，SQL_DIAG_CURSOR_ROW_COUNT诊断字段中提供准确的行计数。  
  
 SQL_CA2_CRC_APPROXIMATE = 当光标是动态光标时，SQL_DIAG_CURSOR_ROW_COUNT诊断字段中有近似行计数可用。  
  
 SQL_CA2_SIMULATE_NON_UNIQUE = 驱动程序不保证当光标是动态游标时，模拟定位更新或删除语句仅影响一行;保证这是应用程序的责任。 （如果语句影响多行 **，SQLExecute**或**SQLExecDirect**将返回 SQLSTATE 01001 [Cursor 操作冲突]。要设置此行为，应用程序调用**SQLSetStmtAttr，SQL_ATTR_SIMULATE_CURSOR**属性设置为SQL_SC_NON_UNIQUE。  
  
 SQL_CA2_SIMULATE_TRY_UNIQUE = 驱动程序尝试保证当光标是动态游标时，模拟定位更新或删除语句仅影响一行。 驱动程序始终执行此类语句，即使它们可能会影响多个行，例如没有唯一键时。 （如果语句影响多行 **，SQLExecute**或**SQLExecDirect**将返回 SQLSTATE 01001 [Cursor 操作冲突]。要设置此行为，应用程序将**SQLSetStmtAttr**调用，SQL_ATTR_SIMULATE_CURSOR属性设置为SQL_SC_TRY_UNIQUE。  
  
 SQL_CA2_SIMULATE_UNIQUE = 驱动程序保证当光标是动态游标时，模拟定位更新或删除语句将仅影响一行。 如果驱动程序无法保证给定语句的此操作 **，SQLExecDirect**或**SQLPrepare**返回 SQLSTATE 01001（Cursor 操作冲突）。 要设置此行为，应用程序调用**SQLSetStmtAttr，SQL_ATTR_SIMULATE_CURSOR**属性设置为SQL_SC_UNIQUE。  
  
 SQL_EXPRESSIONS_IN_ORDERBY（ODBC 1.0）  
 字符串：如果数据源支持 ORDER BY 列表中的表达式，则为"Y";如果数据源支持**ORDER BY**列表中的表达式，则为"Y";"N"，如果它没有。  
  
 SQL_FILE_USAGE（ODBC 2.0）  
 SQLUSMALLINT 值，指示单层驱动程序如何直接处理数据源中的文件：  
  
 SQL_FILE_NOT_SUPPORTED = 驱动程序不是单层驱动程序。 例如，ORACLE 驱动程序是双层驱动程序。  
  
 SQL_FILE_TABLE = 单层驱动程序将数据源中的文件视为表。 例如，Xbase 驱动程序将每个 Xbase 文件视为表。  
  
 SQL_FILE_CATALOG = 单层驱动程序将数据源中的文件视为目录。 例如，Microsoft Access 驱动程序将每个 Microsoft Access 文件视为一个完整的数据库。  
  
 应用程序可能用它来确定用户如何选择数据。 例如，Xbase 用户通常认为数据存储在文件中，而 ORACLE 和 Microsoft Access 用户通常认为数据存储在表中。  
  
 当用户选择 Xbase 数据源时，应用程序可以显示 Windows 文件打开通用对话框;当用户选择 Xbase 数据源时，应用程序可以显示"Windows**文件打开**"通用对话框。当用户选择 Microsoft Access 或 ORACLE 数据源时，应用程序可以显示自定义**选择表**对话框。  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1（ODBC 3.0）  
 一个 SQLUINTEGER 位掩码，用于描述驱动程序支持的仅转发游标的属性。 此位掩码包含属性的第一个子集;对于第二个子集，请参阅SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2。  
  
 以下位掩码用于确定哪些属性受支持：  
  
 SQL_CA1_NEXTSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 有关这些位掩码的说明，请参阅SQL_DYNAMIC_CURSOR_ATTRIBUTES1（并在说明中用"仅前进游标"代替"动态光标"）。  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2（ODBC 3.0）  
 一个 SQLUINTEGER 位掩码，用于描述驱动程序支持的仅转发游标的属性。 此位掩码包含属性的第二个子集;对于第一个子集，请参阅SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1。  
  
 以下位掩码用于确定哪些属性受支持：  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 有关这些位掩码的说明，请参阅SQL_DYNAMIC_CURSOR_ATTRIBUTES2（并在说明中用"仅前进光标"代替"动态光标"）。  
  
 SQL_GETDATA_EXTENSIONS（ODBC 2.0）  
 SQLUINTEGER 位掩码枚举到**SQLGetData**上。  
  
 以下位掩码与标志一起使用，以确定驱动程序支持**SQLGetData**的通用扩展：  
  
 SQL_GD_ANY_COLUMN = **SQLGetData**可以调用任何未绑定列，包括最后一个绑定列之前的列。 请注意，除非还返回SQL_GD_ANY_ORDER，否则必须按升序按列数的顺序调用列。  
  
 SQL_GD_ANY_ORDER = **SQLGetData**可以按任意顺序调用未绑定列。 请注意，除非还返回SQL_GD_ANY_COLUMN，否则只能为最后一个绑定列之后的列调用**SQLGetData。**  
  
 SQL_GD_BLOCK = **SQLGetData**在使用**SQLSetPos**定位到该行后，可以调用数据块中的任何行中的未绑定列（其中行集大小大于 1） 的数据。  
  
 SQL_GD_BOUND = 除了未绑定列之外，还可以为绑定列调用**SQLGetData。** 驱动程序无法返回此值，除非它还返回SQL_GD_ANY_COLUMN。  
  
 可以调用 SQL_GD_OUTPUT_PARAMS = **SQLGetData**来返回输出参数值。 有关详细信息，请参阅使用[SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
 **SQLGetData**需要仅从最后一个绑定列之后发生的未绑定列返回数据，按增加列数的顺序调用，并且不在行块中的行中。  
  
 如果驱动程序支持书签（固定长度或可变长度），则必须支持在列 0 上调用**SQLGetData。** 无论驱动程序返回什么来调用**SQLGetInfo，SQL_GETDATA_EXTENSIONS** *InfoType*都需要什么，都需要这种支持。  
  
 SQL_GROUP_BY（ODBC 2.0）  
 SQLUSMALLINT 值，用于指定**GROUP BY**子句中的列与选择列表中的非聚合列之间的关系：  
  
 SQL_GB_COLLATE = 可以在每个分组列的末尾指定**COLLATE**子句。 （ODBC 3.0）  
  
 不支持SQL_GB_NOT_SUPPORTED =**组 BY**子句。 （ODBC 2.0）  
  
 SQL_GB_GROUP_BY_EQUALS_SELECT = **GROUP BY**子句必须包含选择列表中的所有非聚合列。 它不能包含任何其他列。 例如，**按部门从员工组中选择部门、最大值（工资）。** （ODBC 2.0）  
  
 SQL_GB_GROUP_BY_CONTAINS_SELECT = **GROUP BY**子句必须包含选择列表中的所有非聚合列。 它可以包含不在选择列表中的列。 例如，**按部门、年龄从员工组中选择部门、最高（工资）。** （ODBC 2.0）  
  
 SQL_GB_NO_RELATION = GROUP **BY**子句中的列和选择列表中的列不相关。 选择列表中非分组的非聚合列的含义与数据源相关。 例如，**按部门、年龄从员工组中选择部门、薪酬**。 （ODBC 2.0）  
  
 SQL-92 符合入门级的驱动程序将始终返回支持SQL_GB_GROUP_BY_EQUALS_SELECT选项。 SQL-92 完全符合级别的驱动程序将始终返回支持SQL_GB_COLLATE选项。 如果没有支持任何选项，数据源不支持**GROUP BY**子句。  
  
 SQL_IDENTIFIER_CASE（ODBC 1.0）  
 SQLUSMALLINT 值如下所示：  
  
 SQL_IC_UPPER = SQL 中的标识符不区分大小写，存储在系统目录中的大写中。  
  
 SQL_IC_LOWER = SQL 中的标识符不区分大小写，存储在系统目录中的小写中。  
  
 SQL_IC_SENSITIVE = SQL 中的标识符区分大小写，存储在系统目录中的混合情况下。  
  
 SQL_IC_MIXED = SQL 中的标识符不区分大小写，存储在系统目录中的混合情况下。  
  
 由于 SQL-92 中的标识符从不区分大小写，因此严格遵循 SQL-92（任何级别）的驱动程序永远不会返回受支持的SQL_IC_SENSITIVE选项。  
  
 SQL_IDENTIFIER_QUOTE_CHAR（ODBC 1.0）  
 用作 SQL 语句中引用（分隔）标识符的开始和结束分隔符的字符串。 （作为 ODBC 函数的参数传递给的标识符不必引用。如果数据源不支持引号标识符，则返回空白。  
  
 当连接属性SQL_ATTR_METADATA_ID设置为SQL_TRUE时，此字符串还可用于引用目录函数参数。  
  
 由于 SQL-92 中的标识符引号字符是双引号 （），因此严格遵守 SQL-92 的驱动程序将始终返回双引号字符。  
  
 SQL_INDEX_KEYWORDS（ODBC 3.0）  
 SQLUINTEGER 位掩码，用于枚举驱动程序支持的 CREATE INDEX 语句中的关键字：  
  
 SQL_IK_NONE = 不支持任何关键字。  
  
 SQL_IK_ASC = 支持 ASC 关键字。  
  
 SQL_IK_DESC = 支持 DESC 关键字。  
  
 SQL_IK_ALL = 支持所有关键字。  
  
 要查看是否支持 CREATE INDEX 语句，应用程序使用SQL_DLL_INDEX信息类型调用**SQLGetInfo。**  
  
 SQL_INFO_SCHEMA_VIEWS（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举驱动程序支持的INFORMATION_SCHEMA中的视图。 INFORMATION_SCHEMA中的视图和内容在 SQL-92 中定义。  
  
 必须支持此功能的 SQL-92 或 FIPS 一致性级别显示在每个位掩码旁边的括号中。  
  
 以下位掩码用于确定支持哪些视图：  
  
 SQL_ISV_ASSERTIONS = 标识由给定用户拥有的目录断言。 （全级别）  
  
 SQL_ISV_CHARACTER_SETS = 标识给定用户可以访问的目录的字符集。 （中级）  
  
 SQL_ISV_CHECK_CONSTRAINTS = 标识给定用户拥有的 CHECK 约束。 （中级）  
  
 SQL_ISV_COLLATIONS = 标识给定用户可以访问的目录的字符排序规则。 （全级别）  
  
 SQL_ISV_COLUMN_DOMAIN_USAGE = 标识目录的列，这些列取决于目录中定义的域，并且由给定用户拥有。 （中级）  
  
 SQL_ISV_COLUMN_PRIVILEGES = 标识给定用户可用或授予的持久表列上的权限。 （FIPS 过渡级别）  
  
 SQL_ISV_COLUMNS = 标识给定用户可以访问的持久表的列。 （FIPS 过渡级别）  
  
 SQL_ISV_CONSTRAINT_COLUMN_USAGE = 与CONSTRAINT_TABLE_USAGE视图类似，列标识给定用户拥有的各种约束。 （中级）  
  
 SQL_ISV_CONSTRAINT_TABLE_USAGE = 标识约束（引用、唯一和断言）使用的表，并且由给定用户拥有。 （中级）  
  
 SQL_ISV_DOMAIN_CONSTRAINTS = 标识给定用户可以访问的域约束（目录中的域）。 （中级）  
  
 SQL_ISV_DOMAINS = 标识目录中定义的用户可以访问的域。 （中级）  
  
 SQL_ISV_KEY_COLUMN_USAGE = 标识目录中定义的由给定用户作为键约束的列。 （中级）  
  
 SQL_ISV_REFERENTIAL_CONSTRAINTS = 标识给定用户拥有的引用约束。 （中级）  
  
 SQL_ISV_SCHEMATA = 标识给定用户拥有的架构。 （中级）  
  
 SQL_ISV_SQL_LANGUAGES = 标识 SQL 实现支持的 SQL 一致性级别、选项和方言。 （中级）  
  
 SQL_ISV_TABLE_CONSTRAINTS = 标识给定用户拥有的表约束。 （中级）  
  
 SQL_ISV_TABLE_PRIVILEGES = 标识给定用户可用或授予的持久表上的权限。 （FIPS 过渡级别）  
  
 SQL_ISV_TABLES = 标识目录中定义的持久表，该表可以由给定用户访问。 （FIPS 过渡级别）  
  
 SQL_ISV_TRANSLATIONS = 标识给定用户可以访问的目录的字符转换。 （全级别）  
  
 SQL_ISV_USAGE_PRIVILEGES = 标识给定用户可用或拥有的目录对象的 USAGE 权限。 （FIPS 过渡级别）  
  
 SQL_ISV_VIEW_COLUMN_USAGE = 标识给定用户拥有的目录视图所依赖的列。 （中级）  
  
 SQL_ISV_VIEW_TABLE_USAGE = 标识给定用户拥有的目录视图所依赖的表。 （中级）  
  
 SQL_ISV_VIEWS = 标识此目录中定义的由给定用户可以访问的已查看的表。 （FIPS 过渡级别）  
  
 SQL_INSERT_STATEMENT（ODBC 3.0）  
 指示对**插入**语句支持的 SQLUINTEGER 位掩码：  
  
 SQL_IS_INSERT_LITERALS  
  
 SQL_IS_INSERT_SEARCHED  
  
 SQL_IS_SELECT_INTO  
  
 SQL-92 符合入门级的驱动程序将始终返回所有这些选项（如支持）。  
  
 SQL_INTEGRITY（ODBC 1.0）  
 字符串：如果数据源支持完整性增强工具，则为"Y";"N"，如果它没有。  
  
 此*信息类型*已从 ODBC 2.0*信息类型*SQL_ODBC_SQL_OPT_IEF重命名为 ODBC 3.0。  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES1（ODBC 3.0）  
 一个 SQLUINTEGER 位掩码，用于描述驱动程序支持的键集游标的属性。 此位掩码包含属性的第一个子集;对于第二个子集，请参阅SQL_KEYSET_CURSOR_ATTRIBUTES2。  
  
 以下位掩码用于确定哪些属性受支持：  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 有关这些位掩码的说明，请参阅SQL_DYNAMIC_CURSOR_ATTRIBUTES1（并在说明中用"键集驱动游标"代替"动态游标"）。  
  
 SQL-92 中间级别一致性驱动程序通常会返回SQL_CA1_NEXT、SQL_CA1_ABSOLUTE和SQL_CA1_RELATIVE选项（如支持），因为驱动程序支持通过嵌入式 SQL FETCH 语句滚动游标。 但是，由于这不能直接确定基础 SQL 支持，因此即使对于 SQL-92 符合级别的驱动程序，也不支持可滚动游标。  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES2（ODBC 3.0）  
 一个 SQLUINTEGER 位掩码，用于描述驱动程序支持的键集游标的属性。 此位掩码包含属性的第二个子集;有关第一个子集，请参阅SQL_KEYSET_CURSOR_ATTRIBUTES1。  
  
 以下位掩码用于确定哪些属性受支持：  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 有关这些位掩码的说明，请参阅SQL_DYNAMIC_CURSOR_ATTRIBUTES1（并在说明中用"键集驱动游标"代替"动态游标"）。  
  
 SQL_KEYWORDS（ODBC 2.0）  
 包含所有数据源特定关键字的逗号分隔列表的字符串。 此列表不包含特定于 ODBC 的关键字或数据源和 ODBC 使用的关键字。 此列表表示所有保留的关键字;可互操作的应用程序不应在对象名称中使用这些单词。  
  
 有关 ODBC 关键字的列表，请参阅附录 C 中的[保留关键字](../../../odbc/reference/appendixes/reserved-keywords.md)[：SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。 **#define**值SQL_ODBC_KEYWORDS包含 ODBC 关键字的逗号分隔列表。  
  
 附录 C：SQL 语法  
  
 SQL_LIKE_ESCAPE_CLAUSE（ODBC 2.0）  
 字符串：如果数据源支持百分比字符 （%） 的转义字符，"Y"和下划线字符 （*） 在**LIKE**谓词和驱动程序支持 ODBC 语法定义**LIKE**谓词转义字符;否则为"N"。  
  
 SQL_MAX_ASYNC_CONCURRENT_STATEMENTS（ODBC 3.0）  
 SQLUINTEGER 值，用于指定驱动程序在给定连接上支持的最大活动并发语句数。 如果没有特定限制或限制未知，则此值为零。  
  
 SQL_MAX_BINARY_LITERAL_LEN（ODBC 2.0）  
 SQLUINTEGER 值，用于指定 SQL 语句中二进制文本的最大长度（十六进制字符数，不包括**SQLGetTypeInfo**返回的文本前缀和后缀）。 例如，二进制文本 0xFFAA 的长度为 4。 如果没有最大长度或长度未知，则此值设置为零。  
  
 SQL_MAX_CATALOG_NAME_LEN（ODBC 1.0）  
 指定数据源中目录名称的最大长度的 SQLUSMALLINT 值。 如果没有最大长度或长度未知，则此值设置为零。  
  
 FIPS 全电平符合性驱动程序将返回至少 128。  
  
 此*信息类型*已从 ODBC 2.0*信息类型*SQL_MAX_QUALIFIER_NAME_LEN重命名为 ODBC 3.0。  
  
 SQL_MAX_CHAR_LITERAL_LEN（ODBC 2.0）  
 SQLUINTEGER 值，用于指定 SQL 语句中字符文本的最大长度（字符数，不包括**SQLGetTypeInfo**返回的文本前缀和后缀）。 如果没有最大长度或长度未知，则此值设置为零。  
  
 SQL_MAX_COLUMN_NAME_LEN（ODBC 1.0）  
 指定数据源中列名的最大长度的 SQLUSMALLINT 值。 如果没有最大长度或长度未知，则此值设置为零。  
  
 FIPS 符合等级的驱动程序将返回至少 18 个。 FIPS 中级电平符合性驱动程序将返回至少 128。  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY（ODBC 2.0）  
 指定**GROUP BY**子句中允许的最大列数的 SQLUSMALLINT 值。 如果没有指定限制或限制未知，则此值设置为零。  
  
 FIPS 符合等级的驱动程序将返回至少 6 个。 FIPS 中级级别符合要求的驱动程序将返回至少 15 个。  
  
 SQL_MAX_COLUMNS_IN_INDEX（ODBC 2.0）  
 指定索引中允许的最大列数的 SQLUSMALLINT 值。 如果没有指定限制或限制未知，则此值设置为零。  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY（ODBC 2.0）  
 指定**ORDER BY**子句中允许的最大列数的 SQLUSMALLINT 值。 如果没有指定限制或限制未知，则此值设置为零。  
  
 FIPS 符合等级的驱动程序将返回至少 6 个。 FIPS 中级级别符合要求的驱动程序将返回至少 15 个。  
  
 SQL_MAX_COLUMNS_IN_SELECT（ODBC 2.0）  
 指定选择列表中允许的最大列数的 SQLUSMALLINT 值。 如果没有指定限制或限制未知，则此值设置为零。  
  
 FIPS 符合等级的驱动程序将返回至少 100 个。 FIPS 中级电平符合性驱动程序将返回至少 250 个。  
  
 SQL_MAX_COLUMNS_IN_TABLE（ODBC 2.0）  
 指定表中允许的最大列数的 SQLUSMALLINT 值。 如果没有指定限制或限制未知，则此值设置为零。  
  
 FIPS 符合等级的驱动程序将返回至少 100 个。 FIPS 中级电平符合性驱动程序将返回至少 250 个。  
  
 SQL_MAX_CONCURRENT_ACTIVITIES（ODBC 1.0）  
 SQLUSMALLINT 值，用于指定驱动程序可以支持连接的最大活动语句数。 如果语句的结果挂起，则语句定义为活动，术语"结果"表示**SELECT**操作中的行或受**INSERT、UPDATE**或**DELETE**操作（如行计数）影响的行，或者如果该语句处于NEED_DATA状态。 **UPDATE** 此值可以反映驱动程序或数据源施加的限制。 如果没有指定限制或限制未知，则此值设置为零。  
  
 此*信息类型*已重命名为 ODBC 3.0 从 ODBC 2.0*信息类型*SQL_ACTIVE_STATEMENTS。  
  
 SQL_MAX_CURSOR_NAME_LEN（ODBC 1.0）  
 指定数据源中游标名称的最大长度的 SQLUSMALLINT 值。 如果没有最大长度或长度未知，则此值设置为零。  
  
 FIPS 符合等级的驱动程序将返回至少 18 个。 FIPS 中级电平符合性驱动程序将返回至少 128。  
  
 SQL_MAX_DRIVER_CONNECTIONS（ODBC 1.0）  
 SQLUSMALLINT 值，用于指定驱动程序可以支持环境的最大活动连接数。 此值可以反映驱动程序或数据源施加的限制。 如果没有指定限制或限制未知，则此值设置为零。  
  
 此*信息类型*已重命名为 ODBC 3.0 从 ODBC 2.0*信息类型*SQL_ACTIVE_CONNECTIONS。  
  
 SQL_MAX_IDENTIFIER_LEN（ODBC 3.0）  
 一种 SQLUSMALLINT，用于指示数据源支持用户定义名称的最大大小字符。  
  
 FIPS 符合等级的驱动程序将返回至少 18 个。 FIPS 中级电平符合性驱动程序将返回至少 128。  
  
 SQL_MAX_INDEX_SIZE（ODBC 2.0）  
 指定索引组合字段中允许的最大字节数的 SQLUINTEGER 值。 如果没有指定限制或限制未知，则此值设置为零。  
  
 SQL_MAX_PROCEDURE_NAME_LEN（ODBC 1.0）  
 指定数据源中过程名称的最大长度的 SQLUSMALLINT 值。 如果没有最大长度或长度未知，则此值设置为零。  
  
 SQL_MAX_ROW_SIZE（ODBC 2.0）  
 指定表中单个行的最大长度的 SQLUINTEGER 值。 如果没有指定限制或限制未知，则此值设置为零。  
  
 FIPS 入门级符合要求的驱动程序将返回至少 2，000。 FIPS 中级级别符合要求的驱动程序将返回至少 8，000。  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG（ODBC 3.0）  
 字符串：如果为SQL_MAX_ROW_SIZE信息类型返回的最大行大小包括行中所有SQL_LONGVARCHAR和SQL_LONGVARBINARY列的长度，"Y";否则为"N"。  
  
 SQL_MAX_SCHEMA_NAME_LEN（ODBC 1.0）  
 指定数据源中架构名称的最大长度的 SQLUSMALLINT 值。 如果没有最大长度或长度未知，则此值设置为零。  
  
 FIPS 符合等级的驱动程序将返回至少 18 个。 FIPS 中级电平符合性驱动程序将返回至少 128。  
  
 此*信息类型*已从 ODBC 2.0*信息类型*SQL_MAX_OWNER_NAME_LEN重命名为 ODBC 3.0。  
  
 SQL_MAX_STATEMENT_LEN（ODBC 2.0）  
 指定 SQL 语句的最大长度（字符数，包括空格）的 SQLUINTEGER 值。 如果没有最大长度或长度未知，则此值设置为零。  
  
 SQL_MAX_TABLE_NAME_LEN（ODBC 1.0）  
 指定数据源中表名称的最大长度的 SQLUSMALLINT 值。 如果没有最大长度或长度未知，则此值设置为零。  
  
 FIPS 符合等级的驱动程序将返回至少 18 个。 FIPS 中级电平符合性驱动程序将返回至少 128。  
  
 SQL_MAX_TABLES_IN_SELECT（ODBC 2.0）  
 指定**SELECT**语句 FROM 的**FROM**子句中允许的最大表数的 SQLUSMALLINT 值。 如果没有指定限制或限制未知，则此值设置为零。  
  
 FIPS 符合等级的驱动程序将返回至少 15 个。 FIPS 中级级别符合要求的驱动程序将返回至少 50 个。  
  
 SQL_MAX_USER_NAME_LEN（ODBC 2.0）  
 指定数据源中用户名的最大长度的 SQLUSMALLINT 值。 如果没有最大长度或长度未知，则此值设置为零。  
  
 SQL_MULT_RESULT_SETS（ODBC 1.0）  
 字符串字符串："Y"，如果数据源支持多个结果集，则"N"（如果不支持）。  
  
 有关多个结果集的详细信息，请参阅[多个结果](../../../odbc/reference/develop-app/multiple-results.md)集。  
  
 SQL_MULTIPLE_ACTIVE_TXN（ODBC 1.0）  
 字符串字符串："Y"如果驱动程序同时支持多个活动事务，"N"如果在任何时候只能有一个事务处于活动状态。  
  
 为此信息类型返回的信息不适用于分布式事务。  
  
 SQL_NEED_LONG_DATA_LEN（ODBC 2.0）  
 字符串：如果数据源需要长数据值的长度（数据类型为SQL_LONGVARCHAR、SQL_LONGVARBINARY 或长数据源特定的数据类型）的长度，则"Y"将该值发送到数据源，如果没有，则为"N"。 有关详细信息，请参阅[SQLBind参数函数](../../../odbc/reference/syntax/sqlbindparameter-function.md)和[SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
 SQL_NON_NULLABLE_COLUMNS（ODBC 1.0）  
 SQLUSMALLINT 值，用于指定数据源是否支持列中的非 NULL：  
  
 SQL_NNC_NULL = 所有列都必须为空。  
  
 SQL_NNC_NON_NULL = 列不能为空。 （数据源支持**CREATE TABLE**语句中的 **"非 NULL"** 列约束。  
  
 SQL-92 符合入门级的驱动程序将返回SQL_NNC_NON_NULL。  
  
 SQL_NULL_COLLATION（ODBC 2.0）  
 SQLUSMALLINT 值，用于指定在结果集中对 NUL 的排序位置：  
  
 SQL_NC_END = NUL 在结果集的末尾排序，而不考虑 ASC 或 DESC 关键字。  
  
 SQL_NC_HIGH = NUL 在结果集的高端排序，具体取决于 ASC 或 DESC 关键字。  
  
 SQL_NC_LOW = NUL 在结果集的低端排序，具体取决于 ASC 或 DESC 关键字。  
  
 SQL_NC_START = NUL 在结果集的开头进行排序，而不考虑 ASC 或 DESC 关键字。  
  
 SQL_NUMERIC_FUNCTIONS（ODBC 1.0）  
 注意：信息类型在 ODBC 1.0 中引入;每个位掩码都标有引入它的版本。  
  
 SQLUINTEGER 位掩码，枚举驱动程序和相关数据源支持的标量数字函数。  
  
 以下位掩码用于确定支持哪些数值函数：  
  
 SQL_FN_NUM_ABS （ODBC 1.0）SQL_FN_NUM_ACOS （ODBC 1.0）SQL_FN_NUM_ASIN （ODBC 1.0）SQL_FN_NUM_ATAN （ODBC 1.0）SQL_FN_NUM_ATAN2 （ODBC 1.0）SQL_FN_NUM_CEILING （ODBC 1.0）SQL_FN_NUM_COS （ODBC 1.0）SQL_FN_NUM_COT （ODBC 1.0）SQL_FN_NUM_DEGREES （ODBC 1.0）SQL_FN_NUM_EXP （ODBC 1.0）SQL_FN_NUM_FLOOR（ODBC 1.0）SQL_FN_NUM_LOG（ODBC 1.0）SQL_FN_NUM_LOG10（ODBC 1.0）SQL_FN_NUM_LOG10（ODBC 1.0）SQL_FN_NUM_LOG10（ODBC 1.0）SQL_FN_NUM_MOD （ODBC 1.0）SQL_FN_NUM_PI （ODBC 1.0）SQL_FN_NUM_POWER （ODBC 2.0）SQL_FN_NUM_RADIANS （ODBC 2.0）SQL_FN_NUM_RAND （ODBC 1.0）SQL_FN_NUM_ROUND （ODBC 2.0）SQL_FN_NUM_SIGN （ODBC 1.0）SQL_FN_NUM_SIN （ODBC 1.0）SQL_FN_NUM_SQRT （ODBC 1.0）SQL_FN_NUM_TAN（ODBC 1.0）SQL_FN_NUM_TRUNCATE（ODBC 1.0）SQL_FN_NUM_TRUNCATE（ODBC 2.0）  
  
 SQL_ODBC_INTERFACE_CONFORMANCE（ODBC 3.0）  
 一个 SQLUINTEGER 值，指示驱动程序符合的 ODBC 3 *.x*接口的级别。  
  
 SQL_OIC_CORE：所有 ODBC 驱动程序应遵守的最低水平。 此级别包括基本接口元素，如连接函数、用于准备和执行 SQL 语句的函数、基本结果集元数据函数、基本目录函数等。  
  
 SQL_OIC_LEVEL1：包含核心标准合规性级别功能的级别，以及可滚动的游标、书签、定位更新和删除等。  
  
 SQL_OIC_LEVEL2：包括 1 级标准符合性级别功能以及高级功能（如敏感游标）的级别;按书签更新、删除和刷新;存储程序支持;主键和外键的目录函数;多目录支持;等等。  
  
 有关详细信息，请参阅[接口一致性级别](../../../odbc/reference/develop-app/interface-conformance-levels.md)。  
  
 SQL_ODBC_VER（ODBC 1.0）  
 具有驱动程序管理器符合的 ODBC 版本的字符串。 版本是窗体 #._._.0000，其中前两位数字是主要版本，后两位数字是次要版本。 这仅在驱动程序管理器中实现。  
  
 SQL_OJ_CAPABILITIES（ODBC 2.01）  
 一个 SQLUINTEGER 位掩码，枚举驱动程序和数据源支持的外部联接的类型。 以下位掩码用于确定哪些类型受支持：  
  
 SQL_OJ_LEFT = 支持左外部联接。  
  
 SQL_OJ_RIGHT = 支持右外部联接。  
  
 SQL_OJ_FULL = 支持完全外部联接。  
  
 SQL_OJ_NESTED = 支持嵌套外部联接。  
  
 SQL_OJ_NOT_ORDERED = 外部联接的 ON 子句中的列名称不必与**OUTER JOIN**子句中的相应表名的顺序相同。  
  
 SQL_OJ_INNER = 内部表（左外部联接中的右表或右外部联接中的左表）也可以在内部联接中使用。 这不适用于没有内部表的完整外部联接。  
  
 SQL_OJ_ALL_COMPARISON_OPS = ON 子句中的比较运算符可以是任何 ODBC 比较运算符。 如果未设置此位，则外部联接中只能使用等 （*） 比较运算符。  
  
 如果未返回这些选项作为支持，则不支持外部联接子句。  
  
 有关 SQL-92 定义的 SELECT 语句中关系联接运算符的支持的信息，请参阅SQL_SQL92_RELATIONAL_JOIN_OPERATORS。  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT（ODBC 2.0）  
 字符串：如果 ORDER BY 子句中的列必须位于选择列表中，则为"Y";如果**ORDER BY**子句中的列必须位于选择列表中，则为"Y";否则，"N"。  
  
 SQL_PARAM_ARRAY_ROW_COUNTS（ODBC 3.0）  
 在参数化执行中，对驱动程序的属性进行枚举，了解行计数的可用性。 具有以下值：  
  
 SQL_PARC_BATCH = 每个参数集都可用于单个行计数。 这在概念上等效于生成一批 SQL 语句的驱动程序，该语句针对数组中设置的每个参数一个。 可以使用SQL_PARAM_STATUS_PTR描述符字段检索扩展的错误信息。  
  
 SQL_PARC_NO_BATCH = 只有一个行计数可用，即执行整个参数数组的语句所产生的累积行计数。 这在概念上等效于将语句与完整参数数组一起作为一个原子单元处理。 错误的处理方式与执行一个语句相同。  
  
 SQL_PARAM_ARRAY_SELECTS（ODBC 3.0）  
 一个 SQLUINTEGER，枚举驱动程序的属性，说明参数化执行中结果集的可用性。 具有以下值：  
  
 SQL_PAS_BATCH = 每组参数都有一个结果集可用。 这在概念上等效于生成一批 SQL 语句的驱动程序，该语句针对数组中设置的每个参数一个。  
  
 SQL_PAS_NO_BATCH = 只有一个结果集可用，它表示执行整个参数数组的语句所产生的累积结果集。 这在概念上等效于将语句与完整参数数组一起作为一个原子单元处理。  
  
 SQL_PAS_NO_SELECT = 驱动程序不允许使用参数数组执行结果集生成语句。  
  
 SQL_PROCEDURE_TERM（ODBC 1.0）  
 具有过程的数据源供应商名称的字符串;例如，"数据库过程"、"存储过程"、"过程"、"包"或"存储查询"。  
  
 SQL_PROCEDURES（ODBC 1.0）  
 字符串字符串："Y"，如果数据源支持过程，并且驱动程序支持 ODBC 过程调用语法;如果数据源支持过程调用语法，则为"Y"，否则为"N"。  
  
 SQL_POS_OPERATIONS（ODBC 2.0）  
 在**SQLSetPos**中枚举支持操作的 SQLINTEGER 位掩码。  
  
 以下位掩码与标志一起使用，以确定支持哪些选项。  
  
 SQL_POS_POSITION （ODBC 2.0） SQL_POS_REFRESH （ODBC 2.0） SQL_POS_UPDATE （ODBC 2.0） SQL_POS_DELETE （ODBC 2.0） SQL_POS_ADD （ODBC 2.0）  
  
 SQL_QUOTED_IDENTIFIER_CASE（ODBC 2.0）  
 SQLUSMALLINT 值如下所示：  
  
 SQL_IC_UPPER = SQL 中的引用标识符不区分大小写，存储在系统目录中的大写中。  
  
 SQL_IC_LOWER = SQL 中的引用标识符不区分大小写，存储在系统目录中小写。  
  
 SQL_IC_SENSITIVE = SQL 中的引用标识符区分大小写，存储在系统目录中的混合情况下。 （在符合 SQL-92 的数据库中，引用的标识符始终对大小写敏感。  
  
 SQL_IC_MIXED = SQL 中的引用标识符不区分大小写，存储在系统目录中的混合情况下。  
  
 SQL-92 符合入门级的驱动程序将始终返回SQL_IC_SENSITIVE。  
  
 SQL_ROW_UPDATES（ODBC 1.0）  
 字符串："Y"，如果键集驱动或混合游标维护所有提取行的行版本或值，因此可以检测自上次提取该行以来任何用户对行所做的任何更新。 （这仅适用于更新，不适用于删除或插入。调用**SQLFetchScroll**时，驱动程序可以将SQL_ROW_UPDATED标志返回到行状态数组。 否则，"N"。  
  
 SQL_SCHEMA_TERM（ODBC 1.0）  
 具有数据源供应商名称的架构的字符串;例如，"所有者"、"授权 ID"或"架构"。  
  
 字符字符串可以在上部、下部或混合情况下返回。  
  
 SQL-92 符合入门级的驱动程序将始终返回"架构"。  
  
 此*信息类型*已从 ODBC 2.0*信息类型*SQL_OWNER_TERM重命名为 ODBC 3.0。  
  
 SQL_SCHEMA_USAGE（ODBC 2.0）  
 一个 SQLUINTEGER 位掩码，枚举了可以使用架构的语句：  
  
 SQL_SU_DML_STATEMENTS = 架构在所有数据操作语言语句中都受支持：**选择**、**插入**、**更新**、**删除**等，如果支持，**请选择更新**并定位更新和删除语句。  
  
 SQL_SU_PROCEDURE_INVOCATION = ODBC 过程调用语句中支持架构。  
  
 SQL_SU_TABLE_DEFINITION = 所有表定义语句都支持架构：**创建表**、**创建视图**、**更改表****、DROP TABLE**和 DROP**视图**。  
  
 SQL_SU_INDEX_DEFINITION = 所有索引定义语句都支持架构：**创建索引**和**DROP INDEX**。  
  
 SQL_SU_PRIVILEGE_DEFINITION = 所有权限定义语句都支持架构 **：GRANT**和**REVOKE**。  
  
 SQL-92 符合入门级的驱动程序将始终返回SQL_SU_DML_STATEMENTS、SQL_SU_TABLE_DEFINITION和SQL_SU_PRIVILEGE_DEFINITION选项（如支持）。  
  
 此*信息类型*已从 ODBC 2.0*信息类型*SQL_OWNER_USAGE重命名为 ODBC 3.0。  
  
 SQL_SCROLL_OPTIONS（ODBC 1.0）  
 注意：信息类型在 ODBC 1.0 中引入;每个位掩码都标有引入它的版本。  
  
 SQLUINTEGER 位掩码，枚举可滚动游标支持的滚动选项。  
  
 以下位掩码用于确定哪些选项受支持：  
  
 SQL_SO_FORWARD_ONLY = 光标仅向前滚动。 （ODBC 1.0）  
  
 SQL_SO_STATIC = 结果集中的数据是静态的。 （ODBC 2.0）  
  
 SQL_SO_KEYSET_DRIVEN = 驱动程序保存并使用结果集中每行的键。 （ODBC 1.0）  
  
 SQL_SO_DYNAMIC = 驱动程序保留行集中每行的键（键集大小与行集大小相同）。 （ODBC 1.0）  
  
 SQL_SO_MIXED = 驱动程序保留键集中每行的键，并且键集大小大于行集大小。 游标在键集中内键集驱动，在键集外部动态。 （ODBC 1.0）  
  
 有关可滚动光标的信息，请参阅[可滚动光标](../../../odbc/reference/develop-app/scrollable-cursors.md)。  
  
 SQL_SEARCH_PATTERN_ESCAPE（ODBC 1.0）  
 指定驱动程序支持哪些内容的字符串，允许使用模式匹配元字符下划线 （*） 和百分比符号 （%）作为搜索模式中的有效字符。 此转义字符仅适用于支持搜索字符串的目录函数参数。 如果此字符串为空，则驱动程序不支持搜索模式转义字符。  
  
 由于此信息类型不表示**LIKE**谓词中转义字符的一般支持，因此 SQL-92 不包括对此字符字符串的要求。  
  
 此信息*类型*仅限于目录函数。 有关在搜索模式字符串中使用转义符的说明，请参阅[模式值参数](../../../odbc/reference/develop-app/pattern-value-arguments.md)。  
  
 SQL_SERVER_NAME（ODBC 1.0）  
 具有实际数据源特定服务器名称的字符串;在**SQLConnect** **、SQLDriverConnect****和**（ .  
  
 SQL_SPECIAL_CHARACTERS（ODBC 2.0）  
 一个字符串，其中包含数据源上可用于标识符名称（如表名、列名或索引名称）的所有特殊字符（即除 z、A 到 Z、0 到 Z 和下划线之外的所有字符）。 例如，"$+"。 如果标识符包含一个或多个这些字符，则标识符必须是分隔标识符。  
  
 SQL_SQL_CONFORMANCE（ODBC 3.0）  
 指示驱动程序支持的 SQL-92 级别的 SQLUINTEGER 值：  
  
 SQL_SC_SQL92_ENTRY = 符合入门级 SQL-92。  
  
 SQL_SC_FIPS127_2_TRANSITIONAL = 符合 FIPS 127-2 过渡电平。  
  
 SQL_SC_SQL92_FULL = 符合全级别 SQL-92。  
  
 SQL_SC_SQL92_INTERMEDIATE = 符合中级 SQL-92 标准。  
  
 SQL_SQL92_DATETIME_FUNCTIONS（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举驱动程序和相关数据源支持的约会时间标量函数，如 SQL-92 中定义的那样。  
  
 以下位掩码用于确定哪些日期时间函数受支持：  
  
 SQL_SDF_CURRENT_DATESQL_SDF_CURRENT_TIMESQL_SDF_CURRENT_TIMESTAMP  
  
 SQL_SQL92_FOREIGN_KEY_DELETE_RULE（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举**DELETE**语句中支持的规则，如 SQL-92 中定义的那样。  
  
 以下位掩码用于确定数据源支持哪些子句：  
  
 SQL_SFKD_CASCADESQL_SFKD_NO_ACTIONSQL_SFKD_SET_DEFAULTSQL_SFKD_SET_NULL  
  
 FIPS 过渡电平符合性驱动程序将始终返回支持的所有这些选项。  
  
 SQL_SQL92_FOREIGN_KEY_UPDATE_RULE（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举**更新**语句中支持的规则，如 SQL-92 中定义的那样。  
  
 以下位掩码用于确定数据源支持哪些子句：  
  
 SQL_SFKU_CASCADESQL_SFKU_NO_ACTIONSQL_SFKU_SET_DEFAULTSQL_SFKU_SET_NULL  
  
 SQL-92 完全符合级别的驱动程序将始终返回所有这些选项（如支持）。  
  
 SQL_SQL92_GRANT（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举**在 GRANT**语句中支持的子句，如 SQL-92 中定义的那样。  
  
 必须支持此功能的 SQL-92 或 FIPS 一致性级别显示在每个位掩码旁边的括号中。  
  
 以下位掩码用于确定数据源支持哪些子句：  
  
 SQL_SG_DELETE_TABLE（入门级）SQL_SG_INSERT_COLUMN（中级）SQL_SG_INSERT_COLUMN（中级）SQL_SG_INSERT_TABLE（入门级）SQL_SG_REFERENCES_TABLE（入门级）SQL_SG_REFERENCES_COLUMN（入门级）SQL_SG_SELECT_TABLE（入门级）SQL_SG_UPDATE_COLUMN（入门级）SQL_SG_UPDATE_TABLE（入门级）SQL_SG_USAGE_ON_DOMAIN（FIPS过渡级别）SQL_SG_USAGE_ON_CHARACTER_SET（FIPS过渡级别）SQL_SG_USAGE_ON_COLLATION（FIPS过渡级别）SQL_SG_USAGE_ON_TRANSLATION（FIPS过渡级别）级别）SQL_SG_WITH_GRANT_OPTION（入门级）  
  
 SQL_SQL92_NUMERIC_VALUE_FUNCTIONS（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举驱动程序和相关数据源支持的数字值标量函数，如 SQL-92 中定义的那样。  
  
 以下位掩码用于确定支持哪些数值函数：  
  
 SQL_SNVF_BIT_LENGTHSQL_SNVF_CHAR_LENGTHSQL_SNVF_CHARACTER_LENGTHSQL_SNVF_EXTRACTSQL_SNVF_OCTET_LENGTHSQL_SNVF_POSITION  
  
 SQL_SQL92_PREDICATES（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举**SELECT**语句中支持的谓词，如 SQL-92 中定义的那样。  
  
 必须支持此功能的 SQL-92 或 FIPS 一致性级别显示在每个位掩码旁边的括号中。  
  
 以下位掩码用于确定数据源支持哪些选项：  
  
 SQL_SP_BETWEEN（入门级）SQL_SP_COMPARISON（入门级）SQL_SP_EXISTS（入门级）SQL_SP_IN（入门级）SQL_SP_ISNOTNULL SQL_SP_IN（入门级）SQL_SP_ISNULL（入门级）SQL_SP_LIKE（入门级）SQL_SP_MATCH_FULL（满级）SQL_SP_MATCH_PARTIAL（满级）SQL_SP_MATCH_UNIQUE_FULL（满级）SQL_SP_MATCH_UNIQUE_PARTIAL（满级）SQL_SP_OVERLAPS（FIPS 过渡级别）SQL_SP_QUANTIFIED_COMPARISON（入门级）SQL_SP_UNIQUE（入门级）  
  
 SQL_SQL92_RELATIONAL_JOIN_OPERATORS（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举**SELECT**语句中支持的关系联接运算符，如 SQL-92 中定义的那样。  
  
 必须支持此功能的 SQL-92 或 FIPS 一致性级别显示在每个位掩码旁边的括号中。  
  
 以下位掩码用于确定数据源支持哪些选项：  
  
 SQL_SRJO_CORRESPONDING_CLAUSE（中级）SQL_SRJO_CROSS_JOIN（全级）SQL_SRJO_EXCEPT_JOIN（中级）SQL_SRJO_FULL_OUTER_JOIN（中级）SQL_SRJO_INNER_JOIN（中级）SQL_SRJO_INNER_JOIN（中级过渡级别）SQL_SRJO_INTERSECT_JOIN（中级）SQL_SRJO_LEFT_OUTER_JOIN（FIPS过渡级别）SQL_SRJO_NATURAL_JOIN（FIPS过渡级别）SQL_SRJO_RIGHT_OUTER_JOIN（FIPS过渡级别）SQL_SRJO_UNION_JOIN（全级）  
  
 SQL_SRJO_INNER_JOIN表示对内部**JOIN**语法的支持，而不是内部联接功能的支持。 对内部**JOIN**语法的支持是 FIPS 过渡，而对内部联接功能的支持是**ENTRY**。  
  
 SQL_SQL92_REVOKE（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举**了 REVOKE**语句中支持的子句，如 SQL-92 中定义，数据源支持。  
  
 必须支持此功能的 SQL-92 或 FIPS 一致性级别显示在每个位掩码旁边的括号中。  
  
 以下位掩码用于确定数据源支持哪些子句：  
  
 SQL_SR_CASCADE（FIPS过渡级别）SQL_SR_DELETE_TABLE（入门级）SQL_SR_GRANT_OPTION_FOR（中级）SQL_SR_INSERT_COLUMN（中级）SQL_SR_INSERT_TABLE（入门级）SQL_SR_REFERENCES_COLUMN（入门级）SQL_SR_REFERENCES_TABLE（入门级）SQL_SR_RESTRICT（FIPS过渡级别）SQL_SR_SELECT_TABLE（入门级）SQL_SR_UPDATE_COLUMN（入门级）SQL_SR_UPDATE_TABLE（入门级）SQL_SR_USAGE_ON_DOMAIN（FIPS过渡级别）SQL_SR_USAGE_ON_CHARACTER_SET（FIPS过渡级别）SQL_SR_USAGE_ON_COLLATION（FIPS过渡级别）SQL_SR_USAGE_ON_TRANSLATION（FIPS过渡级别）  
  
 SQL_SQL92_ROW_VALUE_CONSTRUCTOR（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举**SELECT**语句中支持的行值构造函数表达式，如 SQL-92 中定义的那样。 以下位掩码用于确定数据源支持哪些选项：  
  
 SQL_SRVC_VALUE_EXPRESSIONSQL_SRVC_NULLSQL_SRVC_DEFAULTSQL_SRVC_ROW_SUBQUERY  
  
 SQL_SQL92_STRING_FUNCTIONS（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举驱动程序和相关数据源支持的字符串标量函数，如 SQL-92 中定义的那样。  
  
 以下位掩码用于确定支持哪些字符串函数：  
  
 SQL_SSF_CONVERTSQL_SSF_LOWERSQL_SSF_UPPERSQL_SSF_SUBSTRINGSQL_SSF_TRANSLATESQL_SSF_TRIM_BOTHSQL_SSF_TRIM_LEADINGSQL_SSF_TRIM_TRAILING  
  
 SQL_SQL92_VALUE_EXPRESSIONS（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举 SQL-92 中定义的受支持的值表达式。  
  
 必须支持此功能的 SQL-92 或 FIPS 一致性级别显示在每个位掩码旁边的括号中。  
  
 以下位掩码用于确定数据源支持哪些选项：  
  
 SQL_SVE_CASE（中级）SQL_SVE_CAST（FIPS过渡级别）SQL_SVE_COALESCE（中级）SQL_SVE_NULLIF（中级）  
  
 SQL_STANDARD_CLI_CONFORMANCE（ODBC 3.0）  
 一个 SQLUINTEGER 位掩码，枚举驱动程序符合的 CLI 标准或标准。 以下位掩码用于确定驱动程序符合的级别：  
  
 SQL_SCC_XOPEN_CLI_VERSION1：驱动程序符合开放组 CLI 版本 1。  
  
 SQL_SCC_ISO92_CLI：驱动程序符合 ISO 92 CLI。  
  
 SQL_STATIC_CURSOR_ATTRIBUTES1（ODBC 3.0）  
 描述驱动程序支持的静态游标的属性的 SQLUINTEGER 位掩码。 此位掩码包含属性的第一个子集;对于第二个子集，请参阅SQL_STATIC_CURSOR_ATTRIBUTES2。  
  
 以下位掩码用于确定哪些属性受支持：  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 有关这些位掩码的说明，请参阅SQL_DYNAMIC_CURSOR_ATTRIBUTES1（并在说明中用"静态光标"代替"动态光标"）。  
  
 SQL-92 中间级别一致性驱动程序通常会返回SQL_CA1_NEXT、SQL_CA1_ABSOLUTE和SQL_CA1_RELATIVE选项（如支持），因为驱动程序支持通过嵌入式 SQL FETCH 语句滚动游标。 但是，由于这不能直接确定基础 SQL 支持，因此即使对于 SQL-92 符合级别的驱动程序，也不支持可滚动游标。  
  
 SQL_STATIC_CURSOR_ATTRIBUTES2（ODBC 3.0）  
 描述驱动程序支持的静态游标的属性的 SQLUINTEGER 位掩码。 此位掩码包含属性的第二个子集;对于第一个子集，请参阅SQL_STATIC_CURSOR_ATTRIBUTES1。  
  
 以下位掩码用于确定哪些属性受支持：  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 有关这些位掩码的说明，请参阅SQL_DYNAMIC_CURSOR_ATTRIBUTES2（并在说明中用"静态光标"代替"动态光标"）。  
  
 SQL_STRING_FUNCTIONS（ODBC 1.0）  
 注意：信息类型在 ODBC 1.0 中引入;每个位掩码都标有引入它的版本。  
  
 SQLUINTEGER 位掩码，枚举驱动程序和相关数据源支持的标量字符串函数。  
  
 以下位掩码用于确定支持哪些字符串函数：  
  
 SQL_FN_STR_ASCII （ODBC 1.0）SQL_FN_STR_BIT_LENGTH （ODBC 3.0）SQL_FN_STR_CHAR （ODBC 1.0）SQL_FN_STR_CHAR_LENGTH （ODBC 3.0）SQL_FN_STR_CHARACTER_LENGTH （ODBC 3.0）SQL_FN_STR_CONCAT （ODBC 3.0）SQL_FN_STR_CONCAT （ODBC 1.0）SQL_FN_STR_DIFFERENCE （ODBC 1.0）SQL_FN_STR_INSERT （ODBC 1.0）SQL_FN_STR_LCASE （ODBC 1.0）SQL_FN_STR_LEFT （ODBC 1.0）SQL_FN_STR_LENGTH（ODBC 1.0）SQL_FN_STR_LOCATE（ODBC 1.0）SQL_FN_STR_LTRIM（ODBC 1.0）SQL_FN_STR_LTRIM（ODBC 1.0）1.0） SQL_FN_STR_OCTET_LENGTH （ODBC 3.0） SQL_FN_STR_POSITION （ODBC 3.0） SQL_FN_STR_REPEAT （ODBC 1.0）SQL_FN_STR_REPLACE （ODBC 1.0）SQL_FN_STR_RIGHT （ODBC 1.0）SQL_FN_STR_RTRIM （ODBC 1.0）SQL_FN_STR_SOUNDEX （ODBC 2.0）SQL_FN_STR_SPACE （ODBC 2.0）SQL_FN_STR_SUBSTRING （ODBC 1.0）SQL_FN_STR_UCASE（ODBC 1.0）  
  
 如果应用程序可以使用*string_exp1* *、string_exp2*调用**LOCATE**标量函数和*启动*参数，则驱动程序返回SQL_FN_STR_LOCATE位掩码。 如果应用程序只能调用 STRING_EXP1*和**string_exp2*参数的 LOCATE 标量函数，则驱动程序将返回SQL_FN_STR_LOCATE_2位掩码。 完全支持**LOCATE**标量函数的驱动程序将返回两个位掩码。  
  
 （有关详细信息，请参阅附录 E 中的[字符串函数](../../../odbc/reference/appendixes/string-functions.md)"斯卡拉尔函数"。  
  
 SQL_SUBQUERIES（ODBC 2.0）  
 SQLUINTEGER 位掩码，枚举支持子查询的谓词：  
  
 SQL_SQ_CORRELATED_SUBQUERIESSQL_SQ_COMPARISONSQL_SQ_EXISTSSQL_SQ_INSQL_SQ_QUANTIFIED  
  
 SQL_SQ_CORRELATED_SUBQUERIES位掩码表示支持子查询的所有谓词都支持相关的子查询。  
  
 SQL-92 符合入门级的驱动程序将始终返回一个位掩码，其中设置所有这些位。  
  
 SQL_SYSTEM_FUNCTIONS（ODBC 1.0）  
 SQLUINTEGER 位掩码，枚举驱动程序和相关数据源支持的标量系统函数。  
  
 以下位掩码用于确定支持哪些系统功能：  
  
 SQL_FN_SYS_DBNAMESQL_FN_SYS_IFNULLSQL_FN_SYS_USERNAME  
  
 SQL_TABLE_TERM（ODBC 1.0）  
 具有表的数据源供应商名称的字符串;例如，"表"或"文件"。  
  
 此字符串可以是上部、下部或混合大小写。  
  
 SQL-92 符合入门级的驱动程序将始终返回"表"。  
  
 SQL_TIMEDATE_ADD_INTERVALS（ODBC 2.0）  
 SQLUINTEGER 位掩码，枚举了 TIMESTAMPADD 标量函数的驱动程序和相关数据源支持的时间戳间隔。  
  
 以下位掩码用于确定支持哪些间隔：  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 FIPS 过渡电平一致性驱动程序将始终返回一个位掩码，其中设置所有这些位。  
  
 SQL_TIMEDATE_DIFF_INTERVALS（ODBC 2.0）  
 SQLUINTEGER 位掩码，枚举了 TIMESTAMPDIFF 标量函数的驱动程序和相关数据源支持的时间戳间隔。  
  
 以下位掩码用于确定支持哪些间隔：  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 FIPS 过渡电平一致性驱动程序将始终返回一个位掩码，其中设置所有这些位。  
  
 SQL_TIMEDATE_FUNCTIONS（ODBC 1.0）  
 注意：信息类型在 ODBC 1.0 中引入;每个位掩码都标有引入它的版本。  
  
 SQLUINTEGER 位掩码，枚举驱动程序和相关数据源支持的标量日期和时间函数。  
  
 以下位掩码用于确定支持哪些日期和时间函数：  
  
 SQL_FN_TD_CURRENT_DATE ODBC 3.0）SQL_FN_TD_CURRENT_TIME （ODBC 3.0）SQL_FN_TD_CURRENT_TIMESTAMP （ODBC 3.0）SQL_FN_TD_CURDATE （ODBC 1.0）SQL_FN_TD_CURTIME （ODBC 1.0） SQL_FN_TD_DAYNAME （ODBC 1.0） SQL_FN_TD_DAYOFMONTH （ODBC 1.0）SQL_FN_TD_DAYOFWEEK （ODBC 1.0）SQL_FN_TD_DAYOFYEAR （ODBC 1.0） SQL_FN_TD_EXTRACT （ODBC 3.0）SQL_FN_TD_HOUR （ODBC 1.0）SQL_FN_TD_MINUTE（ODBC 1.0）SQL_FN_TD_MONTH（ODBC 1.0）SQL_FN_TD_MONTH（ODBC 1.0）SQL_FN_TD_MONTH（ODBC 1.0）1.0）SQL_FN_TD_MONTHNAME （ODBC 2.0）SQL_FN_TD_NOW （ODBC 1.0）SQL_FN_TD_QUARTER （ODBC 1.0）SQL_FN_TD_SECOND （ODBC 1.0）SQL_FN_TD_TIMESTAMPADD （ODBC 2.0）SQL_FN_TD_TIMESTAMPDIFF （ODBC 2.0）SQL_FN_TD_WEEK （ODBC 1.0）SQL_FN_TD_YEAR（ODBC 1.0）  
  
 SQL_TXN_CAPABLE（ODBC 1.0）  
 注意：信息类型在 ODBC 1.0 中引入;每个返回值都标有引入该值的版本。  
  
 描述驱动程序或数据源中的事务支持的 SQLUSMALLINT 值：  
  
 SQL_TC_NONE = 不支持事务。 （ODBC 1.0）  
  
 SQL_TC_DML = 事务只能包含数据操作语言 （DML） 语句 **（SELECT、****插入**、**更新**、**删除**）. 事务中遇到的数据定义语言 （DDL） 语句会导致错误。 （ODBC 1.0）  
  
 SQL_TC_DDL_COMMIT = 事务只能包含 DML 语句。 事务中遇到的 DDL 语句（**创建表****、DROP INDEX**等）会导致提交事务。 （ODBC 2.0）  
  
 SQL_TC_DDL_IGNORE = 事务只能包含 DML 语句。 忽略事务中遇到的 DDL 语句。 （ODBC 2.0）  
  
 SQL_TC_ALL = 事务可以按任何顺序包含 DDL 语句和 DML 语句。 （ODBC 1.0）  
  
 （由于 SQL-92 中必须支持事务，因此 SQL-92 符合的驱动程序[任何级别]永远不会返回SQL_TC_NONE。  
  
 SQL_TXN_ISOLATION_OPTION（ODBC 1.0）  
 SQLUINTEGER 位掩码，枚举驱动程序或数据源中可用的事务隔离级别。  
  
 以下位掩码与标志一起使用，以确定支持哪些选项：  
  
 SQL_TXN_READ_UNCOMMITTEDSQL_TXN_READ_COMMITTEDSQL_TXN_REPEATABLE_READSQL_TXN_SERIALIZABLE  
  
 有关这些隔离级别的说明，请参阅SQL_DEFAULT_TXN_ISOLATION的说明。  
  
 要设置事务隔离级别，应用程序调用**SQLSetConnectAttr**来设置SQL_ATTR_TXN_ISOLATION属性。 有关详细信息，请参阅[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
 SQL-92 符合入门级的驱动程序将始终返回SQL_TXN_SERIALIZABLE支持。 FIPS 过渡电平符合性驱动程序将始终返回支持的所有这些选项。  
  
 SQL_UNION（ODBC 2.0）  
 枚举**UNION**子句支持的 SQLUINTEGER 位掩码：  
  
 SQL_U_UNION = 数据源支持**UNION**子句。  
  
 SQL_U_UNION_ALL = 数据源支持**UNION**子句中的**ALL**关键字。 （在这种情况下 **，SQLGetInfo**将返回SQL_U_UNION和SQL_U_UNION_ALL。  
  
 SQL-92 符合入门级的驱动程序将始终返回这两个选项作为支持。  
  
 SQL_USER_NAME（ODBC 1.0）  
 具有特定数据库中使用的名称的字符串，该字符串可能不同于登录名。  
  
 SQL_XOPEN_CLI_YEAR（ODBC 3.0）  
 指示 OPENGROUP 规范发布年份的字符串，ODBC 驱动程序管理器的版本完全符合该规范。  
  
 SQL_ACCESSIBLE_PROCEDURES（ODBC 1.0）  
 字符串字符串："Y"，如果用户可以执行**SQL 程序**返回的所有过程;如果返回过程时可能返回用户无法执行，则为"N"。  
  
 SQL_ACCESSIBLE_TABLES（ODBC 1.0）  
 字符串字符串："Y"，**如果用户保证选择** **SQLTables**返回的所有表的权限;如果返回的表是用户无法访问的表，则为"N"。  
  
 SQL_ACTIVE_ENVIRONMENTS（ODBC 3.0）  
 指定驱动程序可以支持的最大活动环境数的 SQLUSMALLINT 值。 如果没有指定限制或限制未知，则此值设置为零。  
  
 SQL_AGGREGATE_FUNCTIONS（ODBC 3.0）  
 SQLUINTEGER 位掩码枚举对聚合函数的支持：  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 SQL-92 符合入门级的驱动程序将始终返回所有这些选项（如支持）。  
  
 SQL_ALTER_DOMAIN（ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举**了在**SQL-92 中定义的 ALTER DOMAIN 语句中子句，数据源支持。 SQL-92 完全符合级别的驱动程序将始终返回所有位掩码。 返回值"0"表示不支持 ALTER **DOMAIN**语句。  
  
 必须支持此功能的 SQL-92 或 FIPS 一致性级别显示在每个位掩码旁边的括号中。  
  
 以下位掩码用于确定哪些子句受支持：  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = 支持添加域约束（完整级别）  
  
 SQL_AD_ADD_DOMAIN_DEFAULT \<= 更改\<域>>受支持的域默认子句（完整级别）  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION \<=>为命名域约束（中间级别）支持约束名称定义子句  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT \<= 支持>删除域约束子句（全级别）  
  
 SQL_AD_DROP_DOMAIN_DEFAULT \<= 更改\<域>删除域默认子句>支持（完整级别）  
  
 如果\<支持>添加域约束\<（设置SQL_AD_ADD_DOMAIN_CONSTRAINT位），以下位指定支持的约束属性>：  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE（全级别）SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE（全级别）SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED（全级别）SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE（全级别）  
  
 SQL_ALTER_TABLE（ODBC 2.0）  
 SQLUINTEGER 位掩码，枚举数据源支持的**ALTER TABLE**语句中子句。  
  
 必须支持此功能的 SQL-92 或 FIPS 一致性级别显示在每个位掩码旁边的括号中。  
  
 以下位掩码用于确定哪些子句受支持：  
  
 SQL_AT_ADD_COLUMN_COLLATION \<= 支持添加列>子句，具有指定列排序规则（完整级别）（ODBC 3.0）的功能  
  
 SQL_AT_ADD_COLUMN_DEFAULT \<= 支持添加列>子句，具有指定列默认值（FIPS 过渡级别）（ODBC 3.0）的功能  
  
 SQL_AT_ADD_COLUMN_SINGLE \<= 支持添加列>（FIPS 过渡级别）（ODBC 3.0）  
  
 SQL_AT_ADD_CONSTRAINT \<= 支持添加列>子句，具有指定列约束（FIPS 过渡级别）（ODBC 3.0）的功能  
  
 SQL_AT_ADD_TABLE_CONSTRAINT \<= 支持>项（FIPS过渡级别）（ODBC 3.0）添加表约束  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION \<=>为命名列和表约束（中间级别）（ODBC 3.0）支持约束名称定义  
  
 支持SQL_AT_DROP_COLUMN_CASCADE \<= 丢弃列> CASCADE（FIPS 过渡级别）（ODBC 3.0）  
  
 SQL_AT_DROP_COLUMN_DEFAULT \<= 更改\<列>删除列默认子句>支持（中级级别）（ODBC 3.0）  
  
 支持SQL_AT_DROP_COLUMN_RESTRICT \<= 下拉列>限制（FIPS 过渡级别）（ODBC 3.0）  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE （ODBC 3.0）  
  
 支持SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT \<=>约束的放置列（FIPS 过渡级别）（ODBC 3.0）  
  
 SQL_AT_SET_COLUMN_DEFAULT \<= 更改\<列>设置列默认子句>支持（中级级别）（ODBC 3.0）  
  
 如果支持指定列或表\<约束（设置SQL_AT_ADD_CONSTRAINT位），以下位将指定支持约束属性>：  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED（全级） （ODBC 3.0） SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE （全级别） （ODBC 3.0）SQL_AT_CONSTRAINT_DEFERRABLE（完整级别）（ODBC 3.0）SQL_AT_CONSTRAINT_NON_DEFERRABLE（全级）（ODBC 3.0）  
  
 SQL_ASYNC_MODE（ODBC 3.0）  
 指示驱动程序中异步支持级别的 SQLUINTEGER 值：  
  
 SQL_AM_CONNECTION = 支持连接级异步执行。 与给定连接句柄关联的所有语句句柄都处于异步模式，或者所有语句句柄都处于同步模式。 连接上的语句句柄不能处于异步模式，而同一连接上的另一个语句句柄处于同步模式，反之亦然。  
  
 SQL_AM_STATEMENT = 支持语句级异步执行。 与连接句柄关联的某些语句句柄可以处于异步模式，而同一连接上的其他语句句柄处于同步模式。  
  
 不支持SQL_AM_NONE = 不支持异步模式。  
  
 SQL_BATCH_ROW_COUNT （ODBC 3.0）  
 SQLUINTEGER 位掩码，枚举驱动程序相对于行计数的可用性的行为。 以下位掩码与信息类型一起使用：  
  
 SQL_BRC_ROLLED_UP = 连续插入、删除或更新语句的行计数汇总为一个。 如果未设置此位，则行计数可用于每个语句。  
  
 SQL_BRC_PROCEDURES = 在存储过程中执行批处理时，行计数（如果有）可用。 如果行计数可用，则它们可以汇总或单独可用，具体取决于SQL_BRC_ROLLED_UP位。  
  
 SQL_BRC_EXPLICIT = 当通过调用 SQLExecute 或**SQLExecDirect**直接执行批处理时**SQLExecDirect**，行计数（如果有）可用。 如果行计数可用，则它们可以汇总或单独可用，具体取决于SQL_BRC_ROLLED_UP位。  
  
## <a name="example"></a>示例  
 **SQLGetInfo**在 #*InfoValuePtr*中返回受支持的选项列表作为 SQLUINTEGER 位掩码。 每个选项的位掩码与标志一起使用，以确定该选项是否受支持。  
  
 例如，应用程序可以使用以下代码来确定与连接关联的驱动程序是否支持 SUBSTRING 标量函数。  
  
 有关使用**SQLGetInfo**的另一个示例，请参阅[SQLTables 函数](../../../odbc/reference/syntax/sqltables-function.md)。  
  
```cpp  
SQLUINTEGER fFuncs;  
  
SQLGetInfo(hdbc,   
           SQL_STRING_FUNCTIONS,  
           (SQLPOINTER)&fFuncs,  
           sizeof(fFuncs),  
           NULL);  
  
// SUBSTRING supported  
if (fFuncs & SQL_FN_STR_SUBSTRING)   
   ;   // do something  
  
// SUBSTRING not supported  
else  
   ;   // do something else  
```  
  
## <a name="related-functions"></a>相关函数  
 返回连接属性的设置  
 [SQLGetConnectAttr 函数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
 确定驱动程序是否支持函数  
 [SQLGetFunctions 函数](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
 返回语句属性的设置  
 [SQLGetStmtAttr 函数](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)  
  
 返回有关数据源数据类型的信息  
 [SQLGetTypeInfo 函数](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
