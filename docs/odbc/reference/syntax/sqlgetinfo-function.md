---
title: "SQLGetInfo 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 48
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 57ba22ee8645f1d3548be91adc9aafb4fc016c79
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetinfo-function"></a>SQLGetInfo 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLGetInfo**返回有关与连接关联的驱动程序和数据源的常规信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLGetInfo(  
     SQLHDBC         ConnectionHandle,  
     SQLUSMALLINT    InfoType,  
     SQLPOINTER      InfoValuePtr,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>参数  
 *ConnectionHandle*  
 [输入]连接句柄。  
  
 *信息类型*  
 [输入]信息的类型。  
  
 *InfoValuePtr*  
 [输出]指向要返回的信息在其中的缓冲区的指针。 具体取决于*信息类型*请求，返回的信息将以下项之一： 以 null 结尾的字符串、 SQLUSMALLINT 值、 SQLUINTEGER 位掩码，SQLUINTEGER 标志、 SQLUINTEGER 二进制值，或SQLULEN 值。  
  
 如果*信息类型*自变量是 SQL_DRIVER_HDESC 或 SQL_DRIVER_HSTMT， *InfoValuePtr*自变量是同时输入和输出。 （请参阅更高版本中的详细信息此函数说明的 SQL_DRIVER_HDESC 或 SQL_DRIVER_HSTMT 描述符。）  
  
 如果*InfoValuePtr*为 NULL， *StringLengthPtr*仍将返回的 （不包括字符数据的 null 终止字符） 的字节总数可用于返回指向的缓冲区中*InfoValuePtr*。  
  
 *BufferLength*  
 [输入]长度\* *InfoValuePtr*缓冲区。 如果中的值* \*InfoValuePtr*不是字符串或如果*InfoValuePtr*是 null 指针， *BufferLength*忽略自变量。 该驱动程序假定的大小* \*InfoValuePtr* SQLUSMALLINT 或 SQLUINTEGER，基于*信息类型*。 如果* \*InfoValuePtr*为 Unicode 字符串 (在调用时**SQLGetInfoW**)，则*BufferLength*参数必须为偶数; 如果不是，SQLSTATE HY090 （返回字符串或缓冲区长度无效）。  
  
 *StringLengthPtr*  
 [输出]指向要返回的 （不包括字符数据的 null 终止字符） 的字节总数在其中缓冲区的指针可用于返回在 **InfoValuePtr*。  
  
 对于字符数据，可用于返回的字节数是否大于或等于*BufferLength*中的信息\* *InfoValuePtr*截断为*BufferLength*减 null 终止的长度的字节字符，且是由驱动程序以 null 结尾。  
  
 对于所有其他类型的数据的值*BufferLength*将被忽略，并且该驱动程序假定的大小\* *InfoValuePtr*是 SQLUSMALLINT 或 SQLUINTEGER，具体取决于*信息类型*。  
  
