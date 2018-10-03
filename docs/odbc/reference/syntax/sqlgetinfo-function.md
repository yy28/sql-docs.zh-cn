---
title: SQLGetInfo 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2b56a96ce4796f8d4409b6b347b58870039e15d2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47666245"
---
# <a name="sqlgetinfo-function"></a>SQLGetInfo 函数
**符合性**  
 版本引入了： ODBC 1.0 标准符合性： ISO 92  
  
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
 [输入]类型的信息。  
  
 *InfoValuePtr*  
 [输出]指向在其中返回的信息的缓冲区的指针。 具体取决于*信息类型*请求，返回的信息将是以下值之一： 以 null 结尾的字符串、 SQLUSMALLINT 值、 SQLUINTEGER 位掩码，SQLUINTEGER 标志、 SQLUINTEGER 的二进制值，或Sqlulen 生成值。  
  
 如果*信息类型*自变量是 SQL_DRIVER_HDESC 或 SQL_DRIVER_HSTMT， *InfoValuePtr*参数进行输入和输出。 （请参阅后面的详细信息此函数说明的 SQL_DRIVER_HDESC 或 SQL_DRIVER_HSTMT 描述符。）  
  
 如果*InfoValuePtr*为 NULL， *StringLengthPtr*仍将返回的总字节数 （不包括字符数据的 null 终止字符） 可用于返回通过指向的缓冲区中*InfoValuePtr*。  
  
 *BufferLength*  
 [输入]长度\* *InfoValuePtr*缓冲区。 如果中的值 *\*InfoValuePtr*不是字符字符串或者如果*InfoValuePtr*为 null 指针*BufferLength*忽略参数。 驱动程序假定的大小 *\*InfoValuePtr* SQLUSMALLINT 或 SQLUINTEGER，基于*信息类型*。 如果 *\*InfoValuePtr*是 Unicode 字符串 (在调用时**SQLGetInfoW**)，则*BufferLength*参数必须为偶数; 如果不是，SQLSTATE HY090 （返回字符串或缓冲区长度无效）。  
  
 *StringLengthPtr*  
 [输出]指向用于返回的总字节数 （不包括字符数据的 null 终止字符） 的缓冲区可用于在返回 **InfoValuePtr*。  
  
 对于字符数据，可用来返回的字节数是否大于或等于*BufferLength*中的信息\* *InfoValuePtr*截断为*BufferLength* null 终止的长度减去字节字符，且是由驱动程序以 null 结尾。  
  
 对于所有其他类型的数据的值*BufferLength*将被忽略，并且该驱动程序假定的大小\* *InfoValuePtr*是 SQLUSMALLINT 或 SQLUINTEGER，具体取决于*信息类型*。  
  