## <a name="return-value"></a>返回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetInfo**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可通过调用获取关联的 SQLSTATE 值**SQLGetDiagRec**与*HandleType*的SQL_HANDLE_DBC 和*处理*的*ConnectionHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLGetInfo**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|缓冲区\* *InfoValuePtr*不是否足够大以返回所有请求的信息。 因此，信息已被截断。 在中返回其未截断的窗体中的请求信息的长度 **StringLengthPtr*。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08003|连接未打开|(DM) 中请求的信息类型*信息类型*需要打开的连接。 通过 ODBC 保留的信息类型，可以打开连接的情况下返回仅 SQL_ODBC_VER。|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已连接到数据源之间的通信链接。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中* \*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY010|函数序列错误|(DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*并返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY024|无效属性值|(DM)*信息类型*自变量为 SQL_DRIVER_HSTMT，和指向的值*InfoValuePtr*不是有效的语句句柄。<br /><br /> (DM)*信息类型*自变量为 SQL_DRIVER_HDESC，和指向的值*InfoValuePtr*不是有效的描述符句柄。|  
|HY090|字符串或缓冲区长度无效|(DM) 参数指定的值*BufferLength*小于 0。<br /><br /> (DM) 为指定的值*BufferLength*为奇数，和* \*InfoValuePtr*属于 Unicode 数据类型。|  
|HY096|超出范围的信息类型|为参数指定的值*信息类型*对 ODBC 驱动程序支持的版本无效。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选字段|为参数指定的值*信息类型*是驱动程序不支持一个特定于驱动程序的值。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 的驱动程序对应于*ConnectionHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 在"信息类型中，"更高版本中此部分，则列出了当前定义的信息类型预计的详细信息将定义以利用不同数据源。 ODBC; 保留一系列的信息类型驱动程序开发人员必须保留用于 Open Group 自己特定于驱动程序使用的值。 **SQLGetInfo**不执行任何 Unicode 的转换或*形式转换*(请参阅[附录 a: ODBC 错误代码](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)的*ODBC 程序员参考*) 为驱动程序定义*信息类型*。 有关详细信息，请参阅[特定于驱动程序的数据类型、 描述符类型、 信息类型、 诊断类型和属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。 在返回的信息的格式\* *InfoValuePtr*取决于*信息类型*请求。 **SQLGetInfo**将五个不同的格式之一返回信息：  
  
-   以 null 结尾的字符串  
  
-   SQLUSMALLINT 值  
  
-   SQLUINTEGER 位掩码  
  
-   SQLUINTEGER 值  
  
-   SQLUINTEGER 二进制值  
  
 每个以下的信息类型的格式将其记录在该类型的说明。 应用程序必须强制转换中返回的值 **InfoValuePtr*相应地。 有关如何应用程序无法检索数据，从 SQLUINTEGER 位掩码的示例，请参阅"代码示例"。  
  
 驱动程序必须返回每个定义下表中的信息类型的值。 如果信息类型不适用于在驱动程序或数据源，该驱动程序将返回下表中列出的值之一。  
  
 字符串 （"Y"或"N"）  
 "N"  
  
 字符串 （不"Y"或"N"）  
 空字符串  
  
 SQLUSMALLINT  
 0  
  
 SQLUINTEGER 位掩码或 SQLUINTEGER 二进制值  
 0 L  
  
 例如，如果数据源不支持过程， **SQLGetInfo**返回的值的下表中列出的值*信息类型*中相关的过程。  
  
 SQL_PROCEDURES  
 "N"  
  
 SQL_ACCESSIBLE_PROCEDURES  
 "N"  
  
 SQL_MAX_PROCEDURE_NAME_LEN  
 0  
  
 SQL_PROCEDURE_TERM  
 空字符串  
  
 **SQLGetInfo**返回 SQLSTATE HY096 （无效的参数值） 的值*信息类型*，位于由 ODBC，保留待使用的信息类型的范围，但未定义的 ODBC 驱动程序支持的版本。 若要确定哪个版本的 ODBC 驱动程序已符合，应用程序调用**SQLGetInfo** SQL_DRIVER_ODBC_VER 信息类型。 **SQLGetInfo**返回 SQLSTATE HYC00 （未实现的可选功能） 的值*信息类型*，保留供特定于驱动程序使用的信息类型的范围中但不是支持驱动程序。  
  
 对所有调用**SQLGetInfo**要求连接为打开，除非*信息类型*是 SQL_ODBC_VER，返回的版本的驱动程序管理器。  
  
## <a name="information-types"></a>信息类型  
 本部分列出支持的信息类型**SQLGetInfo**。 信息类型可明确分组，并按字母顺序列出。 已添加或重命名为 ODBC 3 的信息类型*.x*还会列出。  
  
## <a name="driver-information"></a>驱动程序信息  
 以下值的*信息类型*参数返回的 ODBC 驱动程序，如活动语句、 数据源名称和接口标准符合性级别的数量有关的信息：  
  
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
>  在实现时**SQLGetInfo**，驱动程序可以通过最小化的信息进行发送或从服务器请求的次数来提高性能。  
  
## <a name="dbms-product-information"></a>DBMS 产品信息  
 以下值的*信息类型*参数返回有关 DBMS 产品，例如 DBMS 名称和版本的信息：  
  
 SQL_DATABASE_NAMESQL_DBMS_NAMESQL_DBMS_VER  
  
## <a name="data-source-information"></a>数据源信息  
 以下值的*信息类型*参数返回有关数据源，如光标特征和事务功能的信息：  
  
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
 以下值的*信息类型*参数返回有关数据源所支持的 SQL 语句的信息。 这些信息类型所述的每个功能的 SQL 语法是 SQL 92 语法。 这些信息类型不彻底描述整个 SQL 92 语法。 相反，它们描述了数据源通常提供不同级别的支持的语法的那些部分。 具体而言，涵盖大部分 SQL 92 中的 DDL 语句。  
  
 应用程序应确定一般级别的支持的语法从 SQL_SQL_CONFORMANCE 信息类型，并使用其他信息类型来确定从规定的标准符合性级别的变体。  
  
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
 以下值的*信息类型*自变量返回应用于标识符和子句在 SQL 语句中，例如标识符和最大选择列表中的列数的最大长度的限制信息。 由驱动程序或数据源，可以施加限制。  
  
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
  
## <a name="scalar-function-information"></a>标量函数信息  
 以下值的*信息类型*参数返回有关数据源和驱动程序支持的标量函数的信息。 有关标量函数的详细信息，请参阅[附录 e： 标量函数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)。  
  
|||  
|-|-|  
|SQL_CONVERT_FUNCTIONS|SQL_TIMEDATE_ADD_INTERVALS|  
|SQL_NUMERIC_FUNCTIONS|SQL_TIMEDATE_DIFF_INTERVALS|  
|SQL_STRING_FUNCTIONS|SQL_TIMEDATE_FUNCTIONS|  
|SQL_SYSTEM_FUNCTIONS||  
  
## <a name="conversion-information"></a>转换信息  
 以下值的*信息类型*参数返回的数据源可以具有指定的 SQL 数据类型转换到 SQL 数据类型的列表**转换**标量函数：  
  
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
  
## <a name="information-types-added-for-odbc-3x"></a>信息类型添加适用于 ODBC 3.x  
 以下值的*信息类型*自变量中添加了 ODBC 3*.x*:  
  
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
  
## <a name="information-types-renamed-for-odbc-3x"></a>适用于 ODBC 重命名的信息类型 3.x  
 以下值的*信息类型*ODBC 3 已重命名自变量*.x*。  
  
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
  
## <a name="information-types-deprecated-in-odbc-3x"></a>ODBC 中不推荐使用的信息类型 3.x  
 以下值的*信息类型*ODBC 3 中已弃用参数*.x*。 ODBC 3*.x*驱动程序必须继续为了向后兼容 ODBC 2 支持这些信息类型*.x*应用程序。 (有关这些类型的详细信息，请参阅[SQLGetInfo 支持](../../../odbc/reference/appendixes/sqlgetinfo-support.md)为了向后兼容的附录 g： 驱动程序准则中。)  
  
|||  
|-|-|  
|SQL_FETCH_DIRECTION|SQL_POS_OPERATIONS|  
|SQL_LOCK_TYPES|SQL_POSITIONED_STATEMENTS|  
|SQL_ODBC_API_CONFORMANCE|SQL_SCROLL_CONCURRENCY|  
|SQL_ODBC_SQL_CONFORMANCE|SQL_STATIC_SENSITIVITY|  
  
## <a name="information-type-descriptions"></a>信息类型说明  
 下表按字母顺序列出了每种信息类型，在其中引入它，ODBC 和其描述的版本。  
  
 SQL_ACCESSIBLE_PROCEDURES (ODBC 1.0)  
 字符串:"Y"，如果用户可以执行返回的所有过程**SQLProcedures**;"N"如果可能有过程返回用户无法执行。  
  
 SQL_ACCESSIBLE_TABLES (ODBC 1.0)  
 字符串:"Y"如果保证用户**选择**对返回的所有表特权**SQLTables**;"N"如果可能有表返回，用户无法访问。  
  
 SQL_ACTIVE_ENVIRONMENTS (ODBC 3.0)  
 一个 SQLUSMALLINT 值，指定驱动程序可以支持的活动环境最大数目。 如果没有指定的限制或限制为未知，则将此值设置为零。  
  
 SQL_AGGREGATE_FUNCTIONS (ODBC 3.0)  
 枚举对聚合函数的支持 SQLUINTEGER 位掩码：  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 SQL 92 条目级别 – 符合的驱动程序将始终返回所有这些选项支持。  
  
 SQL_ALTER_DOMAIN (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**ALTER 域**语句，如 SQL 92，支持的数据源中定义。 完整 sql-92 的兼容级别 – 驱动程序将始终返回所有位掩码。 返回值为"0"意味着**ALTER 域**不支持语句。  
  
 从该处必须支持此功能的 SQL 92 或 FIPS 一致性级别显示在每个位掩码旁边的括号中。  
  
 以下的位掩码用于确定支持哪些子句：  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = 的添加支持域约束 （完全级别）  
  
 SQL_AD_ADD_DOMAIN_DEFAULT = \<alter 域 > \<set 域默认子句 > 支持 （完全级别）  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION =\<约束名称定义子句 > 支持命名域约束 （中间级别）  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT =\<放置域 constraint 子句 > 支持 （完全级别）  
  
 SQL_AD_DROP_DOMAIN_DEFAULT = \<alter 域 >\<放置域默认子句 > 支持 （完全级别）  
  
 以下 bits 指定支持\<约束属性 > 如果\<添加域约束 > 支持 （SQL_AD_ADD_DOMAIN_CONSTRAINT 位设置）：  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE （完全级别） SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE （完全级别） SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED （完全级别） SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE （完全级别）  
  
 SQL_ALTER_TABLE (ODBC 2.0)  
 枚举中的子句 SQLUINTEGER 位掩码**ALTER TABLE**数据源所支持的语句。  
  
 从该处必须支持此功能的 SQL 92 或 FIPS 一致性级别显示在每个位掩码旁边的括号中。  
  
 以下的位掩码用于确定支持哪些子句：  
  
 SQL_AT_ADD_COLUMN_COLLATION =\<添加列 > 支持子句，设施来指定列的排序规则 （完全级别） 与 (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT =\<添加列 > 支持子句，与设施来指定列的默认值 （FIPS 过渡等级） (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_SINGLE =\<添加列 > 是支持 （FIPS 过渡等级） (ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT =\<添加列 > 支持子句，与设施来指定列约束 （FIPS 过渡等级） (ODBC 3.0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT =\<添加表约束 > 支持子句 （FIPS 过渡等级） (ODBC 3.0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION =\<约束名称定义 > 命名列和表约束 （中间级别） 支持 (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_CASCADE =\<拖放列 > 支持级联 （FIPS 过渡等级） (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT = \<alter 列 >\<拖放列默认子句 > 是支持 （中间级别） (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT =\<拖放列 > 支持限制 （FIPS 过渡等级） (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT =\<拖放列 > 支持限制 （FIPS 过渡等级） (ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT = \<alter 列 > \<set 列默认子句 > 是支持 （中间级别） (ODBC 3.0)  
  
 以下 bits 指定的支持\<约束属性 > 如果支持指定列或表的约束 （SQL_AT_ADD_CONSTRAINT 位设置）：  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED （完全级别） (ODBC 3.0) SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE （完全级别） (ODBC 3.0) SQL_AT_CONSTRAINT_DEFERRABLE （完全级别） (ODBC 3.0) SQL_AT_CONSTRAINT_NON_DEFERRABLE （完全级别） (ODBC 3.0)  
  
 SQL_ASYNC_DBC_FUNCTIONS (ODBC 3.8)  
 一个 SQLUINTEGER 值，该值指示是否驱动程序可以执行的函数以异步方式连接句柄。  
  
 SQL_ASYNC_DBC_CAPABLE = 驱动程序可以异步方式执行连接函数。  
  
 SQL_ASYNC_DBC_NOT_CAPABLE = 驱动程序可以不会以异步方式执行连接函数。  
  
 SQL_ASYNC_MODE (ODBC 3.0)  
 SQLUINTEGER 值，该值指示的驱动程序中的异步支持级别：  
  
 SQL_AM_CONNECTION = 支持级别的异步执行的连接。 与给定的连接句柄关联的所有语句句柄都处于异步模式，或者都都在同步模式下。 在连接上的语句句柄不能为异步模式中，同一个连接上的另一个语句句柄时在同步模式下，反之亦然。  
  
 SQL_AM_STATEMENT = 支持级别的异步执行的语句。 在同步模式下同一个连接上的其他语句句柄时，在异步模式下，可以是与连接句柄关联的某些语句句柄。  
  
 SQL_AM_NONE = 异步不支持模式。  
  
 SQL_ASYNC_NOTIFICATION  
 一个 SQLUINTEGER 值，该值指示该驱动程序是否支持异步通知：  
  
-   **SQL_ASYNC_NOTIFICATION_CAPABLE**由驱动程序支持异步执行通知。  
  
-   **SQL_ASYNC_NOTIFICATION_NOT_CAPABLE**驱动程序不支持异步执行通知。  
  
 有两个类别的 ODBC 异步操作： 连接级别的异步操作和语句级别异步操作。  如果驱动程序返回 SQL_ASYNC_NOTIFICATION_CAPABLE，它可以异步方式执行的所有 Api 都必须都支持通知。  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 枚举方面的行的可用性驱动程序的行为的 SQLUINTEGER 位掩码对进行计数。 以下的位掩码可以与信息类型一起使用：  
  
 SQL_BRC_ROLLED_UP = 行计数的连续的 INSERT、 DELETE 或 UPDATE 语句进行汇总成一个。 如果未设置此位，行计数是可用于每个语句。  
  
 SQL_BRC_PROCEDURES = 行计数，如果任何，当某一批处理执行存储过程中时才可用。 如果行计数都不可用，则它们可以回滚向上或单独可用，具体取决于 SQL_BRC_ROLLED_UP 位。  
  
 SQL_BRC_EXPLICIT = 行计数，如果任何，可用时直接通过调用执行批处理**SQLExecute**或**SQLExecDirect**。 如果行计数都不可用，则它们可以回滚向上或单独可用，具体取决于 SQL_BRC_ROLLED_UP 位。  
  
 SQL_BATCH_SUPPORT (ODBC 3.0)  
 枚举对于批处理的驱动程序的支持 SQLUINTEGER 位掩码。 以下的位掩码用于确定支持哪些级别：  
  
 SQL_BS_SELECT_EXPLICIT = 驱动程序支持显式批处理可以具有结果集生成语句。  
  
 SQL_BS_ROW_COUNT_EXPLICIT = 可以具有行计数生成语句的驱动程序支持显式批。  
  
 SQL_BS_SELECT_PROC = 的驱动程序支持显式过程可以具有结果集生成语句。  
  
 SQL_BS_ROW_COUNT_PROC = 可以具有行计数生成语句的驱动程序支持显式过程。  
  
 SQL_BOOKMARK_PERSISTENCE (ODBC 2.0)  
 枚举通过该书签保留操作 SQLUINTEGER 位掩码。  
  
 以下的位掩码可以与标志一起使用，以确定通过该选项书签保留：  
  
 SQL_BP_CLOSE = 后应用程序调用书签将变为有效**SQLFreeStmt**使用 SQL_CLOSE 选项，或**SQLCloseCursor**以关闭与语句关联的光标。  
  
 SQL_BP_DELETE = 书签的行在该行已被删除后有效。  
  
 SQL_BP_DROP = 后应用程序调用书签将变为有效**SQLFreeHandle**与*HandleType*的 SQL_HANDLE_STMT 删除一条语句。  
  
 SQL_BP_TRANSACTION = 应用程序提交或回滚事务后，书签将变为有效。  
  
 SQL_BP_UPDATE = 书签的行在该行中的任何列已更新，包括键列后有效。  
  
 SQL_BP_OTHER_HSTMT = 与某个关联的书签语句可以用于另一个语句。 除非指定 SQL_BP_CLOSE 或 SQL_BP_DROP，则将光标放在第一个语句必须打开。  
  
 SQL_CATALOG_LOCATION (ODBC 2.0)  
 SQLUSMALLINT 值，该值指示该目录中的限定的表名的位置：  
  
 SQL_CL_STARTSQL_CL_END  
  
 例如，Xbase 驱动程序返回 SQL_CL_START，因为目录 （目录） 名称的表名称，如下所示 \EMPDATA\EMP 开头。DBF。 ORACLE 服务器驱动程序返回 SQL_CL_END，因为该目录位于末尾的表名，作为ADMIN.EMP@EMPDATA。  
  
 SQL 92 完全级别 – 符合的驱动程序将始终返回 SQL_CL_START。 如果目录不支持数据源，则返回值为 0。 若要确定是否支持目录，应用程序调用**SQLGetInfo** SQL_CATALOG_NAME 信息类型。  
  
 这*信息类型*已重命名为 ODBC 3.0 从 ODBC 2.0*信息类型*SQL_QUALIFIER_LOCATION。  
  
 SQL_CATALOG_NAME (ODBC 3.0)  
 字符串:"Y"，如果服务器支持目录名称或"N"，如果它不存在。  
  
 SQL 92 完全级别 – 符合的驱动程序将始终返回"Y"。  
  
 SQL_CATALOG_NAME_SEPARATOR (ODBC 1.0)  
 字符串： 的字符或数据源定义为目录名称和之后或它前面的限定的名称元素之间的分隔符的字符。  
  
 如果目录不支持数据源，则返回空字符串。 若要确定是否支持目录，应用程序调用**SQLGetInfo** SQL_CATALOG_NAME 信息类型。 SQL 92 完全级别 – 符合的驱动程序将始终返回"。"。  
  
 这*信息类型*已重命名为 ODBC 3.0 从 ODBC 2.0*信息类型*SQL_QUALIFIER_NAME_SEPARATOR。  
  
 SQL_CATALOG_TERM (ODBC 1.0)  
 具有目录; 数据源供应商的名称的字符串例如，"数据库"或者"directory"。 此字符串可以在右上、 较低，还是混合大小写。  
  
 如果目录不支持数据源，则返回空字符串。 若要确定是否支持目录，应用程序调用**SQLGetInfo** SQL_CATALOG_NAME 信息类型。 SQL 92 完全级别 – 符合的驱动程序将始终返回"目录"。  
  
 这*信息类型*已重命名为 ODBC 3.0 从 ODBC 2.0*信息类型*SQL_QUALIFIER_TERM。  
  
 SQL_CATALOG_USAGE (ODBC 2.0)  
 枚举可在其中使用目录的语句 SQLUINTEGER 位掩码。  
  
 以下的位掩码用于确定可以使用目录的位置：  
  
 SQL_CU_DML_STATEMENTS = 目录支持所有的数据操作语言语句中：**选择**，**插入**，**更新**，**删除**，并且支持，**选择更新**和定位 update 和 delete 语句。  
  
 SQL_CU_PROCEDURE_INVOCATION = 目录支持 ODBC 过程调用语句。  
  
 SQL_CU_TABLE_DEFINITION = 目录中所有表定义语句支持： **CREATE TABLE**， **CREATE VIEW**， **ALTER TABLE**， **DROP TABLE**，和**放视图**。  
  
 SQL_CU_INDEX_DEFINITION = 目录中所有索引定义语句支持： **CREATE INDEX**和**DROP INDEX**。  
  
 SQL_CU_PRIVILEGE_DEFINITION = 目录支持所有权限定义语句中：**授予**和**撤消**。  
  
 如果目录不支持数据源，则返回值为 0。 若要确定是否支持目录，应用程序调用**SQLGetInfo** SQL_CATALOG_NAME 信息类型。 SQL 92 完全级别 – 符合的驱动程序将始终返回所有设置这些位的位掩码。  
  
 这*信息类型*已重命名为 ODBC 3.0 从 ODBC 2.0*信息类型*SQL_QUALIFIER_USAGE。  
  
 SQL_COLLATION_SEQ (ODBC 3.0)  
 排序规则序列的名称。 这是一个字符字符串，指示用于此服务器的默认字符集的默认排序规则的名称 (例如，ISO 8859-1 或 EBCDIC)。 如果这是未知的则将返回空字符串。 SQL 92 完全级别 – 符合的驱动程序将始终返回非空字符串。  
  
 SQL_COLUMN_ALIAS (ODBC 2.0)  
 字符串:"Y"，如果数据源支持列别名;否则为"N"。  
  
 列别名是可以通过使用 AS 子句指定选择列表中某一列的备用名称。 SQL 92 条目级别 – 符合的驱动程序将始终返回"Y"。  
  
 SQL_CONCAT_NULL_BEHAVIOR (ODBC 1.0)  
 SQLUSMALLINT 值，该值指示数据源如何处理空值的串联值具有非 NULL 值的字符数据类型列的字符数据类型列：  
  
 SQL_CB_NULL = 结果为 NULL 值。  
  
 SQL_CB_NON_NULL = 结果为非 NULL 值的列或列的串联。  
  
 SQL 92 条目级别 – 符合的驱动程序将始终返回 SQL_CB_NULL。  
  
 SQL_CONVERT_BIGINTSQL_CONVERT_BINARYSQL_CONVERT_BIT SQL_CONVERT_CHAR SQL_CONVERT_GUIDSQL_CONVERT_DATESQL_CONVERT_DECIMALSQL_CONVERT_DOUBLESQL_CONVERT_FLOATSQL_CONVERT_INTEGERSQL_CONVERT_INTERVAL_YEAR_MONTHSQL_CONVERT_INTERVAL_DAY_TIMESQL_CONVERT_LONGVARBINARYSQL_CONVERT_LONGVARCHARSQL_CONVERT_NUMERICSQL_CONVERT_REALSQL_CONVERT_SMALLINTSQL_CONVERT_TIMESQL_CONVERT_TIMESTAMPSQL_CONVERT_TINYINTSQL_CONVERT_VARBINARYSQL_CONVERT_VARCHAR (ODBC 1.0)  
 SQLUINTEGER 位掩码。 位掩码指示数据源所支持的转换**转换**标量函数中指定类型的数据的*信息类型*。 如果位掩码等于零，则数据源不支持从数据在指定的类型，包括转换为相同的数据类型的任何转换。  
  
 例如，若要确定数据源是否支持 SQL_INTEGER 数据转换 SQL_BIGINT 数据类型，应用程序调用**SQLGetInfo**与*信息类型*SQL_CONVERT_INTEGER。 在应用程序执行**AND**使用返回的位掩码和 SQL_CVT_BIGINT 的操作。 如果生成的值不为零，则支持转换。  
  
 以下的位掩码用于确定支持哪些转换：  
  
 SQL_CVT_BIGINT (ODBC 1.0) SQL_CVT_BINARY (ODBC 1.0) SQL_CVT_BIT (ODBC 1.0) SQL_CVT_GUID (ODBC 3.5) SQL_CVT_CHAR (ODBC 1.0) SQL_CVT_DATE (ODBC 1.0) SQL_CVT_DECIMAL (ODBC 1.0) SQL_CVT_DOUBLE (ODBC 1.0) SQL_CVT_FLOAT (ODBC 1.0) SQL_CVT_INTEGER (ODBC 1.0) SQL_CVT_INTERVAL_YEAR_MONTH (ODBC 3.0) SQL_CVT_INTERVAL_DAY_TIME (ODBC 3.0) SQL_CVT_LONGVARBINARY (ODBC 1.0) SQL_CVT_LONGVARCHAR (ODBC 1.0) SQL_CVT_NUMERIC (ODBC 1.0) SQL_CVT_REAL ODBC 1.0) SQL_CVT_SMALLINT (ODBC 1.0) SQL_CVT_TIME (ODBC 1.0) SQL_CVT_时间戳 (ODBC 1.0) SQL_CVT_TINYINT (ODBC 1.0) SQL_CVT_VARBINARY (ODBC 1.0) SQL_CVT_VARCHAR (ODBC 1.0)  
  
 SQL_CONVERT_FUNCTIONS (ODBC 1.0)  
 枚举支持的驱动程序和关联的数据源的标量转换函数 SQLUINTEGER 位掩码。  
  
 以下的位掩码用于确定支持的转换函数：  
  
 SQL_FN_CVT_CASTSQL_FN_CVT_CONVERT  
  
 SQL_CORRELATION_NAME (ODBC 1.0)  
 SQLUSMALLINT 值，该值指示是否支持表相关名称：  
  
 SQL_CN_NONE = 不支持名称的相关。  
  
 SQL_CN_DIFFERENT = 的相关名称支持，但必须不同于它们表示的表的名称。  
  
 SQL_CN_ANY = 的相关名称支持和可以是任何有效的用户定义名称。  
  
 SQL 92 条目级别 – 符合的驱动程序将始终返回 SQL_CN_ANY。  
  
 SQL_CREATE_ASSERTION (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**创建断言**语句，如 SQL 92，支持的数据源中定义。  
  
 以下的位掩码用于确定支持哪些子句：  
  
 SQL_CA_CREATE_ASSERTION  
  
 以下 bits 指定支持的约束属性，如果支持显式指定约束属性的功能 （请参阅 SQL_ALTER_TABLE 和 SQL_CREATE_TABLE 信息类型）：  
  
 SQL_CA_CONSTRAINT_INITIALLY_DEFERREDSQL_CA_CONSTRAINT_INITIALLY_IMMEDIATESQL_CA_CONSTRAINT_DEFERRABLESQL_CA_CONSTRAINT_NON_DEFERRABLE  
  
 SQL 92 完全级别 – 符合的驱动程序将始终返回所有这些选项支持。 返回值为"0"意味着**创建断言**不支持语句。  
  
 SQL_CREATE_CHARACTER_SET (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**创建字符集**语句，如 SQL 92，支持的数据源中定义。  
  
 以下的位掩码用于确定支持哪些子句：  
  
 SQL_CCS_CREATE_CHARACTER_SETSQL_CCS_COLLATE_CLAUSESQL_CCS_LIMITED_COLLATION  
  
 SQL 92 完全级别 – 符合的驱动程序将始终返回所有这些选项支持。 返回值为"0"意味着**创建字符集**不支持语句。  
  
 SQL_CREATE_COLLATION (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**创建排序规则**语句，如 SQL 92，支持的数据源中定义。  
  
 以下的位掩码用于确定支持哪些子句：  
  
 SQL_CCOL_CREATE_COLLATION  
  
 支持的 SQL 92 完整级别 – 符合的驱动程序将始终会返回此选项。 返回值为"0"意味着**创建排序规则**不支持语句。  
  
 SQL_CREATE_DOMAIN (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**创建域**语句，如 SQL 92，支持的数据源中定义。  
  
 以下的位掩码用于确定支持哪些子句：  
  
 SQL_CDO_CREATE_DOMAIN = 创建域支持语句 （中间级别）。  
  
 SQL_CDO_CONSTRAINT_NAME_DEFINITION =\<约束名称定义 > 命名域约束 （中间级别） 的支持。  
  
 以下 bits 指定能够创建列约束： SQL_CDO_DEFAULT = 支持指定域的约束 （中间级别） SQL_CDO_CONSTRAINT = 支持指定域的默认值 （中间级别） SQL_CDO_COLLATION =指定域的排序规则支持 （完全级别）  
  
 以下 bits 指定支持的约束条件属性，如果支持指定域约束 （设置 SQL_CDO_DEFAULT）：  
  
 SQL_CDO_CONSTRAINT_INITIALLY_DEFERRED （完全级别） SQL_CDO_CONSTRAINT_INITIALLY_IMMEDIATE （完全级别） SQL_CDO_CONSTRAINT_DEFERRABLE （完全级别） SQL_CDO_CONSTRAINT_NON_DEFERRABLE （完全级别）  
  
 返回值为"0"意味着**创建域**不支持语句。  
  
 SQL_CREATE_SCHEMA (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**CREATE SCHEMA**语句，如 SQL 92，支持的数据源中定义。  
  
 以下的位掩码用于确定支持哪些子句：  
  
 SQL_CS_CREATE_SCHEMASQL_CS_AUTHORIZATIONSQL_CS_DEFAULT_CHARACTER_SET  
  
 SQL 92 中间级别 – 符合的驱动程序将始终返回 SQL_CS_CREATE_SCHEMA 和 SQL_CS_AUTHORIZATION 选项支持。 这些值还必须在 SQL 92 条目级别，但不是一定 SQL 语句支持。 SQL 92 完全级别 – 符合的驱动程序将始终返回所有这些选项支持。  
  
 SQL_CREATE_TABLE (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**CREATE TABLE**语句，如 SQL 92，支持的数据源中定义。  
  
 从该处必须支持此功能的 SQL 92 或 FIPS 一致性级别显示在每个位掩码旁边的括号中。  
  
 以下的位掩码用于确定支持哪些子句：  
  
 SQL_CT_CREATE_TABLE = CREATE TABLE 语句支持。 （入门级）  
  
 SQL_CT_TABLE_CONSTRAINT = 支持指定表约束 （FIPS 过渡等级）  
  
 SQL_CT_CONSTRAINT_NAME_DEFINITION =\<约束名称定义 > 子句支持命名列和表约束 （中间级别）  
  
 以下 bits 指定能够创建临时表：  
  
 SQL_CT_COMMIT_PRESERVE = 已删除行保留提交。 （完全级别）SQL_CT_COMMIT_DELETE = 已删除提交删除行。 （完全级别）SQL_CT_GLOBAL_TEMPORARY = 全局可以创建临时表。 （完全级别）SQL_CT_LOCAL_TEMPORARY = 本地可以创建临时表。 （完全级别）  
  
 以下 bits 指定能够创建列约束：  
  
 SQL_CT_COLUMN_CONSTRAINT = 支持指定列约束 （FIPS 过渡级别） SQL_CT_COLUMN_DEFAULT = 支持指定列的默认值 （FIPS 过渡级别） SQL_CT_COLUMN_COLLATION = 指定列的排序规则是支持 （完全级别）  
  
 如果支持指定列或表的约束，则以下 bits 指定支持的约束特性：  
  
 SQL_CT_CONSTRAINT_INITIALLY_DEFERRED （完全级别） SQL_CT_CONSTRAINT_INITIALLY_IMMEDIATE （完全级别） SQL_CT_CONSTRAINT_DEFERRABLE （完全级别） SQL_CT_CONSTRAINT_NON_DEFERRABLE （完全级别）  
  
 SQL_CREATE_TRANSLATION (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**创建翻译**语句，如 SQL 92，支持的数据源中定义。  
  
 以下的位掩码用于确定支持哪些子句：  
  
 SQL_CTR_CREATE_TRANSLATION  
  
 支持的 SQL 92 完整级别 – 符合的驱动程序将始终会返回这些选项。 返回值为"0"意味着**创建翻译**不支持语句。  
  
 SQL_CREATE_VIEW (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**CREATE VIEW**语句，如 SQL 92，支持的数据源中定义。  
  
 以下的位掩码用于确定支持哪些子句：  
  
 SQL_CV_CREATE_VIEWSQL_CV_CHECK_OPTIONSQL_CV_CASCADEDSQL_CV_LOCAL  
  
 返回值为"0"意味着**CREATE VIEW**不支持语句。  
  
 SQL 92 条目级别 – 符合的驱动程序将始终返回 SQL_CV_CREATE_VIEW 和 SQL_CV_CHECK_OPTION 选项支持。  
  
 SQL 92 完全级别 – 符合的驱动程序将始终返回所有这些选项支持。  
  
 SQL_CURSOR_COMMIT_BEHAVIOR (ODBC 1.0)  
 SQLUSMALLINT 值，该值指示如何**提交**操作影响游标和数据源 （数据源时提交事务时其行为） 中的已准备的语句。  
  
 此属性的值将反映的下一步的设置的当前状态： SQL_COPT_SS_PRESERVE_CURSORS。  
  
 SQL_CB_DELETE = 关闭游标，并删除已准备的语句。 若要使用光标同样，应用程序必须 reprepare 并重新执行该语句。  
  
 SQL_CB_CLOSE = 关闭游标。 对于已准备的语句，应用程序可以调用**SQLExecute**上而不调用语句**SQLPrepare**试。 SQL ODBC 驱动程序的默认值为 SQL_CB_CLOSE。 这意味着提交事务时，SQL ODBC 驱动程序将关闭你 cursor(s)。  
  
 SQL_CB_PRESERVE 像以前那样 = 保留在相同的位置的游标**提交**操作。 应用程序可以继续提取数据，也可以关闭游标重新执行语句，而无需重新做好准备。  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR (ODBC 1.0)  
 SQLUSMALLINT 值，该值指示如何**回滚**操作影响游标和数据源中的已准备的语句：  
  
 SQL_CB_DELETE = 关闭游标，并删除已准备的语句。 若要使用光标同样，应用程序必须 reprepare 并重新执行该语句。  
  
 SQL_CB_CLOSE = 关闭游标。 对于已准备的语句，应用程序可以调用**SQLExecute**上而不调用语句**SQLPrepare**试。  
  
 SQL_CB_PRESERVE 像以前那样 = 保留在相同的位置的游标**回滚**操作。 应用程序可以继续提取数据，也可以关闭游标重新语句执行而无需 repreparing 它。  
  
 SQL_CURSOR_SENSITIVITY (ODBC 3.0)  
 SQLUINTEGER 值，该值指示光标敏感度的支持：  
  
 SQL_INSENSITIVE = 所有游标语句句柄显示结果集不反映对它进行了任何更改的情况下上通过同一事务中的任何其他光标。  
  
 SQL_UNSPECIFIED = 它是未指定是否语句句柄上的游标请可见对结果集由同一事务中的另一个游标所做的更改。 语句句柄上的游标可能使可见 none、 几个或所有此类更改。  
  
 SQL_SENSITIVE = 游标是敏感到同一事务中的其他游标所做的更改。  
  
 SQL 92 条目级别 – 符合的驱动程序将始终返回 SQL_UNSPECIFIED 选项，因为支持。  
  
 SQL 92 完全级别 – 符合的驱动程序将始终返回 SQL_INSENSITIVE 选项，因为支持。  
  
 SQL_DATA_SOURCE_NAME (ODBC 1.0)  
 在连接过程中使用的数据源名称包含的字符字符串。 如果应用程序调用**SQLConnect**，它的值*szDSN*自变量。 如果应用程序调用**SQLDriverConnect**或**SQLBrowseConnect**，这是传递给该驱动程序的连接字符串中的 DSN 关键字的值。 如果连接字符串未包含**DSN**关键字 (例如当它包含**驱动程序**关键字)，这是一个空字符串。  
  
 SQL_DATA_SOURCE_READ_ONLY (ODBC 1.0)  
 一个字符串。 "Y"如果数据源设置为 READ ONLY 模式下，"N"，否则是否。  
  
 此特性仅属于数据源，然后重试。它不是使用户可以访问数据源驱动程序的特征。 为读/写的驱动程序可以用于的数据源是只读的。 如果驱动程序是只读的所有其数据源必须是只读的并且必须返回 SQL_DATA_SOURCE_READ_ONLY。  
  
 SQL_DATABASE_NAME (ODBC 1.0)  
 如果数据源定义一个命名的对象称为"数据库"，则将字符串字符替换为正在使用中，当前数据库的名称。  
  
> [!NOTE]  
>  ODBC 3 中*.x*，此返回的值*信息类型*还可以通过调用返回**SQLGetConnectAttr**与*属性*SQL_ATTR_CURRENT_CATALOG 自变量。  
  
 SQL_DATETIME_LITERALS (ODBC 3.0)  
 枚举数据源支持的 SQL 92 datetime 文本 SQLUINTEGER 位掩码。 请注意，这些是 sql-92 规范中列出的日期时间文字独立于 datetime 文字转义子句定义的 ODBC。 有关 ODBC datetime 文字转义子句的详细信息，请参阅[日期、 时间和时间戳文本](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)。  
  
 在下面的列表中的位的位掩码，FIPS 过渡级别 – 符合的驱动程序将始终返回"1"的值。 不支持 SQL 92 datetime 文本"0"表示的值。  
  
 以下的位掩码用于确定支持哪些文本：  
  
 SQL_DL_SQL92_DATESQL_DL_SQL92_TIMESQL_DL_SQL92_TIMESTAMPSQL_DL_SQL92_INTERVAL_YEARSQL_DL_SQL92_INTERVAL_MONTHSQL_DL_SQL92_INTERVAL_DAYSQL_DL_SQL92_INTERVAL_HOURSQL_DL_SQL92_INTERVAL_MINUTESQL_DL_SQL92_INTERVAL_SECONDSQL_DL_SQL92_INTERVAL_YEAR_TO_MONTHSQL_DL_SQL92_INTERVAL_DAY_TO_HOUR  
  
 SQL_DL_SQL92_INTERVAL_DAY_TO_MINUTESQL_DL_SQL92_INTERVAL_DAY_TO_SECONDSQL_DL_SQL92_INTERVAL_HOUR_TO_MINUTESQL_DL_SQL92_INTERVAL_HOUR_TO_SECONDSQL_DL_SQL92_INTERVAL_MINUTE_TO_SECOND  
  
 SQL_DBMS_NAME (ODBC 1.0)  
 带有驱动程序访问的 DBMS 产品名称的字符字符串。  
  
 SQL_DBMS_VER (ODBC 1.0)  
 指示由驱动程序访问的 DBMS 产品版本的字符字符串。 版本的格式为 # #。 # #。 # # #，其中前两个数字是否为主要版本，接下来的两位数字是次要版本，，最后四位数是发布版本。 该驱动程序必须呈现此窗体中的 DBMS 产品版本，但也可以附加的 DBMS 特定于产品的版本。 例如，"04.01.0000 Rdb 4.1"。  
  
 SQL_DDL_INDEX (ODBC 3.0)  
 SQLUINTEGER 值，该值指示对创建和删除的索引的支持：  
  
 SQL_DI_CREATE_INDEXSQL_DI_DROP_INDEX  
  
 SQL_DEFAULT_TXN_ISOLATION (ODBC 1.0)  
 一个 SQLUINTEGER 值，该值指示默认事务隔离级别支持驱动程序或数据源或为零的数据源不支持事务。 以下术语用于定义事务隔离级别：  
  
 **脏读**事务 1 更改行。 事务 2 在事务 1 提交更改之前读取已更改的行。 如果事务 1 回滚更改，则将具有事务 2 读取了被视为不存在的行。  
  
 **不可重复读取**事务 1 读取某行。 事务 2 更新或删除该行并提交此更改。 如果事务 1 尝试重新读取行时，它将接收不同的行值或发现该行已被删除。  
  
 **幽灵**事务 1 中读取一套满足某些搜索条件的行。 事务 2 生成一个或多个行 （通过插入或更新） 搜索条件相匹配。 如果事务 1 reexecutes 读取行的语句，它会收到一组不同的行。  
  
 如果数据源支持事务，该驱动程序将返回以下位掩码之一：  
  
 SQL_TXN_READ_UNCOMMITTED = 脏读、 不可重复读取和幻像还可能有。  
  
 SQL_TXN_READ_COMMITTED = Dirty 读取不可能。 也可能不可重复读取和幻像。  
  
 SQL_TXN_REPEATABLE_READ = Dirty 读取不可重复读取，而不可能。 幻像是可能的。  
  
 SQL_TXN_SERIALIZABLE = 事务是可序列化。 脏读、 不可重复读或幻像不允许可序列化事务。  
  
 SQL_DESCRIBE_PARAMETER (ODBC 3.0)  
 字符串:"Y"，如果可以描述参数;"N"，如果不是。  
  
 SQL 92 完全级别 – 符合的驱动程序通常将返回"Y"，因为它将支持**描述输入**语句。 因为这不直接指定基础 SQL 支持，但是，描述参数可能不支持，甚至中的 SQL 92 完全的级别 – 符合的驱动程序。  
  
 SQL_DM_VER (ODBC 3.0)  
 带有版本的驱动程序管理器中的字符字符串。 版本的格式为 # #。 # #。 # # #。 # # #，其中：  
  
 两个数字的第一个集是主要的 ODBC 版本，如通过常量 SQL_SPEC_MAJOR 给定。  
  
 两个数字另一组是次要的 ODBC 版本，如通过常量 SQL_SPEC_MINOR 给定。  
  
 四个数字的第三组是驱动程序管理器主要内部版本号。  
  
 设置的最后一个四位数字是驱动程序管理器的次要版本号。  
  
 Windows 7 驱动程序管理器版本为 03.80。 Windows 8 驱动程序管理器版本为 03.81。  
  
 SQL_DRIVER_AWARE_POOLING_SUPPORTED (ODBC 3.8)  
 SQLUINTEGER 值，该值指示如果驱动程序支持识别驱动程序的池。 (有关详细信息，请参阅[识别驱动程序的连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。  
  
 SQL_DRIVER_AWARE_POOLING_CAPABLE 指示该驱动程序可以支持识别驱动程序的池的机制。  
  
 SQL_DRIVER_AWARE_POOLING_NOT_CAPABLE 指示该驱动程序不能支持识别驱动程序的池的机制。  
  
 驱动程序不需要实现 SQL_DRIVER_AWARE_POOLING_SUPPORTED 和驱动程序管理器将不接受到驱动程序的返回值。  
  
 SQL_DRIVER_HDBCSQL_DRIVER_HENV (ODBC 1.0)  
 SQLULEN 值、 驱动程序的环境句柄或连接句柄，由自变量确定*信息类型*。  
  
 这些信息类型的驱动程序管理器单独实现。  
  
 SQL_DRIVER_HDESC (ODBC 3.0)  
 SQLULEN 值，由驱动程序管理器的描述符句柄，必须在输入中传递的驱动程序的描述符句柄\* *InfoValuePtr*从应用程序。 在这种情况下， *InfoValuePtr*是一个输入和输出参数。 输入的描述符句柄传递中\* *InfoValuePtr*必须具有显式或隐式上分配了*ConnectionHandle*。  
  
 应用程序应创建之前它将调用处理的驱动程序管理器的描述符副本**SQLGetInfo**与此信息类型，以确保句柄不覆盖输出。  
  
 此信息类型的驱动程序管理器单独实现。  
  
 SQL_DRIVER_HLIB (ODBC 2.0)  
 一个 SQLULEN 的值， *hinst*从负载库加载 Microsoft Windows 操作系统或它的等效项在另一个操作系统上的驱动程序 DLL 时返回到驱动程序管理器。 句柄是否仅对的调用中指定的连接句柄有效**SQLGetInfo**。  
  
 此信息类型的驱动程序管理器单独实现。  
  
 SQL_DRIVER_HSTMT (ODBC 1.0)  
 SQLULEN 值，由驱动程序管理器语句句柄，必须在输入中传递的驱动程序的语句句柄\* *InfoValuePtr*从应用程序。 在这种情况下， *InfoValuePtr*是输入和输出参数。 输入的语句句柄传递中\* *InfoValuePtr*必须已对的自变量分配*ConnectionHandle*。  
  
 应用程序应创建副本的驱动程序管理器的语句之前它将调用处理**SQLGetInfo**与此信息类型，以确保句柄不覆盖输出。  
  
 此信息类型的驱动程序管理器单独实现。  
  
 SQL_DRIVER_NAME (ODBC 1.0)  
 包含用于访问数据源驱动程序的文件名称的字符字符串。  
  
 SQL_DRIVER_ODBC_VER (ODBC 2.0)  
 具有 ODBC 驱动程序支持的版本字符串。 版本的格式为 # #。 # #，其中前两个数字是否为主要版本，接下来的两位数字是次要版本。 SQL_SPEC_MAJOR 和 SQL_SPEC_MINOR 定义的主版本号和次版本号。 有关本手册中所述的 ODBC 版本，这些是 3 和 0，，该驱动程序应返回"03.00"。  
  
 ODBC 驱动程序管理器不会修改 SQLGetInfo(SQL_DRIVER_ODBC_VER) 以保持向后的兼容现有应用程序的返回值。 该驱动程序指定将返回的值。 但是，支持 C 数据类型扩展的驱动程序必须返回 3.8 （或更高版本） 在应用程序调用**SQLSetEnvAttr**将 SQL_ATTR_ODBC_VERSION 设置为 3.8。 有关详细信息，请参阅[ODBC 中的 C 数据类型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
 SQL_DRIVER_VER (ODBC 1.0)  
 带有版本的驱动程序和驱动程序的说明 （可选） 的字符字符串。 最低限度的版本是窗体的 # #。 # #。 # # #，其中前两个数字是否为主要版本，接下来的两位数字是次要版本，，最后四位数是发布版本。  
  
 SQL_DROP_ASSERTION (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**删除断言**语句，如 SQL 92，支持的数据源中定义。  
  
 以下的位掩码用于确定支持哪些子句：  
  
 SQL_DA_DROP_ASSERTION  
  
 支持的 SQL 92 完整级别 – 符合的驱动程序将始终会返回此选项。  
  
 SQL_DROP_CHARACTER_SET (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**删除字符集**语句，如 SQL 92，支持的数据源中定义。  
  
 以下的位掩码用于确定支持哪些子句：  
  
 SQL_DCS_DROP_CHARACTER_SET  
  
 支持的 SQL 92 完整级别 – 符合的驱动程序将始终会返回此选项。  
  
 SQL_DROP_COLLATION (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**删除排序规则**语句，如 SQL 92，支持的数据源中定义。  
  
 以下的位掩码用于确定支持哪些子句：  
  
 SQL_DC_DROP_COLLATION  
  
 支持的 SQL 92 完整级别 – 符合的驱动程序将始终会返回此选项。  
  
 SQL_DROP_DOMAIN (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**删除域**语句，如 SQL 92，支持的数据源中定义。  
  
 以下的位掩码用于确定支持哪些子句：  
  
 SQL_DD_DROP_DOMAINSQL_DD_CASCADESQL_DD_RESTRICT  
  
 SQL 92 中间级别 – 符合的驱动程序将始终返回所有这些选项支持。  
  
 SQL_DROP_SCHEMA (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**DROP SCHEMA**语句，如 SQL 92，支持的数据源中定义。  
  
 以下的位掩码用于确定支持哪些子句：  
  
 SQL_DS_DROP_SCHEMASQL_DS_CASCADESQL_DS_RESTRICT  
  
 SQL 92 中间级别 – 符合的驱动程序将始终返回所有这些选项支持。  
  
 SQL_DROP_TABLE (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**DROP TABLE**语句，如 SQL 92，支持的数据源中定义。  
  
 以下的位掩码用于确定支持哪些子句：  
  
 SQL_DT_DROP_TABLESQL_DT_CASCADESQL_DT_RESTRICT  
  
 FIPS 过渡的级别 – 符合的驱动程序将始终返回所有这些选项支持。  
  
 SQL_DROP_TRANSLATION (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**删除转换**语句，如 SQL 92，支持的数据源中定义。  
  
 以下的位掩码用于确定支持哪些子句：  
  
 SQL_DTR_DROP_TRANSLATION  
  
 支持的 SQL 92 完整级别 – 符合的驱动程序将始终会返回此选项。  
  
 SQL_DROP_VIEW (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**DROP VIEW**语句，如 SQL 92，支持的数据源中定义。  
  
 以下的位掩码用于确定支持哪些子句：  
  
 SQL_DV_DROP_VIEWSQL_DV_CASCADESQL_DV_RESTRICT  
  
 FIPS 过渡的级别 – 符合的驱动程序将始终返回所有这些选项支持。  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 描述由驱动程序支持的动态游标属性 SQLUINTEGER 位掩码。 此位掩码包含属性，则第一个部分第二个子集，请参阅 SQL_DYNAMIC_CURSOR_ATTRIBUTES2。  
  
 以下的位掩码用于确定哪些属性受支持：  
  
 SQL_CA1_NEXT = A *FetchOrientation* SQL_FETCH_NEXT 参数支持对的调用中**SQLFetchScroll**当光标位于动态游标。  
  
 SQL_CA1_ABSOLUTE = *FetchOrientation* SQL_FETCH_FIRST、 SQL_FETCH_LAST 和 SQL_FETCH_ABSOLUTE 参数支持对的调用中**SQLFetchScroll**当光标位于动态游标。 （将提取的行集是独立于当前光标位置。）  
  
 SQL_CA1_RELATIVE = *FetchOrientation* SQL_FETCH_PRIOR 和 SQL_FETCH_RELATIVE 参数支持对的调用中**SQLFetchScroll**当光标位于动态游标。 （将提取的行集取决于当前光标位置。 请注意，这分开 SQL_FETCH_NEXT 因为在只进游标，支持仅 SQL_FETCH_NEXT。）  
  
 SQL_CA1_BOOKMARK = A *FetchOrientation* SQL_FETCH_BOOKMARK 参数支持对的调用中**SQLFetchScroll**当光标位于动态游标。  
  
 SQL_CA1_LOCK_EXCLUSIVE = A *LockType* SQL_LOCK_EXCLUSIVE 参数支持对的调用中**SQLSetPos**当光标位于动态游标。  
  
 SQL_CA1_LOCK_NO_CHANGE = A *LockType* SQL_LOCK_NO_CHANGE 参数支持对的调用中**SQLSetPos**当光标位于动态游标。  
  
 SQL_CA1_LOCK_UNLOCK = A *LockType* SQL_LOCK_UNLOCK 参数支持对的调用中**SQLSetPos**当光标位于动态游标。  
  
 SQL_CA1_POS_POSITION =*操作*SQL_POSITION 参数支持对的调用中**SQLSetPos**当光标位于动态游标。  
  
 SQL_CA1_POS_UPDATE =*操作*SQL_UPDATE 参数支持对的调用中**SQLSetPos**当光标位于动态游标。  
  
 SQL_CA1_POS_DELETE =*操作*SQL_DELETE 参数支持对的调用中**SQLSetPos**当光标位于动态游标。  
  
 SQL_CA1_POS_REFRESH =*操作*SQL_REFRESH 参数支持对的调用中**SQLSetPos**当光标位于动态游标。  
  
 SQL_CA1_POSITIONED_UPDATE = 的更新其中当前的 SQL 游标是动态游标时，支持语句。 （SQL 92 条目级别 – 符合的驱动程序将始终返回此选项支持。）  
  
 SQL_CA1_POSITIONED_DELETE = 删除其中当前的 SQL 游标是动态游标时，支持语句。 （SQL 92 条目级别 – 符合的驱动程序将始终返回此选项支持。）  
  
 SQL_CA1_SELECT_FOR_UPDATE = SELECT，光标位于动态游标时才支持更新 SQL 语句。 （SQL 92 条目级别 – 符合的驱动程序将始终返回此选项支持。）  
  
 SQL_CA1_BULK_ADD =*操作*SQL_ADD 参数支持对的调用中**SQLBulkOperations**当光标位于动态游标。  
  
 SQL_CA1_BULK_UPDATE_BY_BOOKMARK =*操作*SQL_UPDATE_BY_BOOKMARK 参数支持对的调用中**SQLBulkOperations**当光标位于动态游标。  
  
 SQL_CA1_BULK_DELETE_BY_BOOKMARK =*操作*SQL_DELETE_BY_BOOKMARK 参数支持对的调用中**SQLBulkOperations**当光标位于动态游标。  
  
 SQL_CA1_BULK_FETCH_BY_BOOKMARK =*操作*SQL_FETCH_BY_BOOKMARK 参数支持对的调用中**SQLBulkOperations**当光标位于动态游标。  
  
 SQL 92 中间级别 – 符合的驱动程序通常将返回 SQL_CA1_NEXT、 SQL_CA1_ABSOLUTE 和 SQL_CA1_RELATIVE 选项受支持，因为它支持通过嵌入提取 SQL 语句的可滚动游标。 因为这不能直接决定基础 SQL 支持，但是，可滚动游标可能不受支持，即使对于的 SQL 92 中间级别 – 符合的驱动程序。  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 描述由驱动程序支持的动态游标属性 SQLUINTEGER 位掩码。 此位掩码包含属性，则第二个部分第一个的子集，请参阅 SQL_DYNAMIC_CURSOR_ATTRIBUTES1。  
  
 以下的位掩码用于确定哪些属性受支持：  
  
 SQL_CA2_READ_ONLY_CONCURRENCY = 只读的支持动态游标，在允许任何更新。 （SQL_ATTR_CONCURRENCY 语句属性可以是 SQL_CONCUR_READ_ONLY 对于动态游标）。  
  
 SQL_CA2_LOCK_CONCURRENCY = 动态游标使用的最低级别的锁定不足以确保支持可更新的行。 （SQL_ATTR_CONCURRENCY 语句属性可以是 SQL_CONCUR_LOCK 对于动态游标。）这些锁必须与由 SQL_ATTR_TXN_ISOLATION 连接属性设置的事务隔离级别一致。  
  
 SQL_CA2_OPT_ROWVER_CONCURRENCY = 动态游标，支持使用乐观并发控制比较行版本。 （SQL_ATTR_CONCURRENCY 语句属性可以是 SQL_CONCUR_ROWVER 对于动态游标。）  
  
 SQL_CA2_OPT_VALUES_CONCURRENCY = 动态游标，支持使用乐观并发控制比较值。 （SQL_ATTR_CONCURRENCY 语句属性可以是 SQL_CONCUR_VALUES 对于动态游标。）  
  
 SQL_CA2_SENSITIVITY_ADDITIONS = Added 行是否可见为动态游标;光标可以滚动到这些行。 （这些行添加到光标处下是依赖于驱动程序的。）  
  
 SQL_CA2_SENSITIVITY_DELETIONS = 已删除行不再适用于动态游标，而不会离开在结果集中;"漏洞"动态游标滚动从已删除的行后，它不能返回到该行。  
  
 SQL_CA2_SENSITIVITY_UPDATES = 到行的更新是为动态游标; 可见如果动态游标从滚动，并返回对已更新行，则光标所返回的数据是更新的数据，而不是原始数据。  
  
 SQL_CA2_MAX_ROWS_SELECT = SQL_ATTR_MAX_ROWS 语句属性影响**选择**光标位于动态游标时的语句。  
  
 SQL_CA2_MAX_ROWS_INSERT = SQL_ATTR_MAX_ROWS 语句属性影响**插入**光标位于动态游标时的语句。  
  
 SQL_CA2_MAX_ROWS_DELETE = SQL_ATTR_MAX_ROWS 语句属性影响**删除**光标位于动态游标时的语句。  
  
 SQL_CA2_MAX_ROWS_UPDATE = SQL_ATTR_MAX_ROWS 语句属性影响**更新**光标位于动态游标时的语句。  
  
 SQL_CA2_MAX_ROWS_CATALOG = SQL_ATTR_MAX_ROWS 语句属性影响**目录**光标位于动态游标时结果集。  
  
 SQL_CA2_MAX_ROWS_AFFECTS_ALL = SQL_ATTR_MAX_ROWS 语句属性影响**选择**，**插入**，**删除**，和**更新**语句，和**目录**结果集，光标位于动态游标时。  
  
 SQL_CA2_CRC_EXACT = 准确行计数是可用的 SQL_DIAG_CURSOR_ROW_COUNT 诊断字段光标位于动态游标时。  
  
 SQL_CA2_CRC_APPROXIMATE = 近似行计数是可用的 SQL_DIAG_CURSOR_ROW_COUNT 诊断字段光标位于动态游标时。  
  
 SQL_CA2_SIMULATE_NON_UNIQUE = 驱动程序不模拟的保证是否定位更新或删除语句将影响只有一行时游标是动态游标;它由应用程序的负责确保这一点。 (如果语句会影响多个行， **SQLExecute**或**SQLExecDirect**返回 SQLSTATE 01001 [游标操作冲突]。)若要设置此行为，应用程序调用**SQLSetStmtAttr**与 SQL_ATTR_SIMULATE_CURSOR 属性设置为 SQL_SC_NON_UNIQUE。  
  
 SQL_CA2_SIMULATE_TRY_UNIQUE = 驱动程序尝试保证模拟定位的 update 或 delete 语句将影响只包含一行，光标位于动态游标时。 该驱动程序执行速度始终都此类语句中，即使它们可能会影响多个行，例如，当没有唯一键。 (如果语句会影响多个行， **SQLExecute**或**SQLExecDirect**返回 SQLSTATE 01001 [游标操作冲突]。)若要设置此行为，应用程序调用**SQLSetStmtAttr**与 SQL_ATTR_SIMULATE_CURSOR 属性设置为 SQL_SC_TRY_UNIQUE。  
  
 SQL_CA2_SIMULATE_UNIQUE = 驱动程序模拟的保证定位更新或删除语句将影响只包含一行，光标位于动态游标时。 如果该驱动程序无法保证这一点对于给定的语句， **SQLExecDirect**或**SQLPrepare**返回 SQLSTATE 01001 （游标操作冲突）。 若要设置此行为，应用程序调用**SQLSetStmtAttr**与 SQL_ATTR_SIMULATE_CURSOR 属性设置为 SQL_SC_UNIQUE。  
  
 SQL_EXPRESSIONS_IN_ORDERBY (ODBC 1.0)  
 字符串:"Y"，如果数据源支持中的表达式**ORDER BY**列表;"N"如果它不存在。  
  
 SQL_FILE_USAGE (ODBC 2.0)  
 SQLUSMALLINT 值，该值指示如何单层驱动程序直接处理数据源中的文件：  
  
 SQL_FILE_NOT_SUPPORTED = 驱动程序不是单层驱动程序。 例如，ORACLE 驱动程序是一个两层驱动程序。  
  
 SQL_FILE_TABLE = 单层驱动程序的视为文件数据源中为表。 例如，Xbase 驱动程序将每个 Xbase 文件视为一个表。  
  
 SQL_FILE_CATALOG = 为编录数据源中的单层驱动程序会将文件。 例如，Microsoft Access 驱动程序将每个 Microsoft Access 文件视为整个数据库。  
  
 应用程序可能会用于确定用户选择数据的方式。 例如，Xbase 用户通常将数据存储在文件中，而 ORACLE 和 Microsoft Access 的用户通常将数据视为存储在表中。  
  
 应用程序时用户选择 Xbase 数据源，无法显示 Windows**文件打开**通用对话框; 当用户选择 Microsoft Access 或 ORACLE 数据源，应用程序可以显示一个自定义**选择表**对话框。  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 描述由驱动程序支持的只进游标属性 SQLUINTEGER 位掩码。 此位掩码包含属性，则第一个部分第二个子集，请参阅 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2。  
  
 以下的位掩码用于确定哪些属性受支持：  
  
 SQL_CA1_NEXTSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 有关这些位掩码的说明，请参阅 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 （和替换"只进游标"对于"动态游标"中的详细说明）。  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 描述由驱动程序支持的只进游标属性 SQLUINTEGER 位掩码。 此位掩码包含属性，则第二个部分第一个的子集，请参阅 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1。  
  
 以下的位掩码用于确定哪些属性受支持：  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 有关这些位掩码的说明，请参阅 SQL_DYNAMIC_CURSOR_ATTRIBUTES2 （和替换"只进游标"对于"动态游标"中的详细说明）。  
  
 SQL_GETDATA_EXTENSIONS (ODBC 2.0)  
 枚举扩展 SQLUINTEGER 位掩码**SQLGetData**。  
  
 以下的位掩码可以与一起使用标志以确定有关驱动程序支持哪些常见扩展名**SQLGetData**:  
  
 SQL_GD_ANY_COLUMN = **SQLGetData**可以为任何未绑定列，包括上次绑定列之前调用。 请注意，必须按顺序的升序列号，除非 SQL_GD_ANY_ORDER，也会返回调用列。  
  
 SQL_GD_ANY_ORDER = **SQLGetData**可以调用未绑定列采用任何顺序。 请注意， **SQLGetData**后，可以调用仅对列上一次绑定列，除非 SQL_GD_ANY_COLUMN，也会返回。  
  
 SQL_GD_BLOCK = **SQLGetData**可以中 （其中的行集大小大于 1） 的数据块中的任意行的未绑定列定位到与该行后调用**SQLSetPos**。  
  
 SQL_GD_BOUND = **SQLGetData**可以调用绑定列，还未绑定的列。 驱动程序不能返回此值，除非它还返回 SQL_GD_ANY_COLUMN。  
  
 SQL_GD_OUTPUT_PARAMS = **SQLGetData**可以调用以返回输出参数值。 有关详细信息，请参阅[检索输出参数使用 SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
 **SQLGetData**需要返回数据只能从上一次绑定列之后, 发生的未绑定列递增列号的顺序调用，并且未按块，这些行中的行。  
  
 如果驱动程序支持书签 （固定长度或可变长度），则它必须支持调用**SQLGetData**列 0。 这种支持无论，都需要驱动程序返回到调用**SQLGetInfo**与 SQL_GETDATA_EXTENSIONS*信息类型*。  
  
 SQL_GROUP_BY (ODBC 2.0)  
 一个 SQLUSMALLINT 值，指定中的列之间的关系**GROUP BY**子句和选择列表中的非聚合的列：  
  
 SQL_GB_COLLATE = A **COLLATE**子句可以指定每个分组列的末尾。 (ODBC 3.0)  
  
 SQL_GB_NOT_SUPPORTED = **GROUP BY**子句不支持。 (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_EQUALS_SELECT = **GROUP BY**子句必须包含在选择列表中的所有非聚合的列。 它不能包含任何其他列。 例如，**选择部门，MAX(SALARY) 从员工组按部门**。 (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_CONTAINS_SELECT = **GROUP BY**子句必须包含在选择列表中的所有非聚合的列。 它可以包含不在选择列表中的列。 例如，**选择部门，MAX(SALARY) 从员工组按部门、 年龄**。 (ODBC 2.0)  
  
 SQL_GB_NO_RELATION = 中的列**GROUP BY**子句，但不相关的选择列表。 选择列表中的非组合、 非聚合列的含义是数据源而定。 例如，**选择部门，薪金从员工组按部门、 年龄**。 (ODBC 2.0)  
  
 SQL 92 条目级别 – 符合的驱动程序将始终返回 SQL_GB_GROUP_BY_EQUALS_SELECT 选项，因为支持。 SQL 92 完全级别 – 符合的驱动程序将始终返回 SQL_GB_COLLATE 选项，因为支持。 如果支持任何选项，则**GROUP BY**子句不支持数据源。  
  
 SQL_IDENTIFIER_CASE (ODBC 1.0)  
 SQLUSMALLINT 值，如下所示：  
  
 SQL_IC_UPPER = SQL 中的标识符不区分大小写，并且存储在系统目录中大写字母。  
  
 SQL_IC_LOWER = SQL 中的标识符不区分大小写，并且存储在系统目录中的小写。  
  
 SQL_IC_SENSITIVE = SQL 中的标识符区分大小写，并且存储在系统目录中的混合大小写。  
  
 SQL_IC_MIXED = SQL 中的标识符不区分大小写，并且存储在系统目录中的混合大小写。  
  
 由于 SQL 92 中的标识符永远不区分大小写，严格符合 SQL 92 （任何级别） 的驱动程序将永远不会返回 SQL_IC_SENSITIVE 选项，因为支持。  
  
 SQL_IDENTIFIER_QUOTE_CHAR (ODBC 1.0)  
 用作的带引号的起始和结束分隔符的字符字符串 （分隔）： 在 SQL 语句中的标识符。 （标识符作为参数传递给 ODBC 函数不需要用引号引起来。）如果数据源不支持带引号的标识符，则返回空白。  
  
 此字符串还可以用于连接属性 SQL_ATTR_METADATA_ID 设置为 SQL_TRUE 时用引号括起来目录函数自变量。  
  
 由于 SQL 92 中的标识符引号字符是双引号 （"） 的驱动程序符合严格到 SQL 92 将始终返回双引号字符。  
  
 SQL_INDEX_KEYWORDS (ODBC 3.0)  
 枚举中的 CREATE INDEX 语句由驱动程序支持的关键字 SQLUINTEGER 位掩码：  
  
 SQL_IK_NONE = 不支持任何关键字。  
  
 SQL_IK_ASC = ASC 支持关键字。  
  
 SQL_IK_DESC = DESC 支持关键字。  
  
 SQL_IK_ALL = 所有支持的关键字。  
  
 若要查看是否支持 CREATE INDEX 语句，应用程序调用**SQLGetInfo** SQL_DLL_INDEX 信息类型。  
  
 SQL_INFO_SCHEMA_VIEWS (ODBC 3.0)  
 枚举由驱动程序支持的视图中 INFORMATION_SCHEMA SQLUINTEGER 位掩码。 在中，视图和内容的 INFORMATION_SCHEMA 是 SQL 92 中定义。  
  
 从该处必须支持此功能的 SQL 92 或 FIPS 一致性级别显示在每个位掩码旁边的括号中。  
  
 以下的位掩码用于确定支持的视图：  
  
 SQL_ISV_ASSERTIONS = 标识由给定用户所拥有的目录的断言。 （完全级别）  
  
 SQL_ISV_CHARACTER_SETS = 的标识给定用户可以访问的目录的字符集。 （中间级别）  
  
 SQL_ISV_CHECK_CONSTRAINTS = 标识检查由给定用户所拥有的约束。 （中间级别）  
  
 SQL_ISV_COLLATIONS = 标识给定用户可以访问该目录的字符排序规则。 （完全级别）  
  
 SQL_ISV_COLUMN_DOMAIN_USAGE = 目录取决于目录中定义的域并由给定用户所拥有的标识列。 （中间级别）  
  
 SQL_ISV_COLUMN_PRIVILEGES = 标识均可为或授予通过给定用户的持久表中的列的权限。 （FIPS 过渡等级）  
  
 SQL_ISV_COLUMNS = 标识给定用户可以访问的持久表的列。 （FIPS 过渡等级）  
  
 SQL_ISV_CONSTRAINT_COLUMN_USAGE = 类似 CONSTRAINT_TABLE_USAGE 视图，请标识给定用户拥有的各种约束列。 （中间级别）  
  
 SQL_ISV_CONSTRAINT_TABLE_USAGE = 标识由约束的表 (引用、 唯一的和断言)，并由给定用户所拥有。 （中间级别）  
  
 SQL_ISV_DOMAIN_CONSTRAINTS = 标识给定用户可以访问的域约束 （的目录中的域）。 （中间级别）  
  
 SQL_ISV_DOMAINS = 域定义用户可以访问的目录中的标识。 （中间级别）  
  
 SQL_ISV_KEY_COLUMN_USAGE = 标识列的目录中定义由给定用户约束为键。 （中间级别）  
  
 SQL_ISV_REFERENTIAL_CONSTRAINTS = 标识给定用户拥有的引用约束。 （中间级别）  
  
 SQL_ISV_SCHEMATA = 标识给定用户拥有的架构。 （中间级别）  
  
 SQL_ISV_SQL_LANGUAGES = SQL 实现 SQL 一致性级别、 选项和方言支持的标识。 （中间级别）  
  
 SQL_ISV_TABLE_CONSTRAINTS = 标识给定用户拥有的表约束。 （中间级别）  
  
 SQL_ISV_TABLE_PRIVILEGES = 标识均可为或授予通过给定用户的持久表上的特权。 （FIPS 过渡等级）  
  
 SQL_ISV_TABLES = 持久表定义可以由给定用户访问的目录中的标识。 （FIPS 过渡等级）  
  
 SQL_ISV_TRANSLATIONS = 标识字符转换为可以由给定用户访问该目录。 （完全级别）  
  
 SQL_ISV_USAGE_PRIVILEGES = 使用权限可使用或由给定用户拥有的目录对象的标识。 （FIPS 过渡等级）  
  
 SQL_ISV_VIEW_COLUMN_USAGE = 在其的目录视图的列属于给定用户的标识依赖。 （中间级别）  
  
 SQL_ISV_VIEW_TABLE_USAGE = 在其的目录视图的表属于给定用户的标识依赖。 （中间级别）  
  
 SQL_ISV_VIEWS = 查看的表定义可以由给定用户访问此目录中的标识。 （FIPS 过渡等级）  
  
 SQL_INSERT_STATEMENT (ODBC 3.0)  
 SQLUINTEGER 位掩码，用于指示是否支持**插入**语句：  
  
 SQL_IS_INSERT_LITERALS  
  
 SQL_IS_INSERT_SEARCHED  
  
 SQL_IS_SELECT_INTO  
  
 SQL 92 条目级别 – 符合的驱动程序将始终返回所有这些选项支持。  
  
 SQL_INTEGRITY (ODBC 1.0)  
 字符串:"Y"，如果数据源支持完整性增强功能设施;"N"如果它不存在。  
  
 这*信息类型*已重命名为 ODBC 3.0 从 ODBC 2.0*信息类型*SQL_ODBC_SQL_OPT_IEF。  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 描述由驱动程序支持的键集游标属性 SQLUINTEGER 位掩码。 此位掩码包含属性，则第一个部分第二个子集，请参阅 SQL_KEYSET_CURSOR_ATTRIBUTES2。  
  
 以下的位掩码用于确定哪些属性受支持：  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 有关这些位掩码的说明，请参阅 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 （和替换"键集驱动游标"对于"动态游标"中的详细说明）。  
  
 SQL 92 中间级别 – 符合的驱动程序通常将返回 SQL_CA1_NEXT、 SQL_CA1_ABSOLUTE 和 SQL_CA1_RELATIVE 选项受支持，因为该驱动程序支持通过嵌入提取 SQL 语句的可滚动游标。 因为这不能直接决定基础 SQL 支持，但是，可滚动游标可能不受支持，即使对于的 SQL 92 中间级别 – 符合的驱动程序。  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 描述由驱动程序支持的键集游标属性 SQLUINTEGER 位掩码。 此位掩码包含属性，则第二个部分第一个的子集，请参阅 SQL_KEYSET_CURSOR_ATTRIBUTES1。  
  
 以下的位掩码用于确定哪些属性受支持：  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 有关这些位掩码的说明，请参阅 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 （和替换"键集驱动游标"对于"动态游标"中的详细说明）。  
  
 SQL_KEYWORDS (ODBC 2.0)  
 包含所有数据源 – 特定关键字的以逗号分隔列表的字符字符串。 此列表不包含特定于 ODBC 的关键字或数据源和 ODBC 所使用的关键字。 此列表表示所有保留的关键字;可互操作的应用程序不应在对象名称中使用这些单词。  
  
 有关 ODBC 关键字的列表，请参阅[保留关键字](../../../odbc/reference/appendixes/reserved-keywords.md)中[附录 c: SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。 **#Define**值 SQL_ODBC_KEYWORDS 包含 ODBC 关键字的以逗号分隔列表。  
  
 附录 c: SQL 语法  
  
 SQL_LIKE_ESCAPE_CLAUSE (ODBC 2.0)  
 字符串： 中的"Y"，如果数据源支持转义符，用于百分比字符 （%） 和下划线字符 (_)**如**谓词和驱动程序支持 ODBC 语法用于定义**如**谓词转义字符;"N"以其他方式。  
  
 SQL_MAX_ASYNC_CONCURRENT_STATEMENTS (ODBC 3.0)  
 一个 SQLUINTEGER 值，该驱动程序可以在给定的连接支持的异步模式中指定的最大活动并发语句数。 如果没有特定的限制或限制为未知，则此值为零。  
  
 SQL_MAX_BINARY_LITERAL_LEN (ODBC 2.0)  
 一个 SQLUINTEGER 值，指定的最大长度 (数字的十六进制字符，不包括文本前缀和后缀返回**SQLGetTypeInfo**) 的 SQL 语句中的二进制文本。 例如，二进制文本 0xFFAA 具有长度为 4。 如果无最大长度，或长度是未知的则将此值设置为零。  
  
 SQL_MAX_CATALOG_NAME_LEN (ODBC 1.0)  
 在数据源中指定的目录名称的最大长度 SQLUSMALLINT 值。 如果无最大长度，或长度是未知的则将此值设置为零。  
  
 FIPS 完全级别 – 符合的驱动程序将返回至少为 128。  
  
 这*信息类型*已重命名为 ODBC 3.0 从 ODBC 2.0*信息类型*SQL_MAX_QUALIFIER_NAME_LEN。  
  
 SQL_MAX_CHAR_LITERAL_LEN (ODBC 2.0)  
 一个 SQLUINTEGER 值，指定的最大长度 (字符，不包括文本前缀和后缀返回数**SQLGetTypeInfo**) 的 SQL 语句中的字符文本。 如果无最大长度，或长度是未知的则将此值设置为零。  
  
 SQL_MAX_COLUMN_NAME_LEN (ODBC 1.0)  
 在数据源中指定的一个列名称的最大长度 SQLUSMALLINT 值。 如果无最大长度，或长度是未知的则将此值设置为零。  
  
 FIPS 条目级别 – 符合的驱动程序将返回至少 18。 FIPS 中间级别 – 符合的驱动程序将返回至少为 128。  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY (ODBC 2.0)  
 指定列中允许的最大数目的 SQLUSMALLINT 值**GROUP BY**子句。 如果没有指定的限制或限制为未知，则将此值设置为零。  
  
 FIPS 条目级别 – 符合的驱动程序将返回至少为 6。 FIPS 中间级别 – 符合的驱动程序将返回至少 15。  
  
 SQL_MAX_COLUMNS_IN_INDEX (ODBC 2.0)  
 索引中指定的最大允许的列数 SQLUSMALLINT 值。 如果没有指定的限制或限制为未知，则将此值设置为零。  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY (ODBC 2.0)  
 指定列中允许的最大数目的 SQLUSMALLINT 值**ORDER BY**子句。 如果没有指定的限制或限制为未知，则将此值设置为零。  
  
 FIPS 条目级别 – 符合的驱动程序将返回至少为 6。 FIPS 中间级别 – 符合的驱动程序将返回至少 15。  
  
 SQL_MAX_COLUMNS_IN_SELECT (ODBC 2.0)  
 选择列表中，指定最大允许的列数 SQLUSMALLINT 值。 如果没有指定的限制或限制为未知，则将此值设置为零。  
  
 FIPS 条目级别 – 符合的驱动程序将返回至少 100。 FIPS 中间级别 – 符合的驱动程序将返回至少 250。  
  
 SQL_MAX_COLUMNS_IN_TABLE (ODBC 2.0)  
 一个 SQLUSMALLINT 值，指定表中的最大允许的列数。 如果没有指定的限制或限制为未知，则将此值设置为零。  
  
 FIPS 条目级别 – 符合的驱动程序将返回至少 100。 FIPS 中间级别 – 符合的驱动程序将返回至少 250。  
  
 SQL_MAX_CONCURRENT_ACTIVITIES (ODBC 1.0)  
 一个 SQLUSMALLINT 值，指定驱动程序可以支持用于连接的活动语句的最大数目。 如果它具有与字词"结果"的含义的行从挂起状态，结果为活动定义语句**选择**操作或通过受影响的行**插入**，**更新**，或**删除**的操作 （如行计数），或如果它处于 NEED_DATA 状态。 此值可以反映由驱动程序或数据源强加的限制。 如果没有指定的限制或限制为未知，则将此值设置为零。  
  
 这*信息类型*已重命名为 ODBC 3.0 从 ODBC 2.0*信息类型*SQL_ACTIVE_STATEMENTS。  
  
 SQL_MAX_CURSOR_NAME_LEN (ODBC 1.0)  
 一个 SQLUSMALLINT 值，指定在数据源中的游标名称的最大长度。 如果无最大长度，或长度是未知的则将此值设置为零。  
  
 FIPS 条目级别 – 符合的驱动程序将返回至少 18。 FIPS 中间级别 – 符合的驱动程序将返回至少为 128。  
  
 SQL_MAX_DRIVER_CONNECTIONS (ODBC 1.0)  
 一个 SQLUSMALLINT 值，指定的最大的驱动程序可以支持为环境的活动连接数。 此值可以反映由驱动程序或数据源强加的限制。 如果没有指定的限制或限制为未知，则将此值设置为零。  
  
 这*信息类型*已重命名为 ODBC 3.0 从 ODBC 2.0*信息类型*SQL_ACTIVE_CONNECTIONS。  
  
 SQL_MAX_IDENTIFIER_LEN (ODBC 3.0)  
 SQLUSMALLINT，该值指示数据源支持的用户定义名称的字符的最大大小。  
  
 FIPS 条目级别 – 符合的驱动程序将返回至少 18。 FIPS 中间级别 – 符合的驱动程序将返回至少为 128。  
  
 SQL_MAX_INDEX_SIZE (ODBC 2.0)  
 一个 SQLUINTEGER 值，指定最大允许在组合的字段的索引中的字节数。 如果没有指定的限制或限制为未知，则将此值设置为零。  
  
 SQL_MAX_PROCEDURE_NAME_LEN (ODBC 1.0)  
 在数据源中指定过程名称的最大长度 SQLUSMALLINT 值。 如果无最大长度，或长度是未知的则将此值设置为零。  
  
 SQL_MAX_ROW_SIZE (ODBC 2.0)  
 一个 SQLUINTEGER 值，指定表中的单个行的最大长度。 如果没有指定的限制或限制为未知，则将此值设置为零。  
  
 FIPS 条目级别 – 符合的驱动程序将返回至少 2000。 FIPS 中间级别 – 符合的驱动程序将返回至少 8,000。  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG (ODBC 3.0)  
 字符串:"Y"，如果为 SQL_MAX_ROW_SIZE 信息类型包括所有 SQL_LONGVARCHAR 和 SQL_LONGVARBINARY 列的长度的行; 中返回的最大行大小"N"以其他方式。  
  
 SQL_MAX_SCHEMA_NAME_LEN (ODBC 1.0)  
 在数据源中指定的架构名称的最大长度 SQLUSMALLINT 值。 如果无最大长度，或长度是未知的则将此值设置为零。  
  
 FIPS 条目级别 – 符合的驱动程序将返回至少 18。 FIPS 中间级别 – 符合的驱动程序将返回至少为 128。  
  
 这*信息类型*已重命名为 ODBC 3.0 从 ODBC 2.0*信息类型*SQL_MAX_OWNER_NAME_LEN。  
  
 SQL_MAX_STATEMENT_LEN (ODBC 2.0)  
 一个 SQLUINTEGER 值，指定 SQL 语句的最大长度 （字符数，包括空格）。 如果无最大长度，或长度是未知的则将此值设置为零。  
  
 SQL_MAX_TABLE_NAME_LEN (ODBC 1.0)  
 在数据源中指定表名称的最大长度 SQLUSMALLINT 值。 如果无最大长度，或长度是未知的则将此值设置为零。  
  
 FIPS 条目级别 – 符合的驱动程序将返回至少 18。 FIPS 中间级别 – 符合的驱动程序将返回至少为 128。  
  
 SQL_MAX_TABLES_IN_SELECT (ODBC 2.0)  
 指定表中允许的最大数目的 SQLUSMALLINT 值**FROM**子句**选择**语句。 如果没有指定的限制或限制为未知，则将此值设置为零。  
  
 FIPS 条目级别 – 符合的驱动程序将返回至少 15。 FIPS 中间级别 – 符合的驱动程序将返回至少 50。  
  
 SQL_MAX_USER_NAME_LEN (ODBC 2.0)  
 在数据源中指定的用户名称的最大长度 SQLUSMALLINT 值。 如果无最大长度，或长度是未知的则将此值设置为零。  
  
 SQL_MULT_RESULT_SETS (ODBC 1.0)  
 字符串:"Y"，如果数据源支持多个结果集，"N"，如果它不存在。  
  
 有关多个结果集的详细信息，请参阅[多个结果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 SQL_MULTIPLE_ACTIVE_TXN (ODBC 1.0)  
 字符串:"Y"，如果驱动程序支持在相同时，"N"的多个活动事务，如果只有一个事务随时可以处于活动状态。  
  
 返回此信息类型的信息不适用于在分布式事务的情况下。  
  
 SQL_NEED_LONG_DATA_LEN (ODBC 2.0)  
 字符串:"Y"，如果数据源需要该值之前的长整型数据值 （数据类型为 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或的长整型数据源 – 特定数据类型） 的长度发送到数据源，"N"中，如果它不存在。 有关详细信息，请参阅[SQLBindParameter 函数](../../../odbc/reference/syntax/sqlbindparameter-function.md)和[SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
 SQL_NON_NULLABLE_COLUMNS (ODBC 1.0)  
 指定数据源是否支持 NOT NULL 列中的 SQLUSMALLINT 值：  
  
 SQL_NNC_NULL = 所有列必须是可以为 null。  
  
 SQL_NNC_NON_NULL = 列不能为 null。 (数据源支持**NOT NULL**中的列约束**CREATE TABLE**语句。)  
  
 SQL 92 条目级别 – 符合的驱动程序将返回 SQL_NNC_NON_NULL。  
  
 SQL_NULL_COLLATION (ODBC 2.0)  
 指定 null 值在结果集中的排序其中 SQLUSMALLINT 值：  
  
 SQL_NC_END = null 值进行排序的结果集，而不考虑 ASC 或 DESC 关键字的末尾。  
  
 SQL_NC_HIGH = null 值进行排序的最高的结果集，具体取决于 ASC 或 DESC 关键字。  
  
 SQL_NC_LOW = null 值进行排序的结果集，具体取决于 ASC 或 DESC 关键字低的末尾。  
  
 SQL_NC_START = null 值进行排序的结果集，而不考虑 ASC 或 DESC 关键字开头。  
  
 SQL_NUMERIC_FUNCTIONS (ODBC 1.0)  
 注意： 在 ODBC 1.0; 中引入的信息类型每个位掩码都标有在其中引入的版本。  
  
 枚举支持的驱动程序和关联的数据源的标量数值函数 SQLUINTEGER 位掩码。  
  
 以下的位掩码用于确定支持的数值的函数：  
  
 SQL_FN_NUM_ABS (ODBC 1.0) SQL_FN_NUM_ACOS (ODBC 1.0) SQL_FN_NUM_ASIN (ODBC 1.0) SQL_FN_NUM_ATAN (ODBC 1.0) SQL_FN_NUM_ATAN2 (ODBC 1.0) SQL_FN_NUM_CEILING (ODBC 1.0) SQL_FN_NUM_COS (ODBC 1.0) SQL_FN_NUM_COT (ODBC 1.0) SQL_FN_NUM_DEGREES (ODBC 2.0) SQL_FN_NUM_EXP (ODBC 1.0) SQL_FN_NUM_FLOOR (ODBC 1.0) SQL_FN_NUM_LOG (ODBC 1.0) SQL_FN_NUM_LOG10 (ODBC 2.0) SQL_FN_NUM_MOD (ODBC 1.0) SQL_FN_NUM_PI (ODBC 1.0) SQL_FN_NUM_POWER (ODBC 2.0) SQL_FN_NUM_RADIANS (ODBC 2.0) SQL_FN_NUM_RAND (ODBC 1.0) SQL_FN_NUM_ROUND (ODBC 2.0) SQL_FN_NUM_SIGN (ODBC 1.0) SQL_FN_NUM_SIN (ODBC 1.0) SQL_FN_NUM_SQRT (ODBC 1.0) SQL_FN_NUM_TAN (ODBC 1.0) SQL_FN_NUM_TRUNCATE (ODBC 2.0)  
  
 SQL_ODBC_INTERFACE_CONFORMANCE (ODBC 3.0)  
 SQLUINTEGER 值，该值指示的级别 ODBC 3*.x*接口与相兼容的驱动程序。  
  
 SQL_OIC_CORE： 所有 ODBC 驱动程序的最低级别应遵守。 此级别包括基本接口元素，如连接函数、 准备和执行 SQL 语句的函数、 基本的结果集元数据函数、 基本的目录函数等。  
  
 SQL_OIC_LEVEL1: 级别包括在核心标准符合性级别功能，加上可滚动游标，书签，定位更新和删除，依次类推。  
  
 SQL_OIC_LEVEL2: 级别包括级别 1 标准符合性级别功能，加上高级的功能，如敏感游标;更新、 删除和刷新书签;存储的过程支持;主键和外键; 的目录函数多目录支持;等等。  
  
 有关详细信息，请参阅[界面一致性级别](../../../odbc/reference/develop-app/interface-conformance-levels.md)。  
  
 SQL_ODBC_VER (ODBC 1.0)  
 带有版本的 ODBC 驱动程序管理器相符的字符字符串。 版本的格式为 # #。 # #。 0000，其中前两个数字是否为主要版本，接下来的两位数是次要版本。 这被实现仅在驱动程序管理器。  
  
 SQL_OJ_CAPABILITIES (ODBC 2.01)  
 枚举类型的驱动程序和数据源所支持的外部联接 SQLUINTEGER 位掩码。 以下的位掩码用于确定哪些类型受支持：  
  
 SQL_OJ_LEFT = 左外部联接都受支持。  
  
 SQL_OJ_RIGHT = 右外部联接都受支持。  
  
 SQL_OJ_FULL = 完全外部联接都受支持。  
  
 SQL_OJ_NESTED = 嵌套支持外部联接。  
  
 SQL_OJ_NOT_ORDERED = 外部联接的 ON 子句中的名称不必与在其各自的表名称相同的顺序的列**外部联接**子句。  
  
 SQL_OJ_INNER = 内部表 （左外部联接中的右表） 或右外部联接左表还可用于在内部联接。 这不适用于完全外部联接，没有内部表。  
  
 SQL_OJ_ALL_COMPARISON_OPS = 比较运算符在 ON 子句可以是任何 ODBC 比较运算符。 如果未设置此位，则可以在外部联接中使用只有等号 （=） 比较运算符。  
  
 如果任何这些选项返回支持，不支持任何外部联接子句。  
  
 有关支持的 SELECT 语句中的关系的联接运算符的信息由 SQL 92 定义，请参阅 SQL_SQL92_RELATIONAL_JOIN_OPERATORS。  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT (ODBC 2.0)  
 字符串:"Y"如果中的列**ORDER BY**子句必须在选择列表中; 否则为"N"。  
  
 SQL_PARAM_ARRAY_ROW_COUNTS (ODBC 3.0)  
 枚举有关行的可用性的驱动程序的属性 SQLUINTEGER 中参数化执行计数。 具有以下值：  
  
 SQL_PARC_BATCH = 个人行计数是每个参数集的可用。 这是在概念上等效于生成一批 SQL 语句，一个用于设置数组中每个参数的驱动程序。 可以通过使用 SQL_PARAM_STATUS_PTR 描述符字段检索扩展的错误信息。  
  
 SQL_PARC_NO_BATCH = 没有只有一个行计数可用，这是整个数组的参数的语句执行后产生的累积行计数。 这是在概念上等效于将完整的参数数组以及语句视为一个原子单元。 错误的处理相同，就像执行一个语句。  
  
 SQL_PARAM_ARRAY_SELECTS (ODBC 3.0)  
 在参数化执行过程中设置 SQLUINTEGER 枚举有关结果的可用性的驱动程序的属性。 具有以下值：  
  
 SQL_PAS_BATCH = 没有一个结果集可用每个参数集。 这是在概念上等效于生成一批 SQL 语句，一个用于设置数组中每个参数的驱动程序。  
  
 SQL_PAS_NO_BATCH = 没有只有一个结果集可用，它表示累积的结果集的完整的数组的参数的语句执行后产生的。 这是在概念上等效于将完整的参数数组以及语句视为一个原子单元。  
  
 SQL_PAS_NO_SELECT = A 驱动程序不允许的结果集生成语句，才能执行的参数数组。  
  
 SQL_PROCEDURE_TERM (ODBC 1.0)  
 具有过程; 的数据源供应商的名称的字符串例如，"数据库过程"、"存储的过程"，"过程"、"包"存储的查询"。  
  
 SQL_PROCEDURES (ODBC 1.0)  
 字符串:"Y"，如果数据源支持过程和驱动程序支持 ODBC 过程调用语法;"N"以其他方式。  
  
 SQL_POS_OPERATIONS (ODBC 2.0)  
 枚举中的支持操作 SQLINTEGER 位掩码**SQLSetPos**。  
  
 以下的位掩码可以与标志一起使用，以确定支持哪些选项。  
  
 SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0)  
  
 SQL_QUOTED_IDENTIFIER_CASE (ODBC 2.0)  
 SQLUSMALLINT 值，如下所示：  
  
 SQL_IC_UPPER = 带引号 SQL 中的标识符不区分大小写，并且存储在系统目录中大写字母。  
  
 SQL_IC_LOWER = 带引号 SQL 中的标识符不区分大小写，并且存储在系统目录中的小写。  
  
 SQL_IC_SENSITIVE = 带引号 SQL 中的标识符区分大小写，并且存储在系统目录中的混合大小写。 （在符合 SQL 92 – 数据库中，带引号的标识符始终是区分大小写。）  
  
 SQL_IC_MIXED = 带引号 SQL 中的标识符不区分大小写，并且存储在系统目录中的混合大小写。  
  
 SQL 92 条目级别 – 符合的驱动程序将始终返回 SQL_IC_SENSITIVE。  
  
 SQL_ROW_UPDATES (ODBC 1.0)  
 字符串:"Y"，如果键集驱动或混合光标维护行版本或所有的值提取行，并因此可以检测对行所做的任何用户自上次提取行的任何更新。 （这仅适用于更新，不适用于删除或插入。）该驱动程序可以返回的行状态 SQL_ROW_UPDATED 标志数组时**SQLFetchScroll**调用。 否则为"N"。  
  
 SQL_SCHEMA_TERM (ODBC 1.0)  
 具有架构; 的数据源供应商的名称的字符串例如，"所有者"、"授权 ID"或者"架构"。  
  
 在上部、 较低，或混合的情况下，可以返回的字符串。  
  
 SQL 92 条目级别 – 符合的驱动程序将始终返回"架构"。  
  
 这*信息类型*已重命名为 ODBC 3.0 从 ODBC 2.0*信息类型*SQL_OWNER_TERM。  
  
 SQL_SCHEMA_USAGE (ODBC 2.0)  
 枚举可在其中使用架构的语句 SQLUINTEGER 位掩码：  
  
 SQL_SU_DML_STATEMENTS = 架构支持所有的数据操作语言语句中：**选择**，**插入**，**更新**，**删除**，并且支持，**选择更新**和定位 update 和 delete 语句。  
  
 SQL_SU_PROCEDURE_INVOCATION = ODBC 过程调用语句中支持的架构。  
  
 SQL_SU_TABLE_DEFINITION = 架构中所有表定义语句支持： **CREATE TABLE**， **CREATE VIEW**， **ALTER TABLE**， **DROP TABLE**，和**放视图**。  
  
 SQL_SU_INDEX_DEFINITION = 所有索引定义语句中支持的架构： **CREATE INDEX**和**DROP INDEX**。  
  
 SQL_SU_PRIVILEGE_DEFINITION = 所有特权定义语句中支持的架构：**授予**和**撤消**。  
  
 SQL 92 条目级别 – 符合的驱动程序将始终返回 SQL_SU_DML_STATEMENTS、 SQL_SU_TABLE_DEFINITION，和 SQL_SU_PRIVILEGE_DEFINITION 选项中，因为支持。  
  
 这*信息类型*已重命名为 ODBC 3.0 从 ODBC 2.0*信息类型*SQL_OWNER_USAGE。  
  
 SQL_SCROLL_OPTIONS (ODBC 1.0)  
 注意： 在 ODBC 1.0; 中引入的信息类型每个位掩码都标有在其中引入的版本。  
  
 枚举支持为可滚动游标的滚动选项 SQLUINTEGER 位掩码。  
  
 以下的位掩码用于确定支持哪些选项：  
  
 SQL_SO_FORWARD_ONLY = 向前滚动游标唯一。 (ODBC 1.0)  
  
 SQL_SO_STATIC = 数据在结果集是静态。 (ODBC 2.0)  
  
 SQL_SO_KEYSET_DRIVEN = 该驱动程序保存和密钥用于结果集中的每一行。 (ODBC 1.0)  
  
 SQL_SO_DYNAMIC = 驱动程序可以使每个行集中的行 （键集大小为行集的大小相同） 的密钥。 (ODBC 1.0)  
  
 SQL_SO_MIXED = 驱动程序可以使密钥的密钥集和由键集大小中的每一行大于行集大小。 光标位于键集驱动内键集和动态外键集。 (ODBC 1.0)  
  
 有关可滚动游标的信息，请参阅[可滚动游标](../../../odbc/reference/develop-app/scrollable-cursors.md)。  
  
 SQL_SEARCH_PATTERN_ESCAPE (ODBC 1.0)  
 指定的驱动程序支持作为允许使用的模式匹配元字符下划线 (_) 和百分号 （%） 中搜索模式的有效字符作为转义字符的字符字符串。 此转义字符仅适用于支持的搜索字符串这些目录函数自变量。 如果此字符串为空，该驱动程序不支持的搜索模式转义字符。  
  
 因为此信息类型不表示中的转义字符的常规支持**如**谓词，SQL 92 不包括此字符串的要求。  
  
 这*信息类型*仅限于目录函数。 有关用法的搜索模式字符串中的转义字符的说明，请参阅[模式值自变量](../../../odbc/reference/develop-app/pattern-value-arguments.md)。  
  
 SQL_SERVER_NAME (ODBC 1.0)  
 字符串与实际的数据源 – 特定服务器名称;当过程中使用数据源名称时有用**SQLConnect**， **SQLDriverConnect**，和**SQLBrowseConnect**。  
  
 SQL_SPECIAL_CHARACTERS (ODBC 2.0)  
 包含的所有特殊字符 （即 a 到 z、 A 到 Z、 0 到 9 和下划线以外的所有字符），可在标识符名称，例如表名称、 列名称或索引名称，请在数据源中的字符字符串。 例如，"#$^"。 如果某个标识符包含一个或多个这些字符，标识符必须是分隔的标识符。  
  
 SQL_SQL_CONFORMANCE (ODBC 3.0)  
 SQLUINTEGER 值，该值指示 SQL 92 驱动程序支持的级别：  
  
 SQL_SC_SQL92_ENTRY = 条目级别 sql-92 符合。  
  
 SQL_SC_FIPS127_2_TRANSITIONAL = FIPS 兼容的 127 2 过渡级别。  
  
 SQL_SC_SQL92_FULL = 完全级别符合 SQL 92。  
  
 SQL_SC_ SQL92_INTERMEDIATE = 中间级别 sql-92 符合。  
  
 SQL_SQL92_DATETIME_FUNCTIONS(ODBC 3.0)  
 枚举的驱动程序和关联的数据源支持的 datetime 标量函数，定义在 SQL 92 SQLUINTEGER 位掩码。  
  
 以下的位掩码用于确定支持的日期时间函数：  
  
 SQL_SDF_CURRENT_DATESQL_SDF_CURRENT_TIMESQL_SDF_CURRENT_TIMESTAMP  
  
 SQL_SQL92_FOREIGN_KEY_DELETE_RULE(ODBC 3.0)  
 枚举中的外键中支持的规则 SQLUINTEGER 位掩码**删除**语句，如 SQL 92 中定义。  
  
 以下的位掩码用于确定哪些子句支持的数据源：  
  
 SQL_SFKD_CASCADESQL_SFKD_NO_ACTIONSQL_SFKD_SET_DEFAULTSQL_SFKD_SET_NULL  
  
 FIPS 过渡的级别 – 符合的驱动程序将始终返回所有这些选项支持。  
  
 SQL_SQL92_FOREIGN_KEY_UPDATE_RULE(ODBC 3.0)  
 枚举中的外键中支持的规则 SQLUINTEGER 位掩码**更新**语句，如 SQL 92 中定义。  
  
 以下的位掩码用于确定哪些子句支持的数据源：  
  
 SQL_SFKU_CASCADESQL_SFKU_NO_ACTIONSQL_SFKU_SET_DEFAULTSQL_SFKU_SET_NULL  
  
 SQL 92 完全级别 – 符合的驱动程序将始终返回所有这些选项支持。  
  
 SQL_SQL92_GRANT(ODBC 3.0)  
 枚举中支持的子句 SQLUINTEGER 位掩码**授予**语句，如 SQL 92 中定义。  
  
 从该处必须支持此功能的 SQL 92 或 FIPS 一致性级别显示在每个位掩码旁边的括号中。  
  
 以下的位掩码用于确定哪些子句支持的数据源：  
  
 SQL_SG_DELETE_TABLE （入门级） SQL_SG_INSERT_COLUMN （中间级别） SQL_SG_INSERT_TABLE （入门级） SQL_SG_REFERENCES_TABLE （入门级） SQL_SG_REFERENCES_COLUMN （入门级） SQL_SG_SELECT_TABLE （入门级） SQL_SG_UPDATE_COLUMN (入门级） SQL_SG_UPDATE_TABLE （入门级） SQL_SG_USAGE_ON_DOMAIN （FIPS 过渡级别） SQL_SG_USAGE_ON_CHARACTER_SET （FIPS 过渡级别） SQL_SG_USAGE_ON_COLLATION （FIPS 过渡级别） SQL_SG_USAGE_ON_TRANSLATION (FIPS过渡级别） SQL_SG_WITH_GRANT_OPTION （入门级）  
  
 SQL_SQL92_NUMERIC_VALUE_FUNCTIONS(ODBC 3.0)  
 枚举受驱动程序和关联的数据源的数字值标量函数，定义在 SQL 92 SQLUINTEGER 位掩码。  
  
 以下的位掩码用于确定支持的数值的函数：  
  
 SQL_SNVF_BIT_LENGTHSQL_SNVF_CHAR_LENGTHSQL_SNVF_CHARACTER_LENGTHSQL_SNVF_EXTRACTSQL_SNVF_OCTET_LENGTHSQL_SNVF_POSITION  
  
 SQL_SQL92_PREDICATES(ODBC 3.0)  
 枚举中支持的谓词 SQLUINTEGER 位掩码**选择**语句，如 SQL 92 中定义。  
  
 从该处必须支持此功能的 SQL 92 或 FIPS 一致性级别显示在每个位掩码旁边的括号中。  
  
 以下的位掩码用于确定哪些选项支持的数据源：  
  
 SQL_SP_BETWEEN （入门级） SQL_SP_COMPARISON （入门级） SQL_SP_EXISTS （入门级） SQL_SP_IN （入门级） SQL_SP_ISNOTNULL （入门级） SQL_SP_ISNULL （入门级） SQL_SP_LIKE （入门级） SQL_SP_MATCH_FULL （完全级别） SQL_SP_MATCH_PARTIAL（完全级别）SQL_SP_MATCH_UNIQUE_FULL （完全级别） SQL_SP_MATCH_UNIQUE_PARTIAL （完全级别） SQL_SP_OVERLAPS （FIPS 过渡级别） SQL_SP_QUANTIFIED_COMPARISON （入门级） SQL_SP_UNIQUE （入门级）  
  
 SQL_SQL92_RELATIONAL_JOIN_OPERATORS(ODBC 3.0)  
 枚举中支持的关系的联接运算符 SQLUINTEGER 位掩码**选择**语句，如 SQL 92 中定义。  
  
 从该处必须支持此功能的 SQL 92 或 FIPS 一致性级别显示在每个位掩码旁边的括号中。  
  
 以下的位掩码用于确定哪些选项支持的数据源：  
  
 SQL_SRJO_CORRESPONDING_CLAUSE （中间级别） SQL_SRJO_CROSS_JOIN （完全级别） SQL_SRJO_EXCEPT_JOIN （中间级别） SQL_SRJO_FULL_OUTER_JOIN （中间级别） SQL_SRJO_INNER_JOIN （FIPS 过渡级别） SQL_SRJO_INTERSECT_JOIN（中间级别）SQL_SRJO_LEFT_OUTER_JOIN （FIPS 过渡级别） SQL_SRJO_NATURAL_JOIN （FIPS 过渡级别） SQL_SRJO_RIGHT_OUTER_JOIN （FIPS 过渡级别） SQL_SRJO_UNION_JOIN （完全级别）  
  
 SQL_SRJO_INNER_JOIN 指示是否支持**内部联接**语法，不适用于内部联接功能。 支持**内部联接**语法是 FIPS 过渡，而支持内部联接功能是**条目**。  
  
 SQL_SQL92_REVOKE(ODBC 3.0)  
 枚举中支持的子句 SQLUINTEGER 位掩码**撤消**语句，如 SQL 92，支持的数据源中定义。  
  
 从该处必须支持此功能的 SQL 92 或 FIPS 一致性级别显示在每个位掩码旁边的括号中。  
  
 以下的位掩码用于确定哪些子句支持的数据源：  
  
 SQL_SR_CASCADE （FIPS 过渡级别） SQL_SR_DELETE_TABLE （入门级） SQL_SR_GRANT_OPTION_FOR （中间级别） SQL_SR_INSERT_COLUMN （中间级别） SQL_SR_INSERT_TABLE （入门级） SQL_SR_REFERENCES_COLUMN （入门级） SQL_SR_REFERENCES_TABLE （入门级） SQL_SR_RESTRICT （FIPS 过渡级别） SQL_SR_SELECT_TABLE （入门级） SQL_SR_UPDATE_COLUMN （入门级） SQL_SR_UPDATE_TABLE （入门级） SQL_SR_USAGE_ON_DOMAIN （FIPS 过渡级别） SQL_SR_USAGE_ON_CHARACTER_SET （FIPS 过渡级别） SQL_SR_USAGE_ON_COLLATION （FIPS 过渡级别） SQL_SR_USAGE_ON_TRANSLATION （FIPS 过渡等级）  
  
 SQL_SQL92_ROW_VALUE_CONSTRUCTOR(ODBC 3.0)  
 枚举中支持的行值构造函数表达式 SQLUINTEGER 位掩码**选择**语句，如 SQL 92 中定义。 以下的位掩码用于确定哪些选项支持的数据源：  
  
 SQL_SRVC_VALUE_EXPRESSION SQL_SRVC_NULL SQL_SRVC_DEFAULT SQL_SRVC_ROW_SUBQUERY  
  
 SQL_SQL92_STRING_FUNCTIONS(ODBC 3.0)  
 枚举字符串标量函数支持的驱动程序和关联的数据源的 SQL 92 中定义 SQLUINTEGER 位掩码。  
  
 以下的位掩码用于确定支持的字符串函数：  
  
 SQL_SSF_CONVERTSQL_SSF_LOWERSQL_SSF_UPPERSQL_SSF_SUBSTRINGSQL_SSF_TRANSLATESQL_SSF_TRIM_BOTHSQL_SSF_TRIM_LEADINGSQL_SSF_TRIM_TRAILING  
  
 SQL_SQL92_VALUE_EXPRESSIONS(ODBC 3.0)  
 枚举支持，值表达式中 SQL 92 定义 SQLUINTEGER 位掩码。  
  
 从该处必须支持此功能的 SQL 92 或 FIPS 一致性级别显示在每个位掩码旁边的括号中。  
  
 以下的位掩码用于确定哪些选项支持的数据源：  
  
 SQL_SVE_CASE （中间级别） SQL_SVE_CAST （FIPS 过渡级别） SQL_SVE_COALESCE （中间级别） SQL_SVE_NULLIF （中间级别）  
  
 SQL_STANDARD_CLI_CONFORMANCE (ODBC 3.0)  
 枚举该驱动程序符合 CLI 标准的一个或多个标准 SQLUINTEGER 位掩码。 以下的位掩码用于确定驱动程序符合哪些级别：  
  
 SQL_SCC_XOPEN_CLI_VERSION1： 驱动程序遵守打开组 CLI 版本 1。  
  
 符合 ISO 92 CLI SQL_SCC_ISO92_CLI： 驱动程序。  
  
 SQL_STATIC_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 描述由驱动程序支持的静态游标属性 SQLUINTEGER 位掩码。 此位掩码包含属性，则第一个部分第二个子集，请参阅 SQL_STATIC_CURSOR_ATTRIBUTES2。  
  
 以下的位掩码用于确定哪些属性受支持：  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 有关这些位掩码的说明，请参阅 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 （和替换"静态游标"对于"动态游标"中的详细说明）。  
  
 SQL 92 中间级别 – 符合的驱动程序通常将返回 SQL_CA1_NEXT、 SQL_CA1_ABSOLUTE 和 SQL_CA1_RELATIVE 选项受支持，因为该驱动程序支持通过嵌入提取 SQL 语句的可滚动游标。 因为这不能直接决定基础 SQL 支持，但是，可滚动游标可能不受支持，即使对于的 SQL 92 中间级别 – 符合的驱动程序。  
  
 SQL_STATIC_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 描述由驱动程序支持的静态游标属性 SQLUINTEGER 位掩码。 此位掩码包含属性，则第二个部分第一个的子集，请参阅 SQL_STATIC_CURSOR_ATTRIBUTES1。  
  
 以下的位掩码用于确定哪些属性受支持：  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 有关这些位掩码的说明，请参阅 SQL_DYNAMIC_CURSOR_ATTRIBUTES2 （和替换"静态游标"对于"动态游标"中的详细说明）。  
  
 SQL_STRING_FUNCTIONS (ODBC 1.0)  
 注意： 在 ODBC 1.0; 中引入的信息类型每个位掩码都标有在其中引入的版本。  
  
 枚举支持的驱动程序和关联的数据源的标量字符串函数 SQLUINTEGER 位掩码。  
  
 以下的位掩码用于确定支持的字符串函数：  
  
 SQL_FN_STR_ASCII (ODBC 1.0) SQL_FN_STR_BIT_LENGTH (ODBC 3.0) SQL_FN_STR_CHAR (ODBC 1.0) SQL_FN_STR_CHAR_LENGTH (ODBC 3.0) SQL_FN_STR_CHARACTER_LENGTH (ODBC 3.0) SQL_FN_STR_CONCAT (ODBC 1.0) SQL_FN_STR_DIFFERENCE (ODBC 2.0) SQL_FN_STR_INSERT (ODBC1.0) SQL_FN_STR_LCASE (ODBC 1.0) SQL_FN_STR_LEFT (ODBC 1.0) SQL_FN_STR_LENGTH (ODBC 1.0) SQL_FN_STR_LOCATE (ODBC 1.0) SQL_FN_STR_LTRIM (ODBC 1.0) SQL_FN_STR_OCTET_LENGTH (ODBC 3.0) SQL_FN_STR_POSITION (ODBC 3.0) SQL_FN_STR_REPEAT (ODBC 1.0) SQL_FN_STR_REPLACE (ODBC 1.0) SQL_FN_STR_RIGHT (ODBC 1.0) SQL_FN_STR_RTRIM (ODBC 1.0) SQL_FN_STR_SOUNDEX (ODBC 2.0) SQL_FN_STR_SPACE (ODBC 2.0) SQL_FN_STR_SUBSTRING (ODBC 1.0) SQL_FN_STR_UCASE (ODBC 1.0)  
  
 如果应用程序可以调用**定位**具有标量函数*string_exp1*， *string_exp2*，和*启动*自变量、 驱动程序返回 SQL_FN_STR_LOCATE 位掩码。 如果应用程序可以调用具有唯一的定位标量函数*string_exp1*和*string_exp2*自变量，该驱动程序返回 SQL_FN_STR_LOCATE_2 位掩码。 完全支持的驱动程序**定位**标量函数返回这两个位掩码。  
  
 (有关详细信息，请参阅[字符串函数](../../../odbc/reference/appendixes/string-functions.md)附录 E 中"标量函数。")  
  
 SQL_SUBQUERIES (ODBC 2.0)  
 枚举支持子查询谓词 SQLUINTEGER 位掩码：  
  
 SQL_SQ_CORRELATED_SUBQUERIESSQL_SQ_COMPARISONSQL_SQ_EXISTSSQL_SQ_INSQL_SQ_QUANTIFIED  
  
 SQL_SQ_CORRELATED_SUBQUERIES 位掩码指示支持子查询的所有谓词都支持相关子查询。  
  
 SQL 92 条目级别 – 符合的驱动程序将始终返回在其中设置所有这些位的位掩码。  
  
 SQL_SYSTEM_FUNCTIONS (ODBC 1.0)  
 枚举支持的驱动程序和关联的数据源的标量系统函数 SQLUINTEGER 位掩码。  
  
 以下的位掩码用于确定支持的系统函数：  
  
 SQL_FN_SYS_DBNAMESQL_FN_SYS_IFNULLSQL_FN_SYS_USERNAME  
  
 SQL_TABLE_TERM (ODBC 1.0)  
 具有表; 数据源供应商的名称的字符串例如，"表"或者"文件"。  
  
 此字符串可以在右上、 较低，还是混合大小写。  
  
 SQL 92 条目级别 – 符合的驱动程序将始终返回"table"。  
  
 SQL_TIMEDATE_ADD_INTERVALS (ODBC 2.0)  
 枚举支持的驱动程序和关联的数据源对于 TIMESTAMPADD 标量函数的时间戳间隔 SQLUINTEGER 位掩码。  
  
 以下的位掩码用于确定支持哪些间隔：  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 FIPS 过渡的级别 – 符合的驱动程序将始终返回在其中设置所有这些位的位掩码。  
  
 SQL_TIMEDATE_DIFF_INTERVALS (ODBC 2.0)  
 枚举支持的驱动程序和关联的数据源对于 TIMESTAMPDIFF 标量函数的时间戳间隔 SQLUINTEGER 位掩码。  
  
 以下的位掩码用于确定支持哪些间隔：  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 FIPS 过渡的级别 – 符合的驱动程序将始终返回在其中设置所有这些位的位掩码。  
  
 SQL_TIMEDATE_FUNCTIONS (ODBC 1.0)  
 注意： 在 ODBC 1.0; 中引入的信息类型每个位掩码都标有在其中引入的版本。  
  
 枚举的标量的日期和时间函数的驱动程序和关联的数据源支持 SQLUINTEGER 位掩码。  
  
 以下的位掩码用于确定支持的日期和时间函数：  
  
 SQL_FN_TD_CURRENT_DATE ODBC 3.0) SQL_FN_TD_CURRENT_TIME (ODBC 3.0) SQL_FN_TD_CURRENT_TIMESTAMP (ODBC 3.0) SQL_FN_TD_CURDATE (ODBC 1.0) SQL_FN_TD_CURTIME (ODBC 1.0) SQL_FN_TD_DAYNAME (ODBC 2.0) SQL_FN_TD_DAYOFMONTH (ODBC 1.0) SQL_FN_TD_DAYOFWEEK (ODBC 1.0) SQL_FN_TD_DAYOFYEAR (ODBC 1.0) SQL_FN_TD_EXTRACT (ODBC 3.0) SQL_FN_TD_HOUR (ODBC 1.0) SQL_FN_TD_MINUTE (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0) SQL_FN_TD_MONTHNAME (ODBC 2.0) SQL_FN_TD_NOW (ODBC 1.0) SQL_FN_TD_QUARTER (ODBC 1.0) SQL_FN_TD_第二个 (ODBC 1.0) SQL_FN_TD_TIMESTAMPADD (ODBC 2.0) SQL_FN_TD_TIMESTAMPDIFF (ODBC 2.0) SQL_FN_TD_WEEK (ODBC 1.0) SQL_FN_TD_YEAR (ODBC 1.0)  
  
 SQL_TXN_CAPABLE (ODBC 1.0)  
 注意： 在 ODBC 1.0; 中引入的信息类型每个返回值都标有在其中引入的版本。  
  
 SQLUSMALLINT 值，描述在驱动程序或数据源中的事务支持：  
  
 SQL_TC_NONE = 不支持的事务。 (ODBC 1.0)  
  
 SQL_TC_DML = 事务可以包含仅数据操作语言 (DML) 语句 (**选择**，**插入**，**更新**，**删除**). 数据定义语言 (DDL) 语句事务原因遇到了错误。 (ODBC 1.0)  
  
 SQL_TC_DDL_COMMIT = 事务可以包含仅 DML 语句。 DDL 语句 (**CREATE TABLE**， **DROP INDEX**，依次类推) 遇到中事务原因要将其提交的事务。 (ODBC 2.0)  
  
 SQL_TC_DDL_IGNORE = 事务可以包含仅 DML 语句。 将忽略在事务中遇到的 DDL 语句。 (ODBC 2.0)  
  
 SQL_TC_ALL = 事务可以包含 DDL 语句和任何顺序中的 DML 语句。 (ODBC 1.0)  
  
 （由于 SQL 92 中所必需的事务的支持，则 SQL 92 符合的驱动程序 [任何级别] 将永远不会返回 SQL_TC_NONE。）  
  
 SQL_TXN_ISOLATION_OPTION (ODBC 1.0)  
 枚举驱动程序或数据源中可用的事务隔离级别 SQLUINTEGER 位掩码。  
  
 以下的位掩码可以与标志一起使用，以确定支持哪些选项：  
  
 SQL_TXN_READ_UNCOMMITTEDSQL_TXN_READ_COMMITTEDSQL_TXN_REPEATABLE_READSQL_TXN_SERIALIZABLE  
  
 有关这些隔离级别的说明，请参阅 SQL_DEFAULT_TXN_ISOLATION 的说明。  
  
 若要设置的事务隔离级别，应用程序调用**SQLSetConnectAttr**设置 SQL_ATTR_TXN_ISOLATION 属性。 有关详细信息，请参阅[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
 SQL 92 条目级别 – 符合的驱动程序将始终返回 SQL_TXN_SERIALIZABLE，因为支持。 FIPS 过渡级别 – 符合的驱动程序将始终返回所有这些选项支持。  
  
 SQL_UNION (ODBC 2.0)  
 枚举支持 SQLUINTEGER 位掩码**联合**子句：  
  
 SQL_U_UNION = 数据源支持**联合**子句。  
  
 SQL_U_UNION_ALL = 数据源支持**所有**中的关键字**联合**子句。 (**SQLGetInfo**在这种情况下返回 SQL_U_UNION 和 SQL_U_UNION_ALL。)  
  
 SQL 92 条目级别 – 符合的驱动程序将始终返回这两种选项支持。  
  
 SQL_USER_NAME (ODBC 1.0)  
 具有特定的数据库，可以不同于登录名中使用的名称字符串。  
  
 SQL_XOPEN_CLI_YEAR (ODBC 3.0)  
 指示与版本的 ODBC 驱动程序管理器完全遵循的 Open Group 规范的发布的年份的字符字符串。  
  
 SQL_ACCESSIBLE_PROCEDURES (ODBC 1.0)  
 字符串:"Y"，如果用户可以执行返回的所有过程**SQLProcedures**;"N"如果可能有过程返回用户无法执行。  
  
 SQL_ACCESSIBLE_TABLES (ODBC 1.0)  
 字符串:"Y"如果保证用户**选择**对返回的所有表特权**SQLTables**;"N"如果可能有表返回，用户无法访问。  
  
 SQL_ACTIVE_ENVIRONMENTS (ODBC 3.0)  
 一个 SQLUSMALLINT 值，指定驱动程序可以支持的活动环境最大数目。 如果没有指定的限制或限制为未知，则将此值设置为零。  
  
 SQL_AGGREGATE_FUNCTIONS (ODBC 3.0)  
 枚举对聚合函数的支持 SQLUINTEGER 位掩码：  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 SQL 92 条目级别 – 符合的驱动程序将始终返回所有这些选项支持。  
  
 SQL_ALTER_DOMAIN (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**ALTER 域**语句，如 SQL 92，支持的数据源中定义。 完整 sql-92 的兼容级别 – 驱动程序将始终返回所有位掩码。 返回值为"0"意味着**ALTER 域**不支持语句。  
  
 从该处必须支持此功能的 SQL 92 或 FIPS 一致性级别显示在每个位掩码旁边的括号中。  
  
 以下的位掩码用于确定支持哪些子句：  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = 的添加支持域约束 （完全级别）  
  
 SQL_AD_ADD_DOMAIN_DEFAULT = \<alter 域 > \<set 域默认子句 > 支持 （完全级别）  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION =\<约束名称定义子句 > 支持命名域约束 （中间级别）  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT =\<放置域 constraint 子句 > 支持 （完全级别）  
  
 SQL_AD_DROP_DOMAIN_DEFAULT = \<alter 域 >\<放置域默认子句 > 支持 （完全级别）  
  
 以下 bits 指定支持\<约束属性 > 如果\<添加域约束 > 支持 （SQL_AD_ADD_DOMAIN_CONSTRAINT 位设置）：  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE （完全级别） SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE （完全级别） SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED （完全级别） SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE （完全级别）  
  
 SQL_ALTER_TABLE (ODBC 2.0)  
 枚举中的子句 SQLUINTEGER 位掩码**ALTER TABLE**数据源所支持的语句。  
  
 从该处必须支持此功能的 SQL 92 或 FIPS 一致性级别显示在每个位掩码旁边的括号中。  
  
 以下的位掩码用于确定支持哪些子句：  
  
 SQL_AT_ADD_COLUMN_COLLATION =\<添加列 > 支持子句，设施来指定列的排序规则 （完全级别） 与 (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT =\<添加列 > 支持子句，与设施来指定列的默认值 （FIPS 过渡等级） (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_SINGLE =\<添加列 > 是支持 （FIPS 过渡等级） (ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT =\<添加列 > 支持子句，与设施来指定列约束 （FIPS 过渡等级） (ODBC 3.0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT =\<添加表约束 > 支持子句 （FIPS 过渡等级） (ODBC 3.0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION =\<约束名称定义 > 命名列和表约束 （中间级别） 支持 (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_CASCADE =\<拖放列 > 支持级联 （FIPS 过渡等级） (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT = \<alter 列 >\<拖放列默认子句 > 是支持 （中间级别） (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT =\<拖放列 > 支持限制 （FIPS 过渡等级） (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT =\<拖放列 > 支持限制 （FIPS 过渡等级） (ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT = \<alter 列 > \<set 列默认子句 > 是支持 （中间级别） (ODBC 3.0)  
  
 以下 bits 指定的支持\<约束属性 > 如果支持指定列或表的约束 （SQL_AT_ADD_CONSTRAINT 位设置）：  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED （完全级别） (ODBC 3.0) SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE （完全级别） (ODBC 3.0) SQL_AT_CONSTRAINT_DEFERRABLE （完全级别） (ODBC 3.0) SQL_AT_CONSTRAINT_NON_DEFERRABLE （完全级别） (ODBC 3.0)  
  
 SQL_ASYNC_MODE (ODBC 3.0)  
 SQLUINTEGER 值，该值指示的驱动程序中的异步支持级别：  
  
 SQL_AM_CONNECTION = 支持级别的异步执行的连接。 与给定的连接句柄关联的所有语句句柄都处于异步模式，或者都都在同步模式下。 在连接上的语句句柄不能为异步模式中，同一个连接上的另一个语句句柄时在同步模式下，反之亦然。  
  
 SQL_AM_STATEMENT = 支持级别的异步执行的语句。 而其他语句句柄上相同的连接是在同步模式下，在异步模式下，可以是与连接句柄关联的某些语句句柄。  
  
 SQL_AM_NONE = 异步不支持模式。  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 枚举方面的行的可用性驱动程序的行为 SQLUINTEGER 位掩码对进行计数。 以下的位掩码可以与信息类型一起使用：  
  
 SQL_BRC_ROLLED_UP = 行计数的连续的 INSERT、 DELETE 或 UPDATE 语句进行汇总成一个。 如果未设置此位，行计数是可用于每个语句。  
  
 SQL_BRC_PROCEDURES = 行计数，如果任何，当某一批处理执行存储过程中时才可用。 如果行计数都不可用，则它们可以回滚向上或单独可用，具体取决于 SQL_BRC_ROLLED_UP 位。  
  
 SQL_BRC_EXPLICIT = 行计数，如果任何，可用时直接通过调用执行批处理**SQLExecute**或**SQLExecDirect**。 如果行计数都不可用，则它们可以回滚向上或单独可用，具体取决于 SQL_BRC_ROLLED_UP 位。  
  
## <a name="example"></a>示例  
 **SQLGetInfo**为 SQLUINTEGER 位掩码中返回的支持的选项列表 **InfoValuePtr*。 每个选项的位掩码与标志一起使用，以确定是否支持的选项。  
  
 例如，应用程序可以使用以下代码来确定是否与连接关联的驱动程序支持的子字符串标量函数。  
  
 有关使用另一个示例**SQLGetInfo**，请参阅[SQLTables 函数](../../../odbc/reference/syntax/sqltables-function.md)。  
  
```  
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
  
 返回语句特性的设置  
 [SQLGetStmtAttr 函数](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)  
  
 返回有关数据源的数据类型信息  
 [SQLGetTypeInfo 函数](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)