## <a name="return-value"></a>返回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetInfo**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可以通过调用获取关联的 SQLSTATE 值**SQLGetDiagRec**与*HandleType*的SQL_HANDLE_DBC 和一个*处理*的*ConnectionHandle*。 下表列出了通常由返回的 SQLSTATE 值**SQLGetInfo** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|缓冲区\* *InfoValuePtr*是否不足够大以返回所有请求的信息。 因此，信息已被截断。 在返回的在其未截断的窗体中所需的信息长度 **StringLengthPtr*。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08003|连接未打开|(DM) 中所请求的信息的类型*信息类型*需要打开的连接。 保留的 ODBC 的信息类型，仅 SQL_ODBC_VER 可以返回没有打开的连接。|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY010|函数序列错误|（数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*和返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY024|属性值无效|（数据挖掘）*信息类型*参数为 SQL_DRIVER_HSTMT，和指向的值*InfoValuePtr*不是有效的语句句柄。<br /><br /> （数据挖掘）*信息类型*参数为 SQL_DRIVER_HDESC，和指向的值*InfoValuePtr*不是有效的描述符句柄。|  
|HY090|字符串或缓冲区长度无效|(DM) 为参数指定的值*BufferLength*小于 0。<br /><br /> (DM) 为指定的值*BufferLength*已为奇数，并 *\*InfoValuePtr*的 Unicode 数据类型。|  
|HY096|信息类型超出了范围|为参数指定的值*信息类型*对 ODBC 驱动程序支持的版本无效。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选字段|为参数指定的值*信息类型*是驱动程序不支持特定于驱动程序的值。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 对应的驱动程序*ConnectionHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 在"信息类型中，"更高版本中此部分，则显示当前定义的信息类型预计的详细信息将定义要充分利用不同的数据源。 由 ODBC; 保留一系列的信息类型驱动程序开发人员必须保留供从 Open Group 自己特定于驱动程序使用的值。 **SQLGetInfo**不执行任何 Unicode 转换或*形式转换*(请参阅[附录 a: ODBC 错误代码](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)的*ODBC 程序员参考*) 为驱动程序定义*信息类型*。 有关详细信息，请参阅[特定于驱动程序的数据类型、 描述符类型、 信息类型、 诊断类型和属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。 中返回的信息的格式\* *InfoValuePtr*取决于*信息类型*请求。 **SQLGetInfo**将五个不同的格式之一返回的信息：  
  
-   以 null 结尾的字符串  
  
-   SQLUSMALLINT 值  
  
-   SQLUINTEGER 位掩码  
  
-   SQLUINTEGER 值  
  
-   SQLUINTEGER 二进制值  
  
 每个以下的信息类型的格式将其记录在该类型的说明。 应用程序必须转换中返回的值 **InfoValuePtr*相应地。 应用程序如何从 SQLUINTEGER 位掩码无法检索数据的示例，请参阅"代码示例"。  
  
 驱动程序必须返回以下表中定义每种信息类型的值。 如果信息类型不适用于驱动程序或数据源，该驱动程序将返回下表中列出的值之一。  
  
 字符串 （"Y"或"N"）  
 "N"  
  
 字符串 （不"Y"或"N"）  
 空字符串  
  
 SQLUSMALLINT  
 0  
  
 SQLUINTEGER 位掩码或 SQLUINTEGER 二进制值  
 0L  
  
 例如，如果数据源不支持过程， **SQLGetInfo**返回的值的下表中列出的值*信息类型*与过程相关的。  
  
 SQL_PROCEDURES  
 "N"  
  
 SQL_ACCESSIBLE_PROCEDURES  
 "N"  
  
 SQL_MAX_PROCEDURE_NAME_LEN  
 0  
  
 SQL_PROCEDURE_TERM  
 空字符串  
  
 **SQLGetInfo**返回 SQLSTATE HY096 （无效的参数值） 的值*信息类型*，保留供 ODBC 的信息类型的范围内，但未定义的 ODBC 驱动程序支持的版本。 若要确定哪个版本的 ODBC 驱动程序符合，应用程序调用**SQLGetInfo** SQL_DRIVER_ODBC_VER 信息类型。 **SQLGetInfo**返回 SQLSTATE HYC00 （未实现的可选功能） 的值*信息类型*，保留供特定于驱动程序使用的信息类型的范围内，但不是支持驱动程序。  
  
 所有调用的**SQLGetInfo**需要打开连接，除非*信息类型*是 SQL_ODBC_VER，返回的版本的驱动程序管理器。  
  
## <a name="information-types"></a>信息类型  
 本部分列出了支持的信息类型**SQLGetInfo**。 信息类型可明确分组并按字母顺序列出。 已添加或重命名为 ODBC 3 的信息类型 *.x*还会列出。  
  
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
>  在实现时**SQLGetInfo**，驱动程序可以通过最小化发送或从服务器请求信息的次数来提高性能。  
  
## <a name="dbms-product-information"></a>DBMS 的产品信息  
 以下值的*信息类型*参数返回 DBMS 产品，例如 DBMS 名称和版本的信息：  
  
 SQL_DATABASE_NAMESQL_DBMS_NAMESQL_DBMS_VER  
  
## <a name="data-source-information"></a>数据源信息  
 以下值的*信息类型*参数返回有关数据源，例如游标特征和事务功能的信息：  
  
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
 以下值的*信息类型*参数返回数据源支持的 SQL 语句的信息。 描述这些信息类型的每个功能的 SQL 语法是 SQL-92 语法。 这些信息类型不会经过了全面介绍整个 SQL-92 语法。 相反，它们描述数据源通常会提供不同级别的支持的语法的那些部分。 具体而言，涵盖了大部分 SQL-92 中的 DDL 语句。  
  
 应用程序应确定一般级别的受支持语法从 SQL_SQL_CONFORMANCE 信息类型，并使用其他信息类型来确定从规定的标准符合性级别的变体。  
  
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
 以下值的*信息类型*参数返回有关应用于标识符和子句在 SQL 语句中，例如标识符和最大的选择列表中的列数的最大长度的限制的信息。 该驱动程序或数据源可以施加限制。  
  
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
 以下值的*信息类型*参数返回数据源和驱动程序支持的标量函数的信息。 有关标量函数的详细信息，请参阅[附录 e： 标量函数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)。  
  
|||  
|-|-|  
|SQL_CONVERT_FUNCTIONS|SQL_TIMEDATE_ADD_INTERVALS|  
|SQL_NUMERIC_FUNCTIONS|SQL_TIMEDATE_DIFF_INTERVALS|  
|SQL_STRING_FUNCTIONS|SQL_TIMEDATE_FUNCTIONS|  
|SQL_SYSTEM_FUNCTIONS||  
  
## <a name="conversion-information"></a>转换信息  
 以下值的*信息类型*参数返回的数据源可以将具有指定的 SQL 数据类型转换到 SQL 数据类型列表**转换**标量函数：  
  
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
 以下值的*信息类型*参数中添加了 ODBC 3 *.x*:  
  
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
  
## <a name="information-types-renamed-for-odbc-3x"></a>信息类型重命名为 ODBC 3.x  
 以下值的*信息类型*ODBC 3 已重命名自变量 *.x*。  
  
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
  
## <a name="information-types-deprecated-in-odbc-3x"></a>在 ODBC 中已过时的信息类型 3.x  
 以下值的*信息类型*ODBC 3 中已弃用参数 *.x*。 ODBC 3 *.x*驱动程序必须继续支持使用这些信息类型进行向后兼容的 ODBC 2 *.x*应用程序。 (有关这些类型的详细信息，请参阅[SQLGetInfo 支持](../../../odbc/reference/appendixes/sqlgetinfo-support.md)中向后兼容性的附录 g： 驱动程序指南。)  
  
|||  
|-|-|  
|SQL_FETCH_DIRECTION|SQL_POS_OPERATIONS|  
|SQL_LOCK_TYPES|SQL_POSITIONED_STATEMENTS|  
|SQL_ODBC_API_CONFORMANCE|SQL_SCROLL_CONCURRENCY|  
|SQL_ODBC_SQL_CONFORMANCE|SQL_STATIC_SENSITIVITY|  
  
## <a name="information-type-descriptions"></a>信息的类型说明  
 下表按字母顺序列出了每种信息类型、 版本中引入它，ODBC 和及其说明。  
  
 SQL_ACCESSIBLE_PROCEDURES (ODBC 1.0)  
 一个字符串:"Y"，如果用户可以执行所有过程返回的**SQLProcedures**;"N"如果可能有过程返回，用户不能执行。  
  
 SQL_ACCESSIBLE_TABLES (ODBC 1.0)  
 一个字符串:"Y"，如果用户保证**选择**返回的所有表的特权**SQLTables**;"N"如果可能存在的表返回该用户无法访问。  
  
 SQL_ACTIVE_ENVIRONMENTS (ODBC 3.0)  
 SQLUSMALLINT 值，该值指定该驱动程序可以支持的活动环境的最大数目。 如果没有指定的限制或未知的限制，则将此值设置为零。  
  
 SQL_AGGREGATE_FUNCTIONS (ODBC 3.0)  
 枚举对聚合函数的支持 SQLUINTEGER 位掩码：  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 SQL-92 条目级别 – 符合的驱动程序始终将返回所有这些选项所支持。  
  
 SQL_ALTER_DOMAIN (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**ALTER 域**语句，如 SQL-92，支持的数据源中定义。 完整 SQL-92 的兼容级别的驱动程序将始终返回所有的位屏蔽。 返回值"0"意味着**ALTER 域**不支持语句。  
  
 此时必须支持此功能的 SQL-92 或 FIPS 符合性级别显示在每位掩码旁边的括号中。  
  
 以下位掩码用于确定支持的子句：  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = 的添加支持域约束 （完全级别）  
  
 SQL_AD_ADD_DOMAIN_DEFAULT = \<alter 域 > \<set 域默认子句 > 支持 （完全级别）  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION =\<约束名称定义子句 > 命名域约束 （中级） 支持  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT =\<删除域约束子句 > 支持 （完全级别）  
  
 SQL_AD_DROP_DOMAIN_DEFAULT = \<alter 域 >\<删除域默认子句 > 支持 （完全级别）  
  
 以下位指定受支持\<约束属性 > 如果\<添加域约束 > 支持 （SQL_AD_ADD_DOMAIN_CONSTRAINT 位设置）：  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE （完全级别） SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE （完全级别） SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED （完全级别） SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE （完全级别）  
  
 SQL_ALTER_TABLE (ODBC 2.0)  
 枚举中的子句 SQLUINTEGER 位掩码**ALTER TABLE**数据源支持的语句。  
  
 此时必须支持此功能的 SQL-92 或 FIPS 符合性级别显示在每位掩码旁边的括号中。  
  
 以下位掩码用于确定支持的子句：  
  
 SQL_AT_ADD_COLUMN_COLLATION =\<将列添加 > 支持子句，使用工具来指定列排序规则 （完全级别） (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT =\<将列添加 > 支持子句，使用工具来指定列默认值 （FIPS 过渡级别） (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_SINGLE =\<将列添加 > 是支持 （FIPS 过渡级别） (ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT =\<将列添加 > 支持子句，使用工具来指定列约束 （FIPS 过渡级别） (ODBC 3.0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT =\<添加表约束 > 支持子句 （FIPS 过渡级别） (ODBC 3.0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION =\<约束名称定义 > 命名列和表约束 （中级） 支持 (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_CASCADE =\<删除列 > 支持级联 （FIPS 过渡级别） (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT =\<更改列 > \<drop 列默认子句 > 是支持 （中级） (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT =\<删除列 > 支持限制 （FIPS 过渡级别） (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT =\<删除列 > 支持限制 （FIPS 过渡级别） (ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT =\<更改列 > \<set 列默认子句 > 是支持 （中级） (ODBC 3.0)  
  
 以下位指定的支持\<约束属性 > 如果支持指定列或表的约束 （SQL_AT_ADD_CONSTRAINT 位设置）：  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED （完全级别） (ODBC 3.0) SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE （完全级别） (ODBC 3.0) SQL_AT_CONSTRAINT_DEFERRABLE （完全级别） (ODBC 3.0) SQL_AT_CONSTRAINT_NON_DEFERRABLE （完全级别） (ODBC 3.0)  
  
 SQL_ASYNC_DBC_FUNCTIONS (ODBC 3.8)  
 SQLUINTEGER 值，该值指示是否驱动程序可以执行函数以异步方式对连接句柄。  
  
 SQL_ASYNC_DBC_CAPABLE = 驱动程序可以以异步方式执行连接函数。  
  
 SQL_ASYNC_DBC_NOT_CAPABLE = 驱动程序不能以异步方式进行连接的函数执行。  
  
 SQL_ASYNC_MODE (ODBC 3.0)  
 一个 SQLUINTEGER 值，该值指示驱动程序中的异步支持的级别：  
  
 SQL_AM_CONNECTION = 的连接支持级别的异步执行。 与给定的连接句柄关联的所有语句句柄都处于异步模式，或者所有都都在同步模式。 在连接上的语句句柄不能为在异步模式下，在同一连接上的另一个语句句柄时在同步模式下，反之亦然。  
  
 SQL_AM_STATEMENT = 支持级别的异步执行的语句。 虽然在同一连接上的其他语句句柄处于同步模式下，在异步模式下，可以是一些与连接句柄相关联的语句句柄。  
  
 SQL_AM_NONE = 异步模式下不支持。  
  
 SQL_ASYNC_NOTIFICATION  
 一个 SQLUINTEGER 值，该值指示该驱动程序是否支持异步通知：  
  
-   **SQL_ASYNC_NOTIFICATION_CAPABLE**驱动程序支持异步执行通知。  
  
-   **SQL_ASYNC_NOTIFICATION_NOT_CAPABLE**驱动程序不支持异步执行通知。  
  
 有两个类别的 ODBC 异步操作： 连接级异步操作和语句级别的异步操作。  如果驱动程序返回 SQL_ASYNC_NOTIFICATION_CAPABLE，它可以异步执行的所有 Api 都必须都支持通知。  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 枚举的行的可用性方面的驱动程序行为的 SQLUINTEGER 位掩码对进行计数。 以下的位屏蔽可以与信息类型一起使用：  
  
 SQL_BRC_ROLLED_UP = 行计数的连续的 INSERT、 DELETE 或 UPDATE 语句将累加起来，为一个。 如果未设置此位，行计数是可用于每个语句。  
  
 SQL_BRC_PROCEDURES = 行计数，如果任何，当某一批处理执行存储过程中时才可用。 如果提供行计数，则他们可以将其回滚或单独可用，具体取决于 SQL_BRC_ROLLED_UP 位。  
  
 SQL_BRC_EXPLICIT = 行计数，如果某一批处理执行直接通过调用时，任何，有可用**SQLExecute**或**SQLExecDirect**。 如果提供行计数，则他们可以将其回滚或单独可用，具体取决于 SQL_BRC_ROLLED_UP 位。  
  
 SQL_BATCH_SUPPORT (ODBC 3.0)  
 枚举对批处理的驱动程序的支持 SQLUINTEGER 位掩码。 以下位掩码用于确定支持的级别：  
  
 SQL_BS_SELECT_EXPLICIT = 驱动程序支持显式批处理，可以有结果集生成语句。  
  
 SQL_BS_ROW_COUNT_EXPLICIT = 可以有行计数生成语句的驱动程序支持显式批处理。  
  
 SQL_BS_SELECT_PROC = 的驱动程序支持显式过程可以有结果集生成语句。  
  
 SQL_BS_ROW_COUNT_PROC = 可以有行计数生成语句的驱动程序支持显式过程。  
  
 SQL_BOOKMARK_PERSISTENCE (ODBC 2.0)  
 枚举通过该书签将保存的操作 SQLUINTEGER 位掩码。  
  
 以下的位屏蔽与标志一起使用，以确定通过该选项的书签保存：  
  
 SQL_BP_CLOSE = 应用程序调用之后，书签将变为有效**SQLFreeStmt** SQL_CLOSE 选项，或**SQLCloseCursor**以关闭游标与语句相关联。  
  
 SQL_BP_DELETE = 书签的该行已被删除后，该行才有效。  
  
 SQL_BP_DROP = 应用程序调用之后，书签将变为有效**SQLFreeHandle**与*HandleType*设为 SQL_HANDLE_STMT 以 drop 语句。  
  
 SQL_BP_TRANSACTION = 应用程序提交或回滚事务之后，书签将变为有效。  
  
 SQL_BP_UPDATE = 书签的行，该行中的任何列进行了更新，包括键列后有效。  
  
 SQL_BP_OTHER_HSTMT = 与某个关联的书签语句可用于另一个语句。 除非指定 SQL_BP_CLOSE 或 SQL_BP_DROP，将光标放在第一条语句必须打开。  
  
 SQL_CATALOG_LOCATION (ODBC 2.0)  
 SQLUSMALLINT 值，该值指示在限定的表名中的目录位置：  
  
 SQL_CL_STARTSQL_CL_END  
  
 例如，Xbase 驱动程序返回 SQL_CL_START，因为目录 （目录） 名称是表名称，如下所示 \EMPDATA\EMP 开头。DBF。 ORACLE Server 驱动程序返回 SQL_CL_END，因为该目录是末尾的表名，如ADMIN.EMP@EMPDATA。  
  
 SQL-92 完整的级别 – 符合的驱动程序将始终返回 SQL_CL_START。 如果数据源不支持目录，则返回值为 0。 若要确定是否支持目录，应用程序调用**SQLGetInfo** SQL_CATALOG_NAME 信息类型。  
  
 这*信息类型*已重命名为从 ODBC 2.0 ODBC 3.0*信息类型*SQL_QUALIFIER_LOCATION。  
  
 SQL_CATALOG_NAME (ODBC 3.0)  
 一个字符串:"Y"，如果服务器支持目录名称或"N"，如果不是。  
  
 SQL-92 完整的级别 – 符合的驱动程序将始终返回"Y"。  
  
 SQL_CATALOG_NAME_SEPARATOR (ODBC 1.0)  
 一个字符串： 数据源定义为目录名称和遵循或它之前的限定的名元素之间的分隔符的字符。  
  
 如果数据源不支持目录，则返回空字符串。 若要确定是否支持目录，应用程序调用**SQLGetInfo** SQL_CATALOG_NAME 信息类型。 SQL-92 完整的级别 – 符合的驱动程序将始终返回"。"。  
  
 这*信息类型*已重命名为从 ODBC 2.0 ODBC 3.0*信息类型*SQL_QUALIFIER_NAME_SEPARATOR。  
  
 SQL_CATALOG_TERM (ODBC 1.0)  
 目录; 数据源供应商的名称字符的字符串例如，"数据库"或者"directory"。 此字符串可以是大写、 较低，或混合大小写。  
  
 如果数据源不支持目录，则返回空字符串。 若要确定是否支持目录，应用程序调用**SQLGetInfo** SQL_CATALOG_NAME 信息类型。 SQL-92 完整的级别 – 符合的驱动程序将始终返回"目录"。  
  
 这*信息类型*已重命名为从 ODBC 2.0 ODBC 3.0*信息类型*SQL_QUALIFIER_TERM。  
  
 SQL_CATALOG_USAGE (ODBC 2.0)  
 枚举可以在其中使用目录的语句 SQLUINTEGER 位掩码。  
  
 以下位掩码用于确定可以使用目录的位置：  
  
 SQL_CU_DML_STATEMENTS = 目录中所有数据操作语言语句支持：**选择**，**插入**，**更新**，**删除**，如果受支持，并**选择更新**和定位 update 和 delete 语句。  
  
 SQL_CU_PROCEDURE_INVOCATION = ODBC 过程调用语句中支持目录。  
  
 SQL_CU_TABLE_DEFINITION = 目录中所有表定义语句支持： **CREATE TABLE**， **CREATE VIEW**， **ALTER TABLE**， **DROP TABLE**，并**DROP 视图**。  
  
 SQL_CU_INDEX_DEFINITION = 目录中所有索引定义语句支持： **CREATE INDEX**并**DROP INDEX**。  
  
 SQL_CU_PRIVILEGE_DEFINITION = 所有特权定义语句中支持目录： **GRANT**并**撤消**。  
  
 如果数据源不支持目录，则返回值为 0。 若要确定是否支持目录，应用程序调用**SQLGetInfo** SQL_CATALOG_NAME 信息类型。 SQL-92 完整的级别 – 符合的驱动程序将始终返回所有这些设置的位的位掩码。  
  
 这*信息类型*已重命名为从 ODBC 2.0 ODBC 3.0*信息类型*SQL_QUALIFIER_USAGE。  
  
 SQL_COLLATION_SEQ (ODBC 3.0)  
 排序规则序列的名称。 这是一个字符串，指示为此服务器设置的默认字符的默认排序规则的名称 (例如，ISO 8859-1 或 EBCDIC)。 如果这是未知的将返回空字符串。 SQL-92 完整的级别 – 符合的驱动程序将始终返回非空字符串。  
  
 SQL_COLUMN_ALIAS (ODBC 2.0)  
 一个字符串:"Y"，如果数据源支持的列别名;否则为"N"。  
  
 列别名是可以通过使用 AS 子句指定的选择列表中的列的替代名称。 SQL-92 条目级别 – 符合的驱动程序将始终返回"Y"。  
  
 SQL_CONCAT_NULL_BEHAVIOR (ODBC 1.0)  
 SQLUSMALLINT 值，该值指示数据源如何处理空值的串联值非 NULL 值的字符数据类型列的字符数据类型列：  
  
 SQL_CB_NULL = 结果为 NULL 值。  
  
 SQL_CB_NON_NULL = 结果为非 NULL 值的列或列的串联。  
  
 SQL-92 条目级别 – 符合的驱动程序将始终返回 SQL_CB_NULL。  
  
 SQL_CONVERT_BIGINTSQL_CONVERT_BINARYSQL_CONVERT_BIT SQL_CONVERT_CHAR SQL_CONVERT_GUIDSQL_CONVERT_DATESQL_CONVERT_DECIMALSQL_CONVERT_DOUBLESQL_CONVERT_FLOATSQL_CONVERT_INTEGERSQL_CONVERT_INTERVAL_YEAR_MONTHSQL_CONVERT_INTERVAL_DAY_TIMESQL_CONVERT_LONGVARBINARYSQL_CONVERT_LONGVARCHARSQL_CONVERT_NUMERICSQL_CONVERT_REALSQL_CONVERT_SMALLINTSQL_CONVERT_TIMESQL_CONVERT_TIMESTAMPSQL_CONVERT_TINYINTSQL_CONVERT_VARBINARYSQL_CONVERT_VARCHAR (ODBC 1.0)  
 SQLUINTEGER 的位掩码。 位掩码，指示数据源支持的转换**转换**数据中名为的类型的标量函数*信息类型*。 位掩码为零，如果数据源不支持从数据已命名的类型，包括转换为相同的数据类型的任何转换。  
  
 例如，若要确定数据源是否支持 SQL_INTEGER 数据转换为 SQL_BIGINT 数据类型，应用程序调用**SQLGetInfo**与*信息类型*SQL_CONVERT_INTEGER。 在应用程序执行**AND** SQL_CVT_BIGINT，返回的位掩码的操作。 生成的值为非零值，如果支持该转换。  
  
 以下位掩码用于确定支持的转换：  
  
 SQL_CVT_BIGINT (ODBC 1.0) SQL_CVT_BINARY (ODBC 1.0) SQL_CVT_BIT (ODBC 1.0) SQL_CVT_GUID (ODBC 3.5) SQL_CVT_CHAR (ODBC 1.0) SQL_CVT_DATE (ODBC 1.0) SQL_CVT_DECIMAL (ODBC 1.0) SQL_CVT_DOUBLE (ODBC 1.0) SQL_CVT_FLOAT (ODBC 1.0) SQL_CVT_INTEGER (ODBC 1.0) SQL_CVT_INTERVAL_YEAR_MONTH (ODBC 3.0) (ODBC 3.0) SQL_CVT_INTERVAL_DAY_TIME SQL_CVT_LONGVARBINARY (ODBC 1.0) SQL_CVT_LONGVARCHAR (ODBC 1.0) SQL_CVT_NUMERIC (ODBC 1.0) SQL_CVT_REAL ODBC 1.0) SQL_CVT_TIME (ODBC 1.0) SQL_CVT_ SQL_CVT_SMALLINT (ODBC 1.0)时间戳 (ODBC 1.0) SQL_CVT_TINYINT (ODBC 1.0) SQL_CVT_VARBINARY (ODBC 1.0) SQL_CVT_VARCHAR (ODBC 1.0)  
  
 SQL_CONVERT_FUNCTIONS (ODBC 1.0)  
 枚举支持的驱动程序和关联的数据源的标量转换函数 SQLUINTEGER 位掩码。  
  
 以下位掩码，用于确定支持的转换函数：  
  
 SQL_FN_CVT_CASTSQL_FN_CVT_CONVERT  
  
 SQL_CORRELATION_NAME (ODBC 1.0)  
 SQLUSMALLINT 值，该值指示是否支持表相关名称：  
  
 SQL_CN_NONE = 的相关名称不受支持。  
  
 SQL_CN_DIFFERENT = 的相关名称支持，但必须不同于它们所表示的表的名称。  
  
 SQL_CN_ANY = 的相关名称支持，并且可以是任何有效的用户定义名称。  
  
 SQL-92 条目级别 – 符合的驱动程序将始终返回 SQL_CN_ANY。  
  
 SQL_CREATE_ASSERTION (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**创建断言**语句，如 SQL-92，支持的数据源中定义。  
  
 以下位掩码用于确定支持的子句：  
  
 SQL_CA_CREATE_ASSERTION  
  
 以下位指定受支持的约束属性，如果受支持的功能来显式指定约束的属性 （请参阅 SQL_ALTER_TABLE 和 SQL_CREATE_TABLE 信息类型）：  
  
 SQL_CA_CONSTRAINT_INITIALLY_DEFERREDSQL_CA_CONSTRAINT_INITIALLY_IMMEDIATESQL_CA_CONSTRAINT_DEFERRABLESQL_CA_CONSTRAINT_NON_DEFERRABLE  
  
 SQL-92 完整的级别 – 符合的驱动程序始终将返回所有这些选项所支持。 返回值"0"意味着**创建断言**不支持语句。  
  
 SQL_CREATE_CHARACTER_SET (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**创建字符集**语句，如 SQL-92，支持的数据源中定义。  
  
 以下位掩码用于确定支持的子句：  
  
 SQL_CCS_CREATE_CHARACTER_SETSQL_CCS_COLLATE_CLAUSESQL_CCS_LIMITED_COLLATION  
  
 SQL-92 完整的级别 – 符合的驱动程序始终将返回所有这些选项所支持。 返回值"0"意味着**创建字符集**不支持语句。  
  
 SQL_CREATE_COLLATION (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**创建排序规则**语句，如 SQL-92，支持的数据源中定义。  
  
 以下位掩码，用于确定支持的子句：  
  
 SQL_CCOL_CREATE_COLLATION  
  
 所支持的 SQL-92 Full 级别 – 符合的驱动程序将始终会返回此选项。 返回值"0"意味着**创建排序规则**不支持语句。  
  
 SQL_CREATE_DOMAIN (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**创建一个域**语句，如 SQL-92，支持的数据源中定义。  
  
 以下位掩码用于确定支持的子句：  
  
 SQL_CDO_CREATE_DOMAIN = 创建域支持语句 （中间级别）。  
  
 SQL_CDO_CONSTRAINT_NAME_DEFINITION =\<约束名称定义 > 命名域约束 （中级） 支持。  
  
 以下位指定能够创建列约束： SQL_CDO_DEFAULT = 支持指定域约束 （中间级别） SQL_CDO_CONSTRAINT = 支持指定域的默认值 （中间级别） SQL_CDO_COLLATION =指定域的排序规则支持 （完全级别）  
  
 如果支持指定域约束，以下位指定受支持的约束属性 （设置 SQL_CDO_DEFAULT）：  
  
 SQL_CDO_CONSTRAINT_INITIALLY_DEFERRED （完全级别） SQL_CDO_CONSTRAINT_INITIALLY_IMMEDIATE （完全级别） SQL_CDO_CONSTRAINT_DEFERRABLE （完全级别） SQL_CDO_CONSTRAINT_NON_DEFERRABLE （完全级别）  
  
 返回值"0"意味着**创建一个域**不支持语句。  
  
 SQL_CREATE_SCHEMA (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**CREATE SCHEMA**语句，如 SQL-92，支持的数据源中定义。  
  
 以下位掩码用于确定支持的子句：  
  
 SQL_CS_CREATE_SCHEMASQL_CS_AUTHORIZATIONSQL_CS_DEFAULT_CHARACTER_SET  
  
 SQL-92 中间级别 – 符合的驱动程序将始终返回所支持的 SQL_CS_CREATE_SCHEMA 和 SQL_CS_AUTHORIZATION 选项。 这些值也必须在 SQL-92 条目级别，但作为 SQL 语句不一定支持。 SQL-92 完整的级别 – 符合的驱动程序始终将返回所有这些选项所支持。  
  
 SQL_CREATE_TABLE (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**CREATE TABLE**语句，如 SQL-92，支持的数据源中定义。  
  
 此时必须支持此功能的 SQL-92 或 FIPS 符合性级别显示在每位掩码旁边的括号中。  
  
 以下位掩码用于确定支持的子句：  
  
 SQL_CT_CREATE_TABLE = CREATE TABLE 语句支持。 （项级别）  
  
 SQL_CT_TABLE_CONSTRAINT = 支持指定表约束 （FIPS 过渡级别）  
  
 SQL_CT_CONSTRAINT_NAME_DEFINITION =\<约束名称定义 > 子句支持用于命名列和表约束 （中间级别）  
  
 以下位指定创建临时表的功能：  
  
 SQL_CT_COMMIT_PRESERVE = 已删除的行保留在提交。 （完全级别）SQL_CT_COMMIT_DELETE = 已删除提交删除行。 （完全级别）SQL_CT_GLOBAL_TEMPORARY = Global 可以创建临时表。 （完全级别）SQL_CT_LOCAL_TEMPORARY = 本地可以创建临时表。 （完全级别）  
  
 以下位指定创建列约束的功能：  
  
 SQL_CT_COLUMN_CONSTRAINT = 支持指定列约束 （FIPS 过渡级别） SQL_CT_COLUMN_DEFAULT = 支持指定列默认值 （FIPS 过渡级别） SQL_CT_COLUMN_COLLATION = 指定列排序规则是支持 （完全级别）  
  
 如果支持指定列或表约束，则以下位指定受支持的约束属性：  
  
 SQL_CT_CONSTRAINT_INITIALLY_DEFERRED （完全级别） SQL_CT_CONSTRAINT_INITIALLY_IMMEDIATE （完全级别） SQL_CT_CONSTRAINT_DEFERRABLE （完全级别） SQL_CT_CONSTRAINT_NON_DEFERRABLE （完全级别）  
  
 SQL_CREATE_TRANSLATION (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**创建转换**语句，如 SQL-92，支持的数据源中定义。  
  
 以下位掩码，用于确定支持的子句：  
  
 SQL_CTR_CREATE_TRANSLATION  
  
 所支持的 SQL-92 Full 级别 – 符合的驱动程序将始终会返回这些选项。 返回值"0"意味着**创建转换**不支持语句。  
  
 SQL_CREATE_VIEW (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**CREATE VIEW**语句，如 SQL-92，支持的数据源中定义。  
  
 以下位掩码用于确定支持的子句：  
  
 SQL_CV_CREATE_VIEWSQL_CV_CHECK_OPTIONSQL_CV_CASCADEDSQL_CV_LOCAL  
  
 返回值"0"意味着**CREATE VIEW**不支持语句。  
  
 SQL-92 条目级别 – 符合的驱动程序将始终返回所支持的 SQL_CV_CREATE_VIEW 和 SQL_CV_CHECK_OPTION 选项。  
  
 SQL-92 完整的级别 – 符合的驱动程序始终将返回所有这些选项所支持。  
  
 SQL_CURSOR_COMMIT_BEHAVIOR (ODBC 1.0)  
 SQLUSMALLINT 值，该值指示如何**提交**操作会影响游标和数据源 （数据源时提交的事务的行为） 中的预定义的语句。  
  
 此属性的值将反映下一步设置的当前状态： SQL_COPT_SS_PRESERVE_CURSORS。  
  
 SQL_CB_DELETE = 关闭游标，并删除预定义的语句。 若要将光标同样，应用程序必须 reprepare 并重新执行该语句。  
  
 SQL_CB_CLOSE = 关闭游标。 对于已准备的语句，该应用程序可以调用**SQLExecute**而无需调用语句**SQLPrepare**试。 SQL ODBC 驱动程序的默认值为 SQL_CB_CLOSE。 这意味着提交事务时，SQL ODBC 驱动程序将关闭你游标。  
  
 SQL_CB_PRESERVE 像以前一样 = 在相同的位置保留游标**提交**操作。 应用程序可以继续提取数据，或者它可以关闭游标，然后重新执行该语句而无需重新准备。  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR (ODBC 1.0)  
 SQLUSMALLINT 值，该值指示如何**回滚**操作会影响游标和数据源中的预定义的语句：  
  
 SQL_CB_DELETE = 关闭游标，并删除预定义的语句。 若要将光标同样，应用程序必须 reprepare 并重新执行该语句。  
  
 SQL_CB_CLOSE = 关闭游标。 对于已准备的语句，该应用程序可以调用**SQLExecute**而无需调用语句**SQLPrepare**试。  
  
 SQL_CB_PRESERVE 像以前一样 = 在相同的位置保留游标**回滚**操作。 应用程序可以继续提取数据，或者它可以关闭游标，然后重新在语句执行而无需 repreparing 它。  
  
 SQL_CURSOR_SENSITIVITY (ODBC 3.0)  
 SQLUINTEGER 值，该值指示游标敏感性的支持：  
  
 SQL_INSENSITIVE = 由在同一事务中任何其他游标的所有游标语句句柄显示的结果集不反映对它进行了任何更改。  
  
 SQL_UNSPECIFIED = 它是未指定是否对语句句柄游标请可见对结果集由在同一事务中的另一个游标所做的更改。 游标语句句柄上的可能会使可见 none、 部分或全部此类更改。  
  
 SQL_SENSITIVE = 游标是通过在同一事务中其他游标所做的更改。  
  
 SQL-92 条目级别 – 符合的驱动程序将始终返回 SQL_UNSPECIFIED 选项，因为受支持。  
  
 所支持的 SQL-92 Full 级别 – 符合的驱动程序将始终会返回 SQL_INSENSITIVE 选项。  
  
 SQL_DATA_SOURCE_NAME (ODBC 1.0)  
 在连接过程中使用的数据源名称字符的字符串。 如果应用程序调用**SQLConnect**，这是值*szDSN*参数。 如果应用程序调用**SQLDriverConnect**或**SQLBrowseConnect**，这是在传递给驱动程序的连接字符串中使用 DSN 关键字的值。 如果连接字符串不包含**DSN**关键字 (例如，当它包含**驱动程序**关键字)，这是一个空字符串。  
  
 SQL_DATA_SOURCE_READ_ONLY (ODBC 1.0)  
 字符的字符串。 "Y"如果数据源设置为只读模式下，"N"，否则如果。  
  
 此特征仅属于该数据源，然后重试。它不是可以访问数据源的驱动程序的特征。 为读/写的驱动程序可用于的数据源，是只读的。 如果驱动程序是只读的所有其数据源必须是只读的并且必须返回 SQL_DATA_SOURCE_READ_ONLY。  
  
 SQL_DATABASE_NAME (ODBC 1.0)  
 如果数据源定义一个命名的对象称为"数据库"的一个字符字符串具有当前在使用中，数据库的名称。  
  
> [!NOTE]  
>  在 ODBC 3 *.x*，此返回的值*信息类型*也可以通过调用返回**SQLGetConnectAttr**与*特性*SQL_ATTR_CURRENT_CATALOG 的参数。  
  
 SQL_DATETIME_LITERALS (ODBC 3.0)  
 枚举数据源支持的 SQL-92 的日期时间文字 SQLUINTEGER 位掩码。 请注意，这些是在 SQL-92 规范中列出的日期时间文字独立于定义的 ODBC datetime 文字转义子句。 有关 ODBC datetime 文字转义子句的详细信息，请参阅[日期、 时间和时间戳文本](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)。  
  
 在下面的列表中的位的位掩码，FIPS 过渡级别 – 符合的驱动程序将始终返回"1"的值。 值为"0"表示不支持 SQL-92 的日期时间文字。  
  
 以下位掩码用于确定支持哪些文本：  
  
 SQL_DL_SQL92_DATESQL_DL_SQL92_TIMESQL_DL_SQL92_TIMESTAMPSQL_DL_SQL92_INTERVAL_YEARSQL_DL_SQL92_INTERVAL_MONTHSQL_DL_SQL92_INTERVAL_DAYSQL_DL_SQL92_INTERVAL_HOURSQL_DL_SQL92_INTERVAL_MINUTESQL_DL_SQL92_INTERVAL_SECONDSQL_DL_SQL92_INTERVAL_YEAR_TO_MONTHSQL_DL_SQL92_INTERVAL_DAY_TO_HOUR  
  
 SQL_DL_SQL92_INTERVAL_DAY_TO_MINUTESQL_DL_SQL92_INTERVAL_DAY_TO_SECONDSQL_DL_SQL92_INTERVAL_HOUR_TO_MINUTESQL_DL_SQL92_INTERVAL_HOUR_TO_SECONDSQL_DL_SQL92_INTERVAL_MINUTE_TO_SECOND  
  
 SQL_DBMS_NAME (ODBC 1.0)  
 驱动程序访问的 DBMS 产品的名称字符的字符串。  
  
 SQL_DBMS_VER (ODBC 1.0)  
 指示由驱动程序访问的 DBMS 产品版本的字符串。 版本是窗体的 # #。 # #。 # # #，其中前两个数字是否为主要版本，接下来的两位数字是次版本，而最后四个数字是否为发布版本。 驱动程序必须呈现此窗体中的 DBMS 产品版本，但也可以追加 DBMS 产品特定版本。 例如，"04.01.0000 Rdb 4.1"。  
  
 SQL_DDL_INDEX (ODBC 3.0)  
 SQLUINTEGER 值，该值指示用于创建和删除索引的支持：  
  
 SQL_DI_CREATE_INDEXSQL_DI_DROP_INDEX  
  
 SQL_DEFAULT_TXN_ISOLATION (ODBC 1.0)  
 SQLUINTEGER 值，该值指示默认事务隔离级别支持的驱动程序或数据源或为零的数据源不支持事务。 使用以下术语来定义事务隔离级别：  
  
 **脏读**事务 1 更改行。 事务 2 在事务 1 提交更改之前读取已更改的行。 如果事务 1 回滚更改，将具有事务 2 读取被视为从未存在过的行。  
  
 **不可重复读**事务 1 读取的行。 事务 2 更新或删除该行并提交此更改。 如果事务 1 尝试重新读取行时，它将接收不同的行值或发现该行已被删除。  
  
 **接触的虚拟**事务 1 读取一组满足某些搜索条件的行。 事务 2 生成一个或多个行 （通过插入或更新） 与搜索条件匹配。 如果事务 1 reexecutes 读取这些行的语句，它会接收一组不同的行。  
  
 如果数据源支持事务，驱动程序将返回以下位屏蔽之一：  
  
 SQL_TXN_READ_UNCOMMITTED = 脏读、 不可重复读取和幻影可使用。  
  
 SQL_TXN_READ_COMMITTED = 繁琐不可能进行读取。 也可能不可重复读取和幻影。  
  
 SQL_TXN_REPEATABLE_READ = 脏读和不可重复读不可能。 可能会出现幻影。  
  
 SQL_TXN_SERIALIZABLE = 事务是可序列化。 可序列化事务不允许脏读、 不可重复读取或幻像。  
  
 SQL_DESCRIBE_PARAMETER (ODBC 3.0)  
 一个字符串:"Y"，如果可以描述参数;"N"，如果不是。  
  
 SQL-92 完整的级别 – 符合的驱动程序通常将返回"Y"，因为它将支持**描述输入**语句。 由于这不会直接指定基础 SQL 支持，但是，描述参数可能不支持，即使在 SQL-92 Full 级别 – 符合的驱动程序。  
  
 SQL_DM_VER (ODBC 3.0)  
 具有版本的驱动程序管理器中的字符字符串。 版本是窗体的 # #。 # #。 # # #。 # # #，其中：  
  
 第一组两个数字是主要的 ODBC 版本，如常量 SQL_SPEC_MAJOR。  
  
 第二个集的两个数字是次要的 ODBC 版本，如常量 SQL_SPEC_MINOR。  
  
 四位数字的第三组是驱动程序管理器主要内部版本号。  
  
 四位数字的最后一组是驱动程序管理器的次要版本号。  
  
 Windows 7 驱动程序管理器版本是 03.80。 Windows 8 驱动程序管理器版本是 03.81。  
  
 SQL_DRIVER_AWARE_POOLING_SUPPORTED (ODBC 3.8)  
 SQLUINTEGER 值，该值指示如果驱动程序支持识别驱动程序的池。 (有关详细信息，请参阅[识别驱动程序的连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。  
  
 SQL_DRIVER_AWARE_POOLING_CAPABLE 指示驱动程序可以支持识别驱动程序的池机制。  
  
 SQL_DRIVER_AWARE_POOLING_NOT_CAPABLE 指示该驱动程序不能支持识别驱动程序的池机制。  
  
 驱动程序不需要实现 SQL_DRIVER_AWARE_POOLING_SUPPORTED 和驱动程序管理器不会对驱动程序的返回值。  
  
 SQL_DRIVER_HDBCSQL_DRIVER_HENV (ODBC 1.0)  
 Sqlulen 生成值、 驱动程序的环境句柄或连接句柄，由自变量*信息类型*。  
  
 由驱动程序管理器就实施这些信息类型。  
  
 SQL_DRIVER_HDESC (ODBC 3.0)  
 Sqlulen 生成值，由驱动程序管理器的描述符句柄，必须在输入中传递的驱动程序的描述符句柄\* *InfoValuePtr*从应用程序。 在这种情况下， *InfoValuePtr*是这两个输入和输出参数。 输入的描述符句柄传入\* *InfoValuePtr*必须显式或隐式分配上*ConnectionHandle*。  
  
 应用程序应制作一份驱动程序管理器的描述符之前它将调用处理**SQLGetInfo**使用此信息类型，以确保不在输出上覆盖该句柄。  
  
 此信息类型是由驱动程序管理器单独实现的。  
  
 SQL_DRIVER_HLIB (ODBC 2.0)  
 一个 sqlulen 生成的值， *hinst*从负载库返回到驱动程序管理器时加载上一个 Microsoft Windows 操作系统或等效的另一个操作系统上的驱动程序 DLL。 仅对连接句柄调用中指定的句柄无效， **SQLGetInfo**。  
  
 此信息类型是由驱动程序管理器单独实现的。  
  
 SQL_DRIVER_HSTMT (ODBC 1.0)  
 Sqlulen 生成值，由驱动程序管理器语句句柄，必须在输入中传递的驱动程序的语句句柄\* *InfoValuePtr*从应用程序。 在这种情况下， *InfoValuePtr*是一个输入和输出参数。 输入的语句句柄传入\* *InfoValuePtr*必须对自变量分配*ConnectionHandle*。  
  
 应用程序应制作一份驱动程序管理器的语句之前它将调用处理**SQLGetInfo**使用此信息类型，以确保不在输出上覆盖该句柄。  
  
 此信息类型是由驱动程序管理器单独实现的。  
  
 SQL_DRIVER_NAME (ODBC 1.0)  
 用来访问数据源驱动程序的文件名字符的字符串。  
  
 SQL_DRIVER_ODBC_VER (ODBC 2.0)  
 使用 ODBC 驱动程序支持的版本字符串。 版本是窗体的 # #。 # #，其中前两个数字是否为主要版本，接下来的两位数字是次要版本。 SQL_SPEC_MAJOR 和 SQL_SPEC_MINOR 定义的主版本号和次版本号。 有关 ODBC 本手册中所述的版本，这些是 3，0，并且该驱动程序应返回"03.00"。  
  
 ODBC 驱动程序管理器不会修改 SQLGetInfo(SQL_DRIVER_ODBC_VER) 以保持向后的兼容现有应用程序的返回值。 该驱动程序指定将返回的值。 但是，支持 C 数据类型可扩展性的驱动程序必须返回 3.8 （或更高版本） 时，应用程序调用**SQLSetEnvAttr** SQL_ATTR_ODBC_VERSION 设 3.8。 有关详细信息，请参阅[ODBC 中的 C 数据类型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
 SQL_DRIVER_VER (ODBC 1.0)  
 使用驱动程序版本和 （可选） 驱动程序的说明字符串。 最低版本是窗体的 # #。 # #。 # # #，其中前两个数字是否为主要版本，接下来的两位数字是次版本，而最后四个数字是否为发布版本。  
  
 SQL_DROP_ASSERTION (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**删除断言**语句，如 SQL-92，支持的数据源中定义。  
  
 以下位掩码，用于确定支持的子句：  
  
 SQL_DA_DROP_ASSERTION  
  
 所支持的 SQL-92 Full 级别 – 符合的驱动程序将始终会返回此选项。  
  
 SQL_DROP_CHARACTER_SET (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**DROP 字符集**语句，如 SQL-92，支持的数据源中定义。  
  
 以下位掩码，用于确定支持的子句：  
  
 SQL_DCS_DROP_CHARACTER_SET  
  
 所支持的 SQL-92 Full 级别 – 符合的驱动程序将始终会返回此选项。  
  
 SQL_DROP_COLLATION (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**删除排序规则**语句，如 SQL-92，支持的数据源中定义。  
  
 以下位掩码，用于确定支持的子句：  
  
 SQL_DC_DROP_COLLATION  
  
 所支持的 SQL-92 Full 级别 – 符合的驱动程序将始终会返回此选项。  
  
 SQL_DROP_DOMAIN (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**删除域**语句，如 SQL-92，支持的数据源中定义。  
  
 以下位掩码用于确定支持的子句：  
  
 SQL_DD_DROP_DOMAINSQL_DD_CASCADESQL_DD_RESTRICT  
  
 SQL-92 中间级别 – 符合的驱动程序始终将返回所有这些选项所支持。  
  
 SQL_DROP_SCHEMA (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**DROP SCHEMA**语句，如 SQL-92，支持的数据源中定义。  
  
 以下位掩码用于确定支持的子句：  
  
 SQL_DS_DROP_SCHEMASQL_DS_CASCADESQL_DS_RESTRICT  
  
 SQL-92 中间级别 – 符合的驱动程序始终将返回所有这些选项所支持。  
  
 SQL_DROP_TABLE (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**DROP TABLE**语句，如 SQL-92，支持的数据源中定义。  
  
 以下位掩码用于确定支持的子句：  
  
 SQL_DT_DROP_TABLESQL_DT_CASCADESQL_DT_RESTRICT  
  
 FIPS 过渡的级别 – 符合的驱动程序始终将返回所有这些选项所支持。  
  
 SQL_DROP_TRANSLATION (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**删除翻译**语句，如 SQL-92，支持的数据源中定义。  
  
 以下位掩码，用于确定支持的子句：  
  
 SQL_DTR_DROP_TRANSLATION  
  
 所支持的 SQL-92 Full 级别 – 符合的驱动程序将始终会返回此选项。  
  
 SQL_DROP_VIEW (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**DROP VIEW**语句，如 SQL-92，支持的数据源中定义。  
  
 以下位掩码用于确定支持的子句：  
  
 SQL_DV_DROP_VIEWSQL_DV_CASCADESQL_DV_RESTRICT  
  
 FIPS 过渡的级别 – 符合的驱动程序始终将返回所有这些选项所支持。  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 介绍驱动程序支持的动态游标属性 SQLUINTEGER 位掩码。 此位掩码包含的属性，则第一个的子集第二个子集，请参阅 SQL_DYNAMIC_CURSOR_ATTRIBUTES2。  
  
 以下位掩码用于确定支持哪些属性：  
  
 SQL_CA1_NEXT = A *FetchOrientation*调用中支持 SQL_FETCH_NEXT 的参数**SQLFetchScroll**当光标位于动态游标。  
  
 SQL_CA1_ABSOLUTE = *FetchOrientation*调用中支持参数 SQL_FETCH_FIRST、 SQL_FETCH_LAST，和 SQL_FETCH_ABSOLUTE **SQLFetchScroll**当光标位于动态游标。 （将提取的行集无关的当前光标位置。）  
  
 SQL_CA1_RELATIVE = *FetchOrientation*调用中支持参数的 SQL_FETCH_PRIOR 和 SQL_FETCH_RELATIVE **SQLFetchScroll**当光标位于动态游标。 （将提取的行集取决于当前光标位置。 请注意，这与分离 SQL_FETCH_NEXT 因为只进游标，在支持仅 SQL_FETCH_NEXT。）  
  
 SQL_CA1_BOOKMARK = A *FetchOrientation*调用中支持 SQL_FETCH_BOOKMARK 参数**SQLFetchScroll**当光标位于动态游标。  
  
 SQL_CA1_LOCK_EXCLUSIVE = A *LockType* SQL_LOCK_EXCLUSIVE 参数支持在调用**SQLSetPos**当光标位于动态游标。  
  
 SQL_CA1_LOCK_NO_CHANGE = A *LockType* SQL_LOCK_NO_CHANGE 参数支持在调用**SQLSetPos**当光标位于动态游标。  
  
 SQL_CA1_LOCK_UNLOCK = A *LockType* SQL_LOCK_UNLOCK 参数支持在调用**SQLSetPos**当光标位于动态游标。  
  
 SQL_CA1_POS_POSITION =*操作*SQL_POSITION 参数支持在调用**SQLSetPos**当光标位于动态游标。  
  
 SQL_CA1_POS_UPDATE =*操作*SQL_UPDATE 参数支持在调用**SQLSetPos**当光标位于动态游标。  
  
 SQL_CA1_POS_DELETE =*操作*SQL_DELETE 参数支持在调用**SQLSetPos**当光标位于动态游标。  
  
 SQL_CA1_POS_REFRESH =*操作*SQL_REFRESH 参数支持在调用**SQLSetPos**当光标位于动态游标。  
  
 SQL_CA1_POSITIONED_UPDATE = 的更新，当前的 SQL 游标是动态游标时，支持语句。 （SQL-92 条目级别 – 符合的驱动程序将始终返回此选项与受支持。）  
  
 SQL_CA1_POSITIONED_DELETE = 删除，当前的 SQL 游标是动态游标时，支持语句。 （SQL-92 条目级别 – 符合的驱动程序将始终返回此选项与受支持。）  
  
 SQL_CA1_SELECT_FOR_UPDATE = SELECT FOR UPDATE SQL 语句时游标是动态游标支持。 （SQL-92 条目级别 – 符合的驱动程序将始终返回此选项与受支持。）  
  
 SQL_CA1_BULK_ADD =*操作*SQL_ADD 参数支持在调用**SQLBulkOperations**当光标位于动态游标。  
  
 SQL_CA1_BULK_UPDATE_BY_BOOKMARK =*操作*SQL_UPDATE_BY_BOOKMARK 参数支持在调用**SQLBulkOperations**当光标位于动态游标。  
  
 SQL_CA1_BULK_DELETE_BY_BOOKMARK =*操作*SQL_DELETE_BY_BOOKMARK 参数支持在调用**SQLBulkOperations**当光标位于动态游标。  
  
 SQL_CA1_BULK_FETCH_BY_BOOKMARK =*操作*SQL_FETCH_BY_BOOKMARK 参数支持在调用**SQLBulkOperations**当光标位于动态游标。  
  
 SQL-92 中间级别 – 符合的驱动程序通常将返回 SQL_CA1_NEXT、 SQL_CA1_ABSOLUTE 和 SQL_CA1_RELATIVE 选项受支持，因为它支持通过嵌入 SQL 提取语句可滚动游标。 因为这不会直接确定基础 SQL 支持，但是，可滚动游标可能不受支持，即使对于 SQL-92 中间级别 – 符合的驱动程序。  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 介绍驱动程序支持的动态游标属性 SQLUINTEGER 位掩码。 此位掩码包含属性，则第二个的子集第一个子集，请参阅 SQL_DYNAMIC_CURSOR_ATTRIBUTES1。  
  
 以下位掩码用于确定支持哪些属性：  
  
 SQL_CA2_READ_ONLY_CONCURRENCY = 只读的动态游标，在其中不允许更新，支持。 （sql_attr_concurrency 设置语句属性可以是 SQL_CONCUR_READ_ONLY 动态游标）。  
  
 SQL_CA2_LOCK_CONCURRENCY = 动态游标使用的最低级别的锁定不足以确保支持可更新的行。 （sql_attr_concurrency 设置语句属性可以是 SQL_CONCUR_LOCK 动态游标。）这些锁必须具有事务隔离级别由 SQL_ATTR_TXN_ISOLATION 连接属性设置保持一致。  
  
 SQL_CA2_OPT_ROWVER_CONCURRENCY = 动态游标，支持使用乐观并发控制比较行版本。 （sql_attr_concurrency 设置语句属性可以是 SQL_CONCUR_ROWVER 动态游标。）  
  
 SQL_CA2_OPT_VALUES_CONCURRENCY = 动态游标，支持使用乐观并发控制比较值。 （sql_attr_concurrency 设置语句属性可以是 SQL_CONCUR_VALUES 动态游标。）  
  
 SQL_CA2_SENSITIVITY_ADDITIONS = 已添加行是动态游标; 对可见游标可以滚动到这些行。 （其中将这些行添加到光标处是驱动程序相关。）  
  
 SQL_CA2_SENSITIVITY_DELETIONS = 已删除行不再可供动态游标，而没有留下一个"hole"的结果集中;动态游标滚动从已删除行之后，它不能返回到该行。  
  
 SQL_CA2_SENSITIVITY_UPDATES = 是动态游标; 可见的行的更新如果动态游标中滚动，并返回对已更新行，则游标所返回的数据是更新的数据，而不是原始数据。  
  
 SQL_CA2_MAX_ROWS_SELECT = SQL_ATTR_MAX_ROWS 语句属性会影响**选择**时游标是动态游标的语句。  
  
 SQL_CA2_MAX_ROWS_INSERT = SQL_ATTR_MAX_ROWS 语句属性会影响**插入**时游标是动态游标的语句。  
  
 SQL_CA2_MAX_ROWS_DELETE = SQL_ATTR_MAX_ROWS 语句属性会影响**删除**时游标是动态游标的语句。  
  
 SQL_CA2_MAX_ROWS_UPDATE = SQL_ATTR_MAX_ROWS 语句属性会影响**更新**时游标是动态游标的语句。  
  
 SQL_CA2_MAX_ROWS_CATALOG = SQL_ATTR_MAX_ROWS 语句属性会影响**目录**时游标是动态游标结果集。  
  
 SQL_CA2_MAX_ROWS_AFFECTS_ALL = SQL_ATTR_MAX_ROWS 语句属性会影响**选择**，**插入**，**删除**，以及**更新**语句，并**目录**结果集，当游标是动态游标。  
  
 SQL_CA2_CRC_EXACT = 完全行计数是可用 SQL_DIAG_CURSOR_ROW_COUNT 诊断字段中时游标是动态游标。  
  
 SQL_CA2_CRC_APPROXIMATE = 近似行计数是可用 SQL_DIAG_CURSOR_ROW_COUNT 诊断字段中时游标是动态游标。  
  
 SQL_CA2_SIMULATE_NON_UNIQUE = 驱动程序不模拟的保证是否定位 update 或 delete 语句将影响只有一行时游标是动态游标;它是应用程序的责任，为确保这一点。 (如果语句影响多个行**SQLExecute**或**SQLExecDirect**返回 SQLSTATE 01001 [游标操作冲突]。)若要设置此行为，应用程序调用**SQLSetStmtAttr**与 SQL_ATTR_SIMULATE_CURSOR 属性设置为 SQL_SC_NON_UNIQUE。  
  
 SQL_CA2_SIMULATE_TRY_UNIQUE = 驱动程序尝试以保证模拟定位的更新或删除语句会影响只有一个行，当游标是动态游标。 即使它们可能会影响多个行，例如当驱动程序将始终执行此类语句没有唯一键。 (如果语句影响多个行**SQLExecute**或**SQLExecDirect**返回 SQLSTATE 01001 [游标操作冲突]。)若要设置此行为，应用程序调用**SQLSetStmtAttr**与 SQL_ATTR_SIMULATE_CURSOR 属性设置为 SQL_SC_TRY_UNIQUE。  
  
 SQL_CA2_SIMULATE_UNIQUE = 驱动程序保证模拟定位更新或 delete 语句将影响只有一行时游标是动态游标。 如果该驱动程序不能保证这一点对于给定的语句， **SQLExecDirect**或**SQLPrepare**返回 SQLSTATE 01001 （游标操作冲突）。 若要设置此行为，应用程序调用**SQLSetStmtAttr**与 SQL_ATTR_SIMULATE_CURSOR 属性设置为 SQL_SC_UNIQUE。  
  
 SQL_EXPRESSIONS_IN_ORDERBY (ODBC 1.0)  
 一个字符串:"Y"，如果数据源支持中的表达式**ORDER BY**列表;"N"如果不是。  
  
 SQL_FILE_USAGE (ODBC 2.0)  
 SQLUSMALLINT 值，该值指示如何单层驱动程序直接处理数据源中的文件：  
  
 SQL_FILE_NOT_SUPPORTED = 驱动程序不是单个层驱动程序。 例如，ORACLE 驱动程序是一个两层驱动程序。  
  
 SQL_FILE_TABLE = 为表的单层驱动程序将文件数据源中。 例如，Xbase 驱动程序将每个 Xbase 文件视为一个表。  
  
 SQL_FILE_CATALOG = 为编录数据源中的单层驱动程序处理文件。 例如，Microsoft Access 驱动程序将每个 Microsoft Access 文件视为完整的数据库。  
  
 应用程序可以使用此来确定用户将如何选择数据。 例如，Xbase 用户通常认为的数据存储在文件中，而 ORACLE 和 Microsoft Access 用户通常认为数据是存储在表中。  
  
 当用户选择 Xbase 数据源时，则应用程序无法显示 Windows**文件打开**常见对话框; 当用户选择 Microsoft Access 或 ORACLE 数据源，则应用程序可以显示一个自定义**选择表**对话框。  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 介绍驱动程序支持的只进游标属性 SQLUINTEGER 位掩码。 此位掩码包含的属性，则第一个的子集第二个子集，请参阅 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2。  
  
 以下位掩码用于确定支持哪些属性：  
  
 SQL_CA1_NEXTSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 有关这些位掩码的说明，请参阅 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 （和替换"只进游标"的说明中的"动态游标"）。  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 介绍驱动程序支持的只进游标属性 SQLUINTEGER 位掩码。 此位掩码包含属性，则第二个的子集第一个子集，请参阅 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1。  
  
 以下位掩码用于确定支持哪些属性：  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 有关这些位掩码的说明，请参阅 SQL_DYNAMIC_CURSOR_ATTRIBUTES2 （和替换"只进游标"的说明中的"动态游标"）。  
  
 SQL_GETDATA_EXTENSIONS (ODBC 2.0)  
 枚举扩展 SQLUINTEGER 位掩码**SQLGetData**。  
  
 以下的位屏蔽一起标志，用于确定有关驱动程序支持哪些常见的扩展插件**SQLGetData**:  
  
 SQL_GD_ANY_COLUMN = **SQLGetData**可以为任何未绑定列，包括那些在最后一个绑定列之前调用。 请注意，必须按顺序的升序列号，除非 SQL_GD_ANY_ORDER，也会返回调用列。  
  
 SQL_GD_ANY_ORDER = **SQLGetData**可以为未绑定列按任何顺序调用。 请注意， **SQLGetData**后，可以调用对于列仅在最后一个绑定列，除非 SQL_GD_ANY_COLUMN，也会返回。  
  
 SQL_GD_BLOCK = **SQLGetData**定位到与该行后可以为数据块 （其中的行集大小大于 1） 中的任意行中的未绑定列调用**SQLSetPos**。  
  
 SQL_GD_BOUND = **SQLGetData**可以调用对于绑定列，还未绑定的列。 驱动程序不能返回此值，除非它还会返回 SQL_GD_ANY_COLUMN。  
  
 SQL_GD_OUTPUT_PARAMS = **SQLGetData**可以调用以返回输出参数值。 有关详细信息，请参阅[使用 SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
 **SQLGetData**需要返回只在最后一个绑定列之后, 发生的未绑定列中的数据列号递增的顺序调用，并且未按行块中的行。  
  
 如果驱动程序支持书签 （固定长度或可变长度），则它必须支持调用**SQLGetData**上第 0 列。 这种支持是而不考虑该驱动程序返回到调用所需**SQLGetInfo**与 SQL_GETDATA_EXTENSIONS*信息类型*。  
  
 SQL_GROUP_BY (ODBC 2.0)  
 SQLUSMALLINT 值，该值指定在列之间的关系**GROUP BY**子句和 select 列表中的非聚合的列：  
  
 SQL_GB_COLLATE = A **COLLATE**子句可以指定每个分组列的末尾。 (ODBC 3.0)  
  
 SQL_GB_NOT_SUPPORTED = **GROUP BY**子句不受支持。 (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_EQUALS_SELECT = **GROUP BY**子句必须包含选择列表中的所有非聚合的列。 不能包含任何其他列。 例如，**选择部门、 MAX(SALARY) 从员工 GROUP BY DEPT**。 (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_CONTAINS_SELECT = **GROUP BY**子句必须包含选择列表中的所有非聚合的列。 它可以包含不在选择列表中的列。 例如，**选择部门，MAX(SALARY) 从员工组按部门、 期限**。 (ODBC 2.0)  
  
 SQL_GB_NO_RELATION = 中的列**GROUP BY**子句和 select 列表不相关。 选择列表中的非组合、 非聚合列的含义是数据源而定。 例如，**选择部门，薪金从员工组按部门、 期限**。 (ODBC 2.0)  
  
 SQL-92 条目级别 – 符合的驱动程序将始终返回 SQL_GB_GROUP_BY_EQUALS_SELECT 选项，因为受支持。 所支持的 SQL-92 Full 级别 – 符合的驱动程序将始终会返回 SQL_GB_COLLATE 选项。 如果支持任何选项，则**GROUP BY**子句不支持数据源。  
  
 SQL_IDENTIFIER_CASE (ODBC 1.0)  
 SQLUSMALLINT 值，如下所示：  
  
 SQL_IC_UPPER = SQL 中的标识符不区分大小写，并存储在系统目录中的大写。  
  
 SQL_IC_LOWER = SQL 中的标识符不区分大小写，并存储在系统目录中的小写。  
  
 SQL_IC_SENSITIVE = SQL 中的标识符区分大小写，并存储在系统目录中的混合大小写。  
  
 SQL_IC_MIXED = SQL 中的标识符不区分大小写，并存储在系统目录中的混合大小写。  
  
 由于 SQL-92 中的标识符是永远不会区分大小写，严格符合 SQL-92 （任何级别） 的驱动程序将永远不会返回 SQL_IC_SENSITIVE，选项所支持。  
  
 SQL_IDENTIFIER_QUOTE_CHAR (ODBC 1.0)  
 用作的起始和结束分隔符的带引号的字符串 （分隔） 中的 SQL 语句的标识符。 （标识符作为参数传递给 ODBC 函数无需用引号引起来。）如果数据源不支持带引号的标识符，则返回空白。  
  
 此字符串还可以用于 SQL_ATTR_METADATA_ID 的连接属性设置为 SQL_TRUE 时用引号括起来目录函数自变量。  
  
 由于 SQL-92 中的标识符引号是双引号 （"），驱动程序符合严格 SQL-92 到将始终返回双引号字符。  
  
 SQL_INDEX_KEYWORDS (ODBC 3.0)  
 SQLUINTEGER 位掩码，它枚举驱动程序支持在 CREATE INDEX 语句中的关键字：  
  
 SQL_IK_NONE = 不支持任何关键字。  
  
 SQL_IK_ASC = ASC 支持关键字。  
  
 SQL_IK_DESC = DESC 关键字受支持。  
  
 SQL_IK_ALL = 所有支持的关键字。  
  
 若要查看是否支持 CREATE INDEX 语句，应用程序调用**SQLGetInfo** SQL_DLL_INDEX 信息类型。  
  
 SQL_INFO_SCHEMA_VIEWS (ODBC 3.0)  
 枚举驱动程序支持在 INFORMATION_SCHEMA 视图 SQLUINTEGER 位掩码。 在中，视图和内容的 SQL-92 中定义为 INFORMATION_SCHEMA。  
  
 此时必须支持此功能的 SQL-92 或 FIPS 符合性级别显示在每位掩码旁边的括号中。  
  
 以下位掩码用于确定支持哪些视图：  
  
 SQL_ISV_ASSERTIONS = 标识由给定用户拥有的目录的断言。 （完全级别）  
  
 SQL_ISV_CHARACTER_SETS = 可以访问由给定用户的标识的目录的字符集。 （中间级别）  
  
 SQL_ISV_CHECK_CONSTRAINTS = 标识检查由给定用户拥有的约束。 （中间级别）  
  
 SQL_ISV_COLLATIONS = 标识给定用户可以访问该目录的字符排序规则。 （完全级别）  
  
 SQL_ISV_COLUMN_DOMAIN_USAGE = 目录取决于在目录中定义的域并由给定用户拥有的标识列。 （中间级别）  
  
 SQL_ISV_COLUMN_PRIVILEGES = 标识列的持久可用表或授权由给定用户的特权。 （FIPS 过渡级别）  
  
 SQL_ISV_COLUMNS = 标识给定用户可以访问的持久表的列。 （FIPS 过渡级别）  
  
 SQL_ISV_CONSTRAINT_COLUMN_USAGE = 类似到 CONSTRAINT_TABLE_USAGE 视图列标识由给定用户拥有的各种约束。 （中间级别）  
  
 SQL_ISV_CONSTRAINT_TABLE_USAGE = 标识约束使用的表 (引用、 唯一的并断言)，并由给定用户拥有。 （中间级别）  
  
 SQL_ISV_DOMAIN_CONSTRAINTS = 标识给定用户可以访问的域约束 （的目录中的域）。 （中间级别）  
  
 SQL_ISV_DOMAINS = 域定义的用户可以访问的目录中的标识。 （中间级别）  
  
 SQL_ISV_KEY_COLUMN_USAGE = 列标识在目录中定义的由给定用户约束为键。 （中间级别）  
  
 SQL_ISV_REFERENTIAL_CONSTRAINTS = 标识由给定用户拥有的引用约束。 （中间级别）  
  
 SQL_ISV_SCHEMATA = 标识由给定用户拥有的架构。 （中间级别）  
  
 SQL_ISV_SQL_LANGUAGES = SQL 一致性级别、 选项和方言支持的 SQL 实现的标识。 （中间级别）  
  
 SQL_ISV_TABLE_CONSTRAINTS = 标识由给定用户拥有的表约束。 （中间级别）  
  
 SQL_ISV_TABLE_PRIVILEGES = 标识持久可用表或授权由给定用户的特权。 （FIPS 过渡级别）  
  
 SQL_ISV_TABLES = 持久性表目录中定义的可访问由给定用户的标识。 （FIPS 过渡级别）  
  
 SQL_ISV_TRANSLATIONS = 标识字符转换为给定用户可以访问该目录。 （完全级别）  
  
 SQL_ISV_USAGE_PRIVILEGES = 使用权限可使用或由给定用户拥有的目录对象的标识。 （FIPS 过渡级别）  
  
 SQL_ISV_VIEW_COLUMN_USAGE = 的标识由给定用户拥有的列所在的目录视图的依赖。 （中间级别）  
  
 SQL_ISV_VIEW_TABLE_USAGE = 的标识由给定用户拥有的表所在的目录视图的依赖。 （中间级别）  
  
 SQL_ISV_VIEWS = 查看的表定义的、 给定用户可以访问此目录中的标识。 （FIPS 过渡级别）  
  
 SQL_INSERT_STATEMENT (ODBC 3.0)  
 指示支持 SQLUINTEGER 位掩码**插入**语句：  
  
 SQL_IS_INSERT_LITERALS  
  
 SQL_IS_INSERT_SEARCHED  
  
 SQL_IS_SELECT_INTO  
  
 SQL-92 条目级别 – 符合的驱动程序始终将返回所有这些选项所支持。  
  
 SQL_INTEGRITY (ODBC 1.0)  
 一个字符串:"Y"，如果数据源支持完整性增强功能;"N"如果不是。  
  
 这*信息类型*已重命名为从 ODBC 2.0 ODBC 3.0*信息类型*SQL_ODBC_SQL_OPT_IEF。  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 介绍驱动程序支持的键集游标属性 SQLUINTEGER 位掩码。 此位掩码包含的属性，则第一个的子集第二个子集，请参阅 SQL_KEYSET_CURSOR_ATTRIBUTES2。  
  
 以下位掩码用于确定支持哪些属性：  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 有关这些位掩码的说明，请参阅 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 （和替换"由键集驱动游标"的说明中的"动态游标"）。  
  
 SQL-92 中间级别 – 符合的驱动程序通常将返回 SQL_CA1_NEXT、 SQL_CA1_ABSOLUTE 和 SQL_CA1_RELATIVE 选项受支持，因为该驱动程序支持通过嵌入 SQL 提取语句可滚动游标。 因为这不会直接确定基础 SQL 支持，但是，可滚动游标可能不受支持，即使对于 SQL-92 中间级别 – 符合的驱动程序。  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 介绍驱动程序支持的键集游标属性 SQLUINTEGER 位掩码。 此位掩码包含属性，则第二个的子集第一个子集，请参阅 SQL_KEYSET_CURSOR_ATTRIBUTES1。  
  
 以下位掩码用于确定支持哪些属性：  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 有关这些位掩码的说明，请参阅 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 （和替换"由键集驱动游标"的说明中的"动态游标"）。  
  
 SQL_KEYWORDS (ODBC 2.0)  
 包含一列以逗号分隔的所有数据源特定关键字的字符串。 此列表不包含特定于 ODBC 的关键字或数据源和 ODBC 使用的关键字。 此列表表示所有保留的关键字;可互操作应用程序不应在对象名称中使用这些单词。  
  
 ODBC 关键字的列表，请参阅[保留关键字](../../../odbc/reference/appendixes/reserved-keywords.md)中[附录 c: SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。 **#Define**值 SQL_ODBC_KEYWORDS 包含 ODBC 关键字的以逗号分隔列表。  
  
 附录 C：SQL 语法  
  
 SQL_LIKE_ESCAPE_CLAUSE (ODBC 2.0)  
 一个字符串： 中的"Y"，如果数据源支持的转义符为百分比字符 （%） 和下划线字符 (_)**等**谓词和驱动程序支持 ODBC 语法的用于定义**等**谓词转义字符;"N"以其他方式。  
  
 SQL_MAX_ASYNC_CONCURRENT_STATEMENTS (ODBC 3.0)  
 SQLUINTEGER 值，该值指定活动的并发语句的最大数目的驱动程序可以支持对给定连接的异步模式。 如果没有任何特定的限制或未知的限制是，此值为零。  
  
 SQL_MAX_BINARY_LITERAL_LEN (ODBC 2.0)  
 一个 SQLUINTEGER 值，指定的最大长度 (十六进制字符组成，不包括文字前缀和后缀返回的数字**SQLGetTypeInfo**) 的 SQL 语句中的二进制文本。 例如，二进制文本 0xFFAA 具有长度为 4。 如果没有最大长度限制或长度为未知，则将此值设置为零。  
  
 SQL_MAX_CATALOG_NAME_LEN (ODBC 1.0)  
 SQLUSMALLINT 值，该值指定数据源中的目录名称的最大长度。 如果没有最大长度限制或长度为未知，则将此值设置为零。  
  
 FIPS 完整的级别 – 符合的驱动程序将返回至少 128。  
  
 这*信息类型*已重命名为从 ODBC 2.0 ODBC 3.0*信息类型*SQL_MAX_QUALIFIER_NAME_LEN。  
  
 SQL_MAX_CHAR_LITERAL_LEN (ODBC 2.0)  
 一个 SQLUINTEGER 值，指定的最大长度 (字符，不包括文字前缀和后缀返回的数**SQLGetTypeInfo**) 的 SQL 语句中的字符文本。 如果没有最大长度限制或长度为未知，则将此值设置为零。  
  
 SQL_MAX_COLUMN_NAME_LEN (ODBC 1.0)  
 SQLUSMALLINT 值，该值指定数据源中的列名称的最大长度。 如果没有最大长度限制或长度为未知，则将此值设置为零。  
  
 FIPS 条目级别 – 符合的驱动程序将返回至少为 18。 FIPS 中间级别 – 符合的驱动程序将返回至少 128。  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY (ODBC 2.0)  
 一个 SQLUSMALLINT 值，指定的列中允许的最大数**GROUP BY**子句。 如果没有指定的限制或未知的限制，则将此值设置为零。  
  
 FIPS 条目级别 – 符合的驱动程序将返回至少为 6。 FIPS 中间级别 – 符合的驱动程序将返回至少 15。  
  
 SQL_MAX_COLUMNS_IN_INDEX (ODBC 2.0)  
 SQLUSMALLINT 值，该值指定在索引中的最大允许的列数。 如果没有指定的限制或未知的限制，则将此值设置为零。  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY (ODBC 2.0)  
 一个 SQLUSMALLINT 值，指定的列中允许的最大数**ORDER BY**子句。 如果没有指定的限制或未知的限制，则将此值设置为零。  
  
 FIPS 条目级别 – 符合的驱动程序将返回至少为 6。 FIPS 中间级别 – 符合的驱动程序将返回至少 15。  
  
 SQL_MAX_COLUMNS_IN_SELECT (ODBC 2.0)  
 选择列表中，指定最大允许的列数 SQLUSMALLINT 值。 如果没有指定的限制或未知的限制，则将此值设置为零。  
  
 FIPS 条目级别 – 符合的驱动程序将返回至少为 100。 FIPS 中间级别 – 符合的驱动程序将返回至少 250。  
  
 SQL_MAX_COLUMNS_IN_TABLE (ODBC 2.0)  
 SQLUSMALLINT 值，该值指定表中的最大允许的列数。 如果没有指定的限制或未知的限制，则将此值设置为零。  
  
 FIPS 条目级别 – 符合的驱动程序将返回至少为 100。 FIPS 中间级别 – 符合的驱动程序将返回至少 250。  
  
 SQL_MAX_CONCURRENT_ACTIVITIES (ODBC 1.0)  
 SQLUSMALLINT 值，该值指定该驱动程序可以支持的连接的活动语句的最大数目。 如果它已挂起、 包含字词"结果"含义中的行的结果，为活动定义语句**选择**操作或受影响的行**插入**，**更新**，或**删除**操作 （例如，行计数），或如果它处于 NEED_DATA 状态。 此值可以反映驱动程序或数据源所强加的限制。 如果没有指定的限制或未知的限制，则将此值设置为零。  
  
 这*信息类型*已重命名为从 ODBC 2.0 ODBC 3.0*信息类型*SQL_ACTIVE_STATEMENTS。  
  
 SQL_MAX_CURSOR_NAME_LEN (ODBC 1.0)  
 SQLUSMALLINT 值，该值指定数据源中的游标名称的最大长度。 如果没有最大长度限制或长度为未知，则将此值设置为零。  
  
 FIPS 条目级别 – 符合的驱动程序将返回至少为 18。 FIPS 中间级别 – 符合的驱动程序将返回至少 128。  
  
 SQL_MAX_DRIVER_CONNECTIONS (ODBC 1.0)  
 一个 SQLUSMALLINT 值，指定的最大的驱动程序可以支持为环境的活动连接数。 此值可以反映驱动程序或数据源所强加的限制。 如果没有指定的限制或未知的限制，则将此值设置为零。  
  
 这*信息类型*已重命名为从 ODBC 2.0 ODBC 3.0*信息类型*SQL_ACTIVE_CONNECTIONS。  
  
 SQL_MAX_IDENTIFIER_LEN (ODBC 3.0)  
 SQLUSMALLINT，该值指示数据源支持的用户定义名称的字符的最大大小。  
  
 FIPS 条目级别 – 符合的驱动程序将返回至少为 18。 FIPS 中间级别 – 符合的驱动程序将返回至少 128。  
  
 SQL_MAX_INDEX_SIZE (ODBC 2.0)  
 SQLUINTEGER 值，该值指定最大允许索引的合并字段中的字节数。 如果没有指定的限制或未知的限制，则将此值设置为零。  
  
 SQL_MAX_PROCEDURE_NAME_LEN (ODBC 1.0)  
 SQLUSMALLINT 值，该值指定数据源中的过程名称的最大长度。 如果没有最大长度限制或长度为未知，则将此值设置为零。  
  
 SQL_MAX_ROW_SIZE (ODBC 2.0)  
 SQLUINTEGER 值，该值指定表中的单个行的最大长度。 如果没有指定的限制或未知的限制，则将此值设置为零。  
  
 FIPS 条目级别 – 符合的驱动程序将返回至少 2,000。 FIPS 中间级别 – 符合的驱动程序将返回至少 8,000。  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG (ODBC 3.0)  
 一个字符串:"Y"如果 SQL_MAX_ROW_SIZE 信息类型包括所有 SQL_LONGVARCHAR 和 SQL_LONGVARBINARY 列的长度的行; 中返回的最大行大小"N"以其他方式。  
  
 SQL_MAX_SCHEMA_NAME_LEN (ODBC 1.0)  
 SQLUSMALLINT 值，该值指定数据源中的架构名称的最大长度。 如果没有最大长度限制或长度为未知，则将此值设置为零。  
  
 FIPS 条目级别 – 符合的驱动程序将返回至少为 18。 FIPS 中间级别 – 符合的驱动程序将返回至少 128。  
  
 这*信息类型*已重命名为从 ODBC 2.0 ODBC 3.0*信息类型*SQL_MAX_OWNER_NAME_LEN。  
  
 SQL_MAX_STATEMENT_LEN (ODBC 2.0)  
 SQLUINTEGER 值，该值指定 SQL 语句的最大长度 （字符数，包括空格）。 如果没有最大长度限制或长度为未知，则将此值设置为零。  
  
 SQL_MAX_TABLE_NAME_LEN (ODBC 1.0)  
 SQLUSMALLINT 值，该值指定数据源中的表名称的最大长度。 如果没有最大长度限制或长度为未知，则将此值设置为零。  
  
 FIPS 条目级别 – 符合的驱动程序将返回至少为 18。 FIPS 中间级别 – 符合的驱动程序将返回至少 128。  
  
 SQL_MAX_TABLES_IN_SELECT (ODBC 2.0)  
 SQLUSMALLINT 值，该值指定表中允许的最大数目**FROM**子句**选择**语句。 如果没有指定的限制或未知的限制，则将此值设置为零。  
  
 FIPS 条目级别 – 符合的驱动程序将返回至少 15。 FIPS 中间级别 – 符合的驱动程序将返回至少 50。  
  
 SQL_MAX_USER_NAME_LEN (ODBC 2.0)  
 SQLUSMALLINT 值，该值指定数据源中的用户名称的最大长度。 如果没有最大长度限制或长度为未知，则将此值设置为零。  
  
 SQL_MULT_RESULT_SETS (ODBC 1.0)  
 一个字符串:"Y"，如果数据源支持多个结果集，"N"，如果不是。  
  
 有关多个结果集的详细信息，请参阅[多个结果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 SQL_MULTIPLE_ACTIVE_TXN (ODBC 1.0)  
 一个字符串:"Y"，如果该驱动程序支持在相同时，"N"的多个活动事务，如果只有一个事务可以在任何时候处于活动状态。  
  
 返回此信息类型的信息不适用于在分布式事务的情况下。  
  
 SQL_NEED_LONG_DATA_LEN (ODBC 2.0)  
 一个字符串： 如果不是"Y"，如果数据源需要该值之前的长数据值 （数据类型为 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或的长整型数据源特定于数据类型） 的长度发送到数据源，"N"。 有关详细信息，请参阅[SQLBindParameter 函数](../../../odbc/reference/syntax/sqlbindparameter-function.md)并[SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
 SQL_NON_NULLABLE_COLUMNS (ODBC 1.0)  
 SQLUSMALLINT 值，该值指定数据源是否支持 NOT NULL 列中：  
  
 SQL_NNC_NULL = 所有列必须可为 null。  
  
 SQL_NNC_NON_NULL = 列不能为 null。 (数据源支持**NOT NULL**中的列约束**CREATE TABLE**语句。)  
  
 SQL-92 条目级别 – 符合的驱动程序将返回 SQL_NNC_NON_NULL。  
  
 SQL_NULL_COLLATION (ODBC 2.0)  
 指定 null 值在结果集中的排序位置 SQLUSMALLINT 值：  
  
 SQL_NC_END = null 值进行排序的结果集，而不考虑 ASC 或 DESC 关键字结尾处。  
  
 SQL_NC_HIGH = null 值进行排序的结果集，具体取决于 ASC 或 DESC 关键字高的末尾。  
  
 SQL_NC_LOW = null 值进行排序的结果集，具体取决于 ASC 或 DESC 关键字偏低时。  
  
 SQL_NC_START = null 值进行排序的结果集，而不考虑 ASC 或 DESC 关键字开头。  
  
 SQL_NUMERIC_FUNCTIONS (ODBC 1.0)  
 注意： ODBC 1.0; 中引入的信息类型位掩码，每个带有中引入的版本。  
  
 枚举支持的驱动程序和关联的数据源的标量数字函数 SQLUINTEGER 位掩码。  
  
 以下位掩码用于确定支持的数值的函数：  
  
 SQL_FN_NUM_ABS (ODBC 1.0) SQL_FN_NUM_ACOS (ODBC 1.0) SQL_FN_NUM_ASIN (ODBC 1.0) SQL_FN_NUM_ATAN (ODBC 1.0) SQL_FN_NUM_ATAN2 (ODBC 1.0) SQL_FN_NUM_CEILING (ODBC 1.0) SQL_FN_NUM_COS (ODBC 1.0) SQL_FN_NUM_COT (ODBC 1.0) SQL_FN_NUM_DEGREES (ODBC 2.0) SQL_FN_NUM_EXP (ODBC 1.0) SQL_FN_NUM_FLOOR (ODBC 1.0) SQL_FN_NUM_LOG (ODBC 1.0) SQL_FN_NUM_LOG10 (ODBC 2.0) SQL_FN_NUM_MOD (ODBC 1.0) SQL_FN_NUM_PI (ODBC 1.0) SQL_FN_NUM_POWER (ODBC 2.0) SQL_FN_NUM_RADIANS (ODBC 2.0) SQL_FN_ SQL_FN_NUM_RAND (ODBC 1.0)NUM_ROUND (ODBC 2.0) SQL_FN_NUM_SIGN (ODBC 1.0) SQL_FN_NUM_SIN (ODBC 1.0) SQL_FN_NUM_SQRT (ODBC 1.0) SQL_FN_NUM_TAN (ODBC 1.0) SQL_FN_NUM_TRUNCATE (ODBC 2.0)  
  
 SQL_ODBC_INTERFACE_CONFORMANCE (ODBC 3.0)  
 SQLUINTEGER 值，该值指示 ODBC 3 别的 *.x*驱动程序符合的接口。  
  
 SQL_OIC_CORE： 所有 ODBC 驱动程序的最低级别应遵守。 此级别包括基本界面元素，如连接函数、 准备和执行 SQL 语句的函数、 基本的结果集元数据函数，基本的目录函数等。  
  
 SQL_OIC_LEVEL1： 级别包括核心标准符合性级别功能，加上可滚动游标，书签，定位更新和删除，等等。  
  
 SQL_OIC_LEVEL2: 级别包括第 1 级标准符合性级别功能，加上高级的功能，例如敏感游标;更新、 删除和刷新的书签;存储的过程支持;主键和外键; 的目录函数多目录支持;等等。  
  
 有关详细信息，请参阅[接口一致性级别](../../../odbc/reference/develop-app/interface-conformance-levels.md)。  
  
 SQL_ODBC_VER (ODBC 1.0)  
 版本的 ODBC 驱动程序管理器符合字符的字符串。 版本是窗体的 # #。 # #。 0000，其中前两个数字是否为主要版本，接下来的两位数字是次要版本。 这被实现仅在驱动程序管理器。  
  
 SQL_OJ_CAPABILITIES (ODBC 2.01)  
 枚举类型的驱动程序和数据源支持的外部联接 SQLUINTEGER 位掩码。 以下位掩码用于确定哪些类型受支持：  
  
 SQL_OJ_LEFT = 左外部联接都受支持。  
  
 SQL_OJ_RIGHT = 右外部联接都受支持。  
  
 SQL_OJ_FULL = 完全支持外部联接。  
  
 SQL_OJ_NESTED = 嵌套外部联接都受支持。  
  
 SQL_OJ_NOT_ORDERED = 外部联接的 ON 子句中的名称不需要为其相应的表名称相同的顺序的列**外部联接**子句。  
  
 SQL_OJ_INNER = 内部表 （左外部联接的右表） 或右外部联接中的左表还可用于在内部联接。 这不适用于完全外部联接，而没有内部表。  
  
 SQL_OJ_ALL_COMPARISON_OPS = 比较运算符在 ON 子句中的可以是任何 ODBC 比较运算符。 如果未设置此位，可以在外部联接中使用等于 （=） 比较运算符。  
  
 如果这些选项都不返回受支持，不支持任何外部联接子句。  
  
 有关支持的 SELECT 语句中的关系联接运算符的信息根据 SQL-92 的定义，请参阅 SQL_SQL92_RELATIONAL_JOIN_OPERATORS。  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT (ODBC 2.0)  
 一个字符串:"Y"如果中的列**ORDER BY**子句必须内嵌在 select 列表中; 否则为"N"。  
  
 SQL_PARAM_ARRAY_ROW_COUNTS (ODBC 3.0)  
 枚举驱动程序的属性有关的行可用性 SQLUINTEGER 中参数化执行计数。 具有以下值：  
  
 SQL_PARC_BATCH = 个人行计数是可用于每个组的参数。 这是概念上等同于生成一批 SQL 语句，一个用于设置数组中每个参数的驱动程序。 可以通过使用 SQL_PARAM_STATUS_PTR 描述符字段检索扩展的错误信息。  
  
 SQL_PARC_NO_BATCH = 没有只有一个行计数，这是整个数组的参数的语句执行后生成的累计行计数。 这是概念上等同于完整的参数数组以及语句视为一个原子单元。 错误的处理相同，就像一条语句执行。  
  
 SQL_PARAM_ARRAY_SELECTS (ODBC 3.0)  
 在参数化执行过程中设置 SQLUINTEGER 枚举结果的可用性有关的驱动程序的属性。 具有以下值：  
  
 SQL_PAS_BATCH = 没有一个结果集可用的每个参数集。 这是概念上等同于生成一批 SQL 语句，一个用于设置数组中每个参数的驱动程序。  
  
 SQL_PAS_NO_BATCH = 没有只有一个结果集可用，表示累积的结果集的完整数组的参数的语句执行后生成。 这是概念上等同于完整的参数数组以及语句视为一个原子单元。  
  
 SQL_PAS_NO_SELECT = A 驱动程序不允许使用参数数组执行的结果集生成语句。  
  
 SQL_PROCEDURE_TERM (ODBC 1.0)  
 过程; 的数据源供应商的名称字符的字符串例如，"数据库过程"、"存储的过程"，"过程"、"包"存储的查询"。  
  
 SQL_PROCEDURES (ODBC 1.0)  
 一个字符串:"Y"，如果数据源支持过程，并且该驱动程序支持 ODBC 过程调用语法;"N"以其他方式。  
  
 SQL_POS_OPERATIONS (ODBC 2.0)  
 枚举中的支持操作 SQLINTEGER 位掩码**SQLSetPos**。  
  
 以下的位屏蔽与标志一起使用，以确定支持哪些选项。  
  
 SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0)  
  
 SQL_QUOTED_IDENTIFIER_CASE (ODBC 2.0)  
 SQLUSMALLINT 值，如下所示：  
  
 SQL_IC_UPPER = 带引号 SQL 中的标识符不区分大小写，并存储在系统目录中的大写。  
  
 SQL_IC_LOWER = 带引号 SQL 中的标识符不区分大小写，并存储在系统目录中的小写。  
  
 SQL_IC_SENSITIVE = 带引号 SQL 中的标识符区分大小写，并存储在系统目录中的混合大小写。 （在 SQL-92 兼容的数据库中，带引号的标识符是始终区分大小写。）  
  
 SQL_IC_MIXED = 带引号 SQL 中的标识符不区分大小写，并存储在系统目录中的混合大小写。  
  
 SQL-92 条目级别 – 符合的驱动程序将始终返回 SQL_IC_SENSITIVE。  
  
 SQL_ROW_UPDATES (ODBC 1.0)  
 一个字符串:"Y"，如果由键集驱动或混合游标维护行版本或所有的值中提取行并因此可以检测对行所做的任何用户自上次提取该行的任何更新。 （这仅适用于更新，不适用于删除或插入操作。）该驱动程序可以返回 SQL_ROW_UPDATED 标志将行状态数组何时**SQLFetchScroll**调用。 否则为"N"。  
  
 SQL_SCHEMA_TERM (ODBC 1.0)  
 为架构; 数据源供应商的名称字符的字符串例如，"所有者"、"授权 ID"或者"架构"。  
  
 可以大写、 较低，或混合大小写中返回的字符串。  
  
 SQL-92 条目级别 – 符合的驱动程序将始终返回"架构"。  
  
 这*信息类型*已重命名为从 ODBC 2.0 ODBC 3.0*信息类型*SQL_OWNER_TERM。  
  
 SQL_SCHEMA_USAGE (ODBC 2.0)  
 枚举架构可以用于的语句 SQLUINTEGER 位掩码：  
  
 SQL_SU_DML_STATEMENTS = 架构中所有数据操作语言语句支持：**选择**，**插入**，**更新**，**删除**，如果受支持，并**选择更新**和定位 update 和 delete 语句。  
  
 SQL_SU_PROCEDURE_INVOCATION = ODBC 过程调用语句中支持的架构。  
  
 SQL_SU_TABLE_DEFINITION = 架构中所有表定义语句支持： **CREATE TABLE**， **CREATE VIEW**， **ALTER TABLE**， **DROP TABLE**，并**DROP 视图**。  
  
 SQL_SU_INDEX_DEFINITION = 所有索引定义语句中支持的架构： **CREATE INDEX**并**DROP INDEX**。  
  
 SQL_SU_PRIVILEGE_DEFINITION = 所有特权定义语句中支持的架构： **GRANT**并**撤消**。  
  
 SQL-92 条目级别 – 符合的驱动程序将始终返回 SQL_SU_DML_STATEMENTS、 SQL_SU_TABLE_DEFINITION 和 SQL_SU_PRIVILEGE_DEFINITION 选项，因为受支持。  
  
 这*信息类型*已重命名为从 ODBC 2.0 ODBC 3.0*信息类型*SQL_OWNER_USAGE。  
  
 SQL_SCROLL_OPTIONS (ODBC 1.0)  
 注意： ODBC 1.0; 中引入的信息类型位掩码，每个带有中引入的版本。  
  
 枚举支持的可滚动游标滚动选项 SQLUINTEGER 位掩码。  
  
 以下位掩码用于确定支持的选项：  
  
 SQL_SO_FORWARD_ONLY = 向前滚动游标唯一。 (ODBC 1.0)  
  
 SQL_SO_STATIC = 数据在结果集为静态。 (ODBC 2.0)  
  
 SQL_SO_KEYSET_DRIVEN = 驱动程序将保存并使用密钥进行中的结果集的每一行。 (ODBC 1.0)  
  
 SQL_SO_DYNAMIC = 驱动程序保留 （由键集大小为行集大小相同） 的行集中的每个行的键。 (ODBC 1.0)  
  
 SQL_SO_MIXED = 驱动程序保留密钥的每个行的键集和由键集大小大于行集大小。 游标是在由键集由键集驱动和动态外键集。 (ODBC 1.0)  
  
 有关可滚动游标的信息，请参阅[可滚动游标](../../../odbc/reference/develop-app/scrollable-cursors.md)。  
  
 SQL_SEARCH_PATTERN_ESCAPE (ODBC 1.0)  
 指定的驱动程序支持作为转义符，允许使用模式匹配元字符下划线 (_) 和百分号 （%） 作为搜索模式中的有效字符的字符字符串。 此转义符仅适用于这些目录函数支持参数的搜索字符串。 如果此字符串为空，则驱动程序不支持的搜索模式转义符。  
  
 因为此信息类型并不表示常规支持的中的转义字符**如**谓词，SQL-92 不包括此字符串的要求。  
  
 这*信息类型*仅限于目录函数。 使用搜索模式字符串中的转义字符的说明，请参阅[模式值自变量](../../../odbc/reference/develop-app/pattern-value-arguments.md)。  
  
 SQL_SERVER_NAME (ODBC 1.0)  
 字符的字符串的实际数据源特定于服务器名称;过程中使用数据源名称时很有用**SQLConnect**， **SQLDriverConnect**，并**SQLBrowseConnect**。  
  
 SQL_SPECIAL_CHARACTERS (ODBC 2.0)  
 包含所有特殊字符 （即 a 到 z、 A 到 Z、 0 到 9 和下划线以外的所有字符），可在标识符名称，如表名、 列名称或索引名称，请在数据源中的字符字符串。 例如，"#$^"。 如果标识符包含一个或多个这些字符，则标识符必须是分隔的标识符。  
  
 SQL_SQL_CONFORMANCE (ODBC 3.0)  
 SQLUINTEGER 值，该值指示 SQL-92 驱动程序支持的级别：  
  
 SQL_SC_SQL92_ENTRY = 条目级别 SQL-92 兼容。  
  
 SQL_SC_FIPS127_2_TRANSITIONAL = FIPS 127-2 过渡级别兼容。  
  
 SQL_SC_SQL92_FULL = 完全级别 SQL-92 兼容。  
  
 SQL_SC_ SQL92_INTERMEDIATE = 中间级别 SQL-92 兼容。  
  
 SQL_SQL92_DATETIME_FUNCTIONS(ODBC 3.0)  
 枚举支持的驱动程序和关联的数据源，而日期时间标量函数，如 SQL-92 中定义 SQLUINTEGER 位掩码。  
  
 以下位掩码用于确定支持的日期时间函数：  
  
 SQL_SDF_CURRENT_DATESQL_SDF_CURRENT_TIMESQL_SDF_CURRENT_TIMESTAMP  
  
 SQL_SQL92_FOREIGN_KEY_DELETE_RULE(ODBC 3.0)  
 枚举中的外键支持的规则 SQLUINTEGER 位掩码**删除**语句，如 SQL-92 中定义。  
  
 以下位掩码用于确定数据源支持的子句：  
  
 SQL_SFKD_CASCADESQL_SFKD_NO_ACTIONSQL_SFKD_SET_DEFAULTSQL_SFKD_SET_NULL  
  
 FIPS 过渡的级别 – 符合的驱动程序始终将返回所有这些选项所支持。  
  
 SQL_SQL92_FOREIGN_KEY_UPDATE_RULE(ODBC 3.0)  
 枚举中的外键支持的规则 SQLUINTEGER 位掩码**更新**语句，如 SQL-92 中定义。  
  
 以下位掩码用于确定数据源支持的子句：  
  
 SQL_SFKU_CASCADESQL_SFKU_NO_ACTIONSQL_SFKU_SET_DEFAULTSQL_SFKU_SET_NULL  
  
 SQL-92 完整的级别 – 符合的驱动程序始终将返回所有这些选项所支持。  
  
 SQL_SQL92_GRANT(ODBC 3.0)  
 枚举中支持的子句 SQLUINTEGER 位掩码**授予**语句，如 SQL-92 中定义。  
  
 此时必须支持此功能的 SQL-92 或 FIPS 符合性级别显示在每位掩码旁边的括号中。  
  
 以下位掩码用于确定数据源支持的子句：  
  
 SQL_SG_DELETE_TABLE （入门级） SQL_SG_INSERT_COLUMN （中级） SQL_SG_INSERT_TABLE （入门级） SQL_SG_REFERENCES_TABLE （入门级） SQL_SG_REFERENCES_COLUMN （入门级） SQL_SG_SELECT_TABLE （入门级） SQL_SG_UPDATE_COLUMN (入门级） SQL_SG_UPDATE_TABLE （入门级） SQL_SG_USAGE_ON_DOMAIN （FIPS 过渡级别） SQL_SG_USAGE_ON_CHARACTER_SET （FIPS 过渡级别） SQL_SG_USAGE_ON_COLLATION （FIPS 过渡级别） SQL_SG_USAGE_ON_TRANSLATION (FIPS过渡级别） SQL_SG_WITH_GRANT_OPTION （入门级）  
  
 SQL_SQL92_NUMERIC_VALUE_FUNCTIONS(ODBC 3.0)  
 枚举支持的驱动程序和关联的数据源的数字值标量函数，如 SQL-92 中定义 SQLUINTEGER 位掩码。  
  
 以下位掩码用于确定支持的数值的函数：  
  
 SQL_SNVF_BIT_LENGTHSQL_SNVF_CHAR_LENGTHSQL_SNVF_CHARACTER_LENGTHSQL_SNVF_EXTRACTSQL_SNVF_OCTET_LENGTHSQL_SNVF_POSITION  
  
 SQL_SQL92_PREDICATES(ODBC 3.0)  
 枚举中支持的谓词 SQLUINTEGER 位掩码**选择**语句，如 SQL-92 中定义。  
  
 此时必须支持此功能的 SQL-92 或 FIPS 符合性级别显示在每位掩码旁边的括号中。  
  
 以下位掩码用于确定数据源支持的选项：  
  
 SQL_SP_BETWEEN （入门级） SQL_SP_COMPARISON （入门级） SQL_SP_EXISTS （入门级） SQL_SP_IN （入门级） SQL_SP_ISNOTNULL （入门级） SQL_SP_ISNULL （入门级） SQL_SP_LIKE （入门级） SQL_SP_MATCH_FULL （完全级别） SQL_SP_MATCH_PARTIAL（完全级别）SQL_SP_MATCH_UNIQUE_FULL （完全级别） SQL_SP_MATCH_UNIQUE_PARTIAL （完全级别） SQL_SP_OVERLAPS （FIPS 过渡级别） SQL_SP_QUANTIFIED_COMPARISON （入门级） SQL_SP_UNIQUE （入门级）  
  
 SQL_SQL92_RELATIONAL_JOIN_OPERATORS(ODBC 3.0)  
 枚举中支持的关系联接运算符 SQLUINTEGER 位掩码**选择**语句，如 SQL-92 中定义。  
  
 此时必须支持此功能的 SQL-92 或 FIPS 符合性级别显示在每位掩码旁边的括号中。  
  
 以下位掩码用于确定数据源支持的选项：  
  
 SQL_SRJO_CORRESPONDING_CLAUSE （中级） SQL_SRJO_CROSS_JOIN （完全级别） SQL_SRJO_EXCEPT_JOIN （中级） SQL_SRJO_FULL_OUTER_JOIN （中级） SQL_SRJO_INNER_JOIN （FIPS 过渡级别） SQL_SRJO_INTERSECT_JOIN（中间级别）SQL_SRJO_LEFT_OUTER_JOIN （FIPS 过渡级别） SQL_SRJO_NATURAL_JOIN （FIPS 过渡级别） SQL_SRJO_RIGHT_OUTER_JOIN （FIPS 过渡级别） SQL_SRJO_UNION_JOIN （完全级别）  
  
 SQL_SRJO_INNER_JOIN 指示支持**内部联接**语法，不适用于内部联接功能。 为支持**内部联接**语法是 FIPS 过渡，而对内部联接功能的支持**条目**。  
  
 SQL_SQL92_REVOKE(ODBC 3.0)  
 枚举中支持的子句 SQLUINTEGER 位掩码**撤消**语句，如 SQL-92，支持的数据源中定义。  
  
 此时必须支持此功能的 SQL-92 或 FIPS 符合性级别显示在每位掩码旁边的括号中。  
  
 以下位掩码用于确定数据源支持的子句：  
  
 SQL_SR_CASCADE （FIPS 过渡级别） SQL_SR_DELETE_TABLE （入门级） SQL_SR_GRANT_OPTION_FOR （中级） SQL_SR_INSERT_COLUMN （中级） SQL_SR_INSERT_TABLE （入门级） SQL_SR_ SQL_SR_REFERENCES_COLUMN （入门级）REFERENCES_TABLE （入门级） SQL_SR_RESTRICT （FIPS 过渡级别） SQL_SR_SELECT_TABLE （入门级） SQL_SR_UPDATE_COLUMN （入门级） SQL_SR_UPDATE_TABLE （入门级） SQL_SR_USAGE_ON_ SQL_SR_USAGE_ON_DOMAIN （FIPS 过渡级别）了 CHARACTER_SET （FIPS 过渡级别） SQL_SR_USAGE_ON_COLLATION （FIPS 过渡级别） SQL_SR_USAGE_ON_TRANSLATION （FIPS 过渡级别）  
  
 SQL_SQL92_ROW_VALUE_CONSTRUCTOR(ODBC 3.0)  
 枚举支持中的行值构造函数表达式 SQLUINTEGER 位掩码**选择**语句，如 SQL-92 中定义。 以下位掩码用于确定数据源支持的选项：  
  
 SQL_SRVC_VALUE_EXPRESSION SQL_SRVC_NULL SQL_SRVC_DEFAULT SQL_SRVC_ROW_SUBQUERY  
  
 SQL_SQL92_STRING_FUNCTIONS(ODBC 3.0)  
 枚举的字符串标量函数的驱动程序和关联的数据源都支持 SQL-92 中定义 SQLUINTEGER 位掩码。  
  
 以下位掩码用于确定支持的字符串函数：  
  
 SQL_SSF_CONVERTSQL_SSF_LOWERSQL_SSF_UPPERSQL_SSF_SUBSTRINGSQL_SSF_TRANSLATESQL_SSF_TRIM_BOTHSQL_SSF_TRIM_LEADINGSQL_SSF_TRIM_TRAILING  
  
 SQL_SQL92_VALUE_EXPRESSIONS(ODBC 3.0)  
 SQL-92 中定义枚举值表达式支持，SQLUINTEGER 位掩码。  
  
 此时必须支持此功能的 SQL-92 或 FIPS 符合性级别显示在每位掩码旁边的括号中。  
  
 以下位掩码用于确定数据源支持的选项：  
  
 SQL_SVE_CASE （中级） SQL_SVE_CAST （FIPS 过渡级别） SQL_SVE_COALESCE （中级） SQL_SVE_NULLIF （中间级别）  
  
 SQL_STANDARD_CLI_CONFORMANCE (ODBC 3.0)  
 在枚举驱动程序符合标准的一个或多个标准 SQLUINTEGER 位掩码。 以下位掩码用于确定驱动程序符合哪些级别：  
  
 SQL_SCC_XOPEN_CLI_VERSION1: 驱动程序符合开放组 CLI 版本 1。  
  
 SQL_SCC_ISO92_CLI: 驱动程序符合 ISO 92 CLI。  
  
 SQL_STATIC_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 介绍驱动程序支持的静态游标属性 SQLUINTEGER 位掩码。 此位掩码包含的属性，则第一个的子集第二个子集，请参阅 SQL_STATIC_CURSOR_ATTRIBUTES2。  
  
 以下位掩码用于确定支持哪些属性：  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 有关这些位掩码的说明，请参阅 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 （和替换"静态游标"的说明中的"动态游标"）。  
  
 SQL-92 中间级别 – 符合的驱动程序通常将返回 SQL_CA1_NEXT、 SQL_CA1_ABSOLUTE 和 SQL_CA1_RELATIVE 选项受支持，因为该驱动程序支持通过嵌入 SQL 提取语句可滚动游标。 因为这不会直接确定基础 SQL 支持，但是，可滚动游标可能不受支持，即使对于 SQL-92 中间级别 – 符合的驱动程序。  
  
 SQL_STATIC_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 介绍驱动程序支持的静态游标属性 SQLUINTEGER 位掩码。 此位掩码包含属性，则第二个的子集第一个子集，请参阅 SQL_STATIC_CURSOR_ATTRIBUTES1。  
  
 以下位掩码用于确定支持哪些属性：  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 有关这些位掩码的说明，请参阅 SQL_DYNAMIC_CURSOR_ATTRIBUTES2 （和替换"静态游标"的说明中的"动态游标"）。  
  
 SQL_STRING_FUNCTIONS (ODBC 1.0)  
 注意： ODBC 1.0; 中引入的信息类型位掩码，每个带有中引入的版本。  
  
 枚举支持的驱动程序和关联的数据源的标量字符串函数 SQLUINTEGER 位掩码。  
  
 以下位掩码用于确定支持的字符串函数：  
  
 SQL_FN_STR_ASCII (ODBC 1.0) SQL_FN_STR_BIT_LENGTH (ODBC 3.0) (ODBC 1.0) SQL_FN_STR_CHAR SQL_FN_STR_CHAR_LENGTH (ODBC 3.0) (ODBC 3.0) SQL_FN_STR_CHARACTER_LENGTH SQL_FN_STR_CONCAT (ODBC 1.0) SQL_FN_STR_DIFFERENCE (ODBC 2.0) SQL_FN_STR_INSERT (ODBC1.0) SQL_FN_STR_LCASE (ODBC 1.0) SQL_FN_STR_LEFT (ODBC 1.0) SQL_FN_STR_LENGTH (ODBC 1.0) SQL_FN_STR_LOCATE (ODBC 1.0) SQL_FN_STR_LTRIM (ODBC 1.0) SQL_FN_STR_OCTET_LENGTH (ODBC 3.0) SQL_FN_STR_POSITION (ODBC 3.0) (ODBC 1.0) SQL_FN_STR_REPEAT SQL_FN_STR_REPLACE (ODBC 1.0) SQL_FN_STR_RIGHT (ODBC 1.0) SQL_FN_STR_RTRIM (ODBC 1.0) SQL_FN_STR_SOUNDEX (ODBC 2.0) SQL_FN_STR_SPACE (ODBC 2.0) SQL_FN_STR_SUBSTRING (ODBC 1.0) SQL_FN_STR_UCASE (ODBC 1.0)  
  
 如果应用程序可以调用**定位**标量函数*string_exp1*， *string_exp2*，以及*启动*参数，则驱动程序返回 SQL_FN_STR_LOCATE 位掩码。 如果应用程序可以调用具有唯一的定位标量函数*string_exp1*并*string_exp2*参数，驱动程序返回 SQL_FN_STR_LOCATE_2 位掩码。 完全支持的驱动程序**定位**标量函数返回这两个的位屏蔽。  
  
 (有关详细信息，请参阅[字符串函数](../../../odbc/reference/appendixes/string-functions.md)附录 E 中"标量函数。")  
  
 SQL_SUBQUERIES (ODBC 2.0)  
 枚举支持子查询的谓词 SQLUINTEGER 位掩码：  
  
 SQL_SQ_CORRELATED_SUBQUERIESSQL_SQ_COMPARISONSQL_SQ_EXISTSSQL_SQ_INSQL_SQ_QUANTIFIED  
  
 SQL_SQ_CORRELATED_SUBQUERIES 位掩码指示支持子查询的所有谓词都支持相关子查询。  
  
 SQL-92 条目级别 – 符合的驱动程序将始终返回在其中设置所有这些位的位掩码。  
  
 SQL_SYSTEM_FUNCTIONS (ODBC 1.0)  
 枚举支持的驱动程序和关联的数据源的标量系统函数 SQLUINTEGER 位掩码。  
  
 以下位掩码用于确定支持的系统函数：  
  
 SQL_FN_SYS_DBNAMESQL_FN_SYS_IFNULLSQL_FN_SYS_USERNAME  
  
 SQL_TABLE_TERM (ODBC 1.0)  
 表; 数据源供应商的名称字符的字符串例如，"table"或者"文件"。  
  
 此字符串可以是大写、 较低，或混合大小写。  
  
 SQL-92 条目级别 – 符合的驱动程序将始终返回"table"。  
  
 SQL_TIMEDATE_ADD_INTERVALS (ODBC 2.0)  
 枚举支持的驱动程序和 TIMESTAMPADD 标量函数的关联的数据源的时间戳时间间隔 SQLUINTEGER 位掩码。  
  
 以下位掩码用于确定支持的时间间隔：  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 FIPS 过渡的级别 – 符合的驱动程序将始终返回在其中设置所有这些位的位掩码。  
  
 SQL_TIMEDATE_DIFF_INTERVALS (ODBC 2.0)  
 枚举支持的驱动程序和 TIMESTAMPDIFF 标量函数的关联的数据源的时间戳时间间隔 SQLUINTEGER 位掩码。  
  
 以下位掩码用于确定支持的时间间隔：  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 FIPS 过渡的级别 – 符合的驱动程序将始终返回在其中设置所有这些位的位掩码。  
  
 SQL_TIMEDATE_FUNCTIONS (ODBC 1.0)  
 注意： ODBC 1.0; 中引入的信息类型位掩码，每个带有中引入的版本。  
  
 枚举的标量的日期和时间函数的驱动程序和关联的数据源支持 SQLUINTEGER 位掩码。  
  
 以下位掩码用于确定支持的日期和时间函数：  
  
 SQL_FN_TD_CURRENT_DATE ODBC 3.0) (ODBC 3.0) SQL_FN_TD_CURRENT_TIME SQL_FN_TD_CURRENT_TIMESTAMP (ODBC 3.0) (ODBC 1.0) SQL_FN_TD_CURDATE SQL_FN_TD_CURTIME (ODBC 1.0) SQL_FN_TD_DAYNAME (ODBC 2.0) SQL_FN_TD_DAYOFMONTH (ODBC 1.0) SQL_FN_TD_DAYOFWEEK (ODBC 1.0) SQL_FN_TD_DAYOFYEAR (ODBC 1.0) SQL_FN_TD_EXTRACT (ODBC 3.0) (ODBC 1.0) SQL_FN_TD_HOUR SQL_FN_TD_MINUTE (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0) SQL_FN_TD_MONTHNAME (ODBC 2.0) SQL_FN_TD_NOW (ODBC 1.0) SQL_FN_TD_QUARTER (ODBC 1.0) SQL_FN_TD_第二个 (ODBC 1.0) SQL_FN_TD_TIMESTAMPADD (ODBC 2.0) SQL_FN_TD_TIMESTAMPDIFF (ODBC 2.0) SQL_FN_TD_WEEK (ODBC 1.0) SQL_FN_TD_YEAR (ODBC 1.0)  
  
 SQL_TXN_CAPABLE (ODBC 1.0)  
 注意： ODBC 1.0; 中引入的信息类型每个返回值都标有中引入的版本。  
  
 SQLUSMALLINT 值，描述在驱动程序或数据源中的事务支持：  
  
 SQL_TC_NONE = 不支持事务。 (ODBC 1.0)  
  
 SQL_TC_DML = 事务可以包含仅数据操作语言 (DML) 语句 (**选择**，**插入**，**更新**，**删除**). 数据定义语言 (DDL) 语句在事务原因中遇到错误。 (ODBC 1.0)  
  
 SQL_TC_DDL_COMMIT = 事务可以包含仅 DML 语句。 DDL 语句 (**CREATE TABLE**， **DROP INDEX**，依次类推) 在一个事务的原因中遇到要提交的事务。 (ODBC 2.0)  
  
 SQL_TC_DDL_IGNORE = 事务可以包含仅 DML 语句。 在事务中遇到的 DDL 语句将被忽略。 (ODBC 2.0)  
  
 SQL_TC_ALL = 事务可以包含 DDL 语句和任何顺序中的 DML 语句。 (ODBC 1.0)  
  
 （为事务提供支持是 SQL-92 中必需的因为 SQL-92 符合的驱动程序 [任何级别] 将永远不会返回 SQL_TC_NONE。）  
  
 SQL_TXN_ISOLATION_OPTION (ODBC 1.0)  
 枚举驱动程序或数据源中可用的事务隔离级别 SQLUINTEGER 位掩码。  
  
 以下的位屏蔽与标志一起使用，以确定哪些选项受支持：  
  
 SQL_TXN_READ_UNCOMMITTEDSQL_TXN_READ_COMMITTEDSQL_TXN_REPEATABLE_READSQL_TXN_SERIALIZABLE  
  
 有关这些隔离级别的说明，请参阅 SQL_DEFAULT_TXN_ISOLATION 的说明。  
  
 若要设置事务隔离级别，应用程序调用**SQLSetConnectAttr**设置 SQL_ATTR_TXN_ISOLATION 属性。 有关详细信息，请参阅[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
 SQL-92 条目级别 – 符合的驱动程序将始终返回 SQL_TXN_SERIALIZABLE 所支持。 FIPS 过渡级别 – 符合的驱动程序始终将返回所有这些选项所支持。  
  
 SQL_UNION (ODBC 2.0)  
 枚举对支持 SQLUINTEGER 位掩码**UNION**子句：  
  
 SQL_U_UNION = 数据源支持**UNION**子句。  
  
 SQL_U_UNION_ALL = 数据源支持**所有**中的关键字**UNION**子句。 (**SQLGetInfo**这种情况下返回 SQL_U_UNION 和 SQL_U_UNION_ALL。)  
  
 SQL-92 条目级别 – 符合的驱动程序将始终返回这两种选项所支持。  
  
 SQL_USER_NAME (ODBC 1.0)  
 具有特定的数据库，可以不同于登录名中使用的名称的字符字符串。  
  
 SQL_XOPEN_CLI_YEAR (ODBC 3.0)  
 表示与该版本的 ODBC 驱动程序管理器完全符合 Open Group 规范的发布的年份的字符串。  
  
 SQL_ACCESSIBLE_PROCEDURES (ODBC 1.0)  
 一个字符串:"Y"，如果用户可以执行所有过程返回的**SQLProcedures**;"N"如果可能有过程返回，用户不能执行。  
  
 SQL_ACCESSIBLE_TABLES (ODBC 1.0)  
 一个字符串:"Y"，如果用户保证**选择**返回的所有表的特权**SQLTables**;"N"如果可能存在的表返回该用户无法访问。  
  
 SQL_ACTIVE_ENVIRONMENTS (ODBC 3.0)  
 SQLUSMALLINT 值，该值指定该驱动程序可以支持的活动环境的最大数目。 如果没有指定的限制或未知的限制，则将此值设置为零。  
  
 SQL_AGGREGATE_FUNCTIONS (ODBC 3.0)  
 枚举对聚合函数的支持 SQLUINTEGER 位掩码：  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 SQL-92 条目级别 – 符合的驱动程序始终将返回所有这些选项所支持。  
  
 SQL_ALTER_DOMAIN (ODBC 3.0)  
 枚举中的子句 SQLUINTEGER 位掩码**ALTER 域**语句，如 SQL-92，支持的数据源中定义。 完整 SQL-92 的兼容级别的驱动程序将始终返回所有的位屏蔽。 返回值"0"意味着**ALTER 域**不支持语句。  
  
 此时必须支持此功能的 SQL-92 或 FIPS 符合性级别显示在每位掩码旁边的括号中。  
  
 以下位掩码用于确定支持的子句：  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = 的添加支持域约束 （完全级别）  
  
 SQL_AD_ADD_DOMAIN_DEFAULT = \<alter 域 > \<set 域默认子句 > 支持 （完全级别）  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION =\<约束名称定义子句 > 命名域约束 （中级） 支持  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT =\<删除域约束子句 > 支持 （完全级别）  
  
 SQL_AD_DROP_DOMAIN_DEFAULT = \<alter 域 >\<删除域默认子句 > 支持 （完全级别）  
  
 以下位指定受支持\<约束属性 > 如果\<添加域约束 > 支持 （SQL_AD_ADD_DOMAIN_CONSTRAINT 位设置）：  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE （完全级别） SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE （完全级别） SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED （完全级别） SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE （完全级别）  
  
 SQL_ALTER_TABLE (ODBC 2.0)  
 枚举中的子句 SQLUINTEGER 位掩码**ALTER TABLE**数据源支持的语句。  
  
 此时必须支持此功能的 SQL-92 或 FIPS 符合性级别显示在每位掩码旁边的括号中。  
  
 以下位掩码用于确定支持的子句：  
  
 SQL_AT_ADD_COLUMN_COLLATION =\<将列添加 > 支持子句，使用工具来指定列排序规则 （完全级别） (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT =\<将列添加 > 支持子句，使用工具来指定列默认值 （FIPS 过渡级别） (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_SINGLE =\<将列添加 > 是支持 （FIPS 过渡级别） (ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT =\<将列添加 > 支持子句，使用工具来指定列约束 （FIPS 过渡级别） (ODBC 3.0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT =\<添加表约束 > 支持子句 （FIPS 过渡级别） (ODBC 3.0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION =\<约束名称定义 > 命名列和表约束 （中级） 支持 (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_CASCADE =\<删除列 > 支持级联 （FIPS 过渡级别） (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT =\<更改列 > \<drop 列默认子句 > 是支持 （中级） (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT =\<删除列 > 支持限制 （FIPS 过渡级别） (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT =\<删除列 > 支持限制 （FIPS 过渡级别） (ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT =\<更改列 > \<set 列默认子句 > 是支持 （中级） (ODBC 3.0)  
  
 以下位指定的支持\<约束属性 > 如果支持指定列或表的约束 （SQL_AT_ADD_CONSTRAINT 位设置）：  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED （完全级别） (ODBC 3.0) SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE （完全级别） (ODBC 3.0) SQL_AT_CONSTRAINT_DEFERRABLE （完全级别） (ODBC 3.0) SQL_AT_CONSTRAINT_NON_DEFERRABLE （完全级别） (ODBC 3.0)  
  
 SQL_ASYNC_MODE (ODBC 3.0)  
 SQLUINTEGER 值，该值指示驱动程序中的异步支持的级别：  
  
 SQL_AM_CONNECTION = 的连接支持级别的异步执行。 与给定的连接句柄关联的所有语句句柄都处于异步模式，或者所有都都在同步模式。 在连接上的语句句柄不能为在异步模式下，在同一连接上的另一个语句句柄时在同步模式下，反之亦然。  
  
 SQL_AM_STATEMENT = 支持级别的异步执行的语句。 而在同一连接上的其他语句句柄是在同步模式下，在异步模式下，可以是一些与连接句柄相关联的语句句柄。  
  
 SQL_AM_NONE = 异步模式下不支持。  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 枚举与行的可用性相关驱动程序的行为 SQLUINTEGER 位掩码对进行计数。 以下的位屏蔽可以与信息类型一起使用：  
  
 SQL_BRC_ROLLED_UP = 行计数的连续的 INSERT、 DELETE 或 UPDATE 语句将累加起来，为一个。 如果未设置此位，行计数是可用于每个语句。  
  
 SQL_BRC_PROCEDURES = 行计数，如果任何，当某一批处理执行存储过程中时才可用。 如果提供行计数，则他们可以将其回滚或单独可用，具体取决于 SQL_BRC_ROLLED_UP 位。  
  
 SQL_BRC_EXPLICIT = 行计数，如果某一批处理执行直接通过调用时，任何，有可用**SQLExecute**或**SQLExecDirect**。 如果提供行计数，则他们可以将其回滚或单独可用，具体取决于 SQL_BRC_ROLLED_UP 位。  
  
## <a name="example"></a>示例  
 **SQLGetInfo**为 SQLUINTEGER 位掩码中返回的受支持的选项列表 **InfoValuePtr*。 每个选项的位掩码与标志一起使用，以确定是否支持的选项。  
  
 例如，应用程序可以使用以下代码以确定是否与连接关联的驱动程序支持的子字符串标量函数。  
  
 有关使用的另一个示例**SQLGetInfo**，请参阅[SQLTables 函数](../../../odbc/reference/syntax/sqltables-function.md)。  
  
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
  
 返回语句属性的设置  
 [SQLGetStmtAttr 函数](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)  
  
 返回有关数据源的数据类型的信息  
 [SQLGetTypeInfo 函数](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
