---
title: SQLGetInfo （视觉福克斯Pro ODBC驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetInfo function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: fbc39e3d-67d9-4331-bf5f-76dbd74c4c45
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2d4b976083b46bf632c4890c7fce3b0f13a9a761
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295187"
---
# <a name="sqlgetinfo-visual-foxpro-odbc-driver"></a>SQLGetInfo（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 特定于驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 支持： 完整  
  
 ODBC API 符合性：1 级  
  
 返回有关 Visual FoxPro ODBC 驱动程序和与连接句柄*hdbc*关联的数据源的一般信息。 下面的列表显示了 Visual FoxPro ODBC 驱动程序为每个*fInfoType*参数返回的值，以及有关返回值的注释。  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLGetInfo。](../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
## <a name="a"></a>A  
 SQL_ACCESSIBLE_PROCEDURES返回"N"。  
  
 SQL_ACCESSIBLE_TABLES返回"Y"。  
  
 SQL_ACTIVE_CONNECTIONS返回 0。  
  
 SQL_ACTIVE_STATEMENTS返回 0。  
  
 SQL_ALTER_TABLE返回SQL_AT_ADD_COLUMN或SQL_AT_DROP_COLUMN。  
  
## <a name="b"></a>B  
 SQL_BOOKMARK_PERSISTENCE返回SQL_BP_SCROLL。  
  
## <a name="c"></a>C  
 SQL_COLUMN_ALIAS返回"Y"。  
  
 SQL_CONCAT_NULL_BEHAVIOR返回SQL_CB_NULL。  
  
 SQL_CONVERT_BIGINT返回 0。 视觉福克斯Pro ODBC驱动程序不支持*Bigint。*  
  
 SQL_CONVERT_BINARY返回 0。  
  
 SQL_CONVERT_BIT返回 0。  
  
 SQL_CONVERT_CHAR返回 0。  
  
 SQL_CONVERT_DATE返回 0。  
  
 SQL_CONVERT_DECIMAL返回 0。  
  
 SQL_CONVERT_DOUBLE返回 0。  
  
 SQL_CONVERT_FLOAT返回 0。  
  
 SQL_CONVERT_INTEGER返回 0。  
  
 SQL_CONVERT_LONGVARBINARY返回 0。  
  
 SQL_CONVERT_LONGVARCHAR返回 0。  
  
 SQL_CONVERT_NUMERIC返回 0。  
  
 SQL_CONVERT_REAL返回 0。  
  
 SQL_CONVERT_SMALLINT返回 0。  
  
 SQL_CONVERT_TIME返回 0。  
  
 SQL_CONVERT_TIMESTAMP返回 0。  
  
 SQL_CONVERT_TINYINT返回 0。  
  
 SQL_CONVERT_VARBINARY返回 0。  
  
 SQL_CONVERT_VARCHAR返回 0。  
  
 SQL_CONVERT_FUNCTIONS返回 0。  
  
 SQL_CORRELATION_NAME返回SQL_CN_ANY。  
  
 SQL_CURSOR_COMMIT_BEHAVIOR返回SQL_CB_PRESERVE。  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR返回SQL_CB_PRESERVE。  
  
## <a name="d"></a>D  
 SQL_DATA_SOURCE_NAME返回作为 DSN 传递到[SQLConnect](../../odbc/microsoft/sqlconnect-visual-foxpro-odbc-driver.md)的值 ，或[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md);如果未指定 DSN，则返回空字符串。  
  
 SQL_DATA_SOURCE_READ_ONLY返回"N"。  
  
 如果数据源是[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)，SQL_DATABASE_NAME将完整的 UNC 路径返回到当前数据库。 如果数据源连接到[表](../../odbc/microsoft/visual-foxpro-terminology.md)的目录，则函数将路径返回到该目录。  
  
 SQL_DBMS_NAME返回"视觉福克斯专业"。  
  
 SQL_DBMS_VER返回"03.00.0000"。  
  
 SQL_DEFAULT_TXN_ISOLATION返回SQL_TXN_READ_COMMITTED。 脏读是不可能的，但不可重复读取和幻象是可能的。  
  
 SQL_DRIVER_HDBC由驱动程序管理器实施。  
  
 SQL_DRIVER_HENV由驱动程序管理器实施。  
  
 SQL_DRIVER_HLIB由驱动程序管理器实现。  
  
 SQL_DRIVER_HSTMT由驱动程序管理器实施。  
  
 SQL_DRIVER_NAME返回"vfpodbc.dll"。  
  
 SQL_DRIVER_ODBC_VER返回"02.50"（SQL_SPEC_MAJOR，SQL_SPEC_MINOR）。  
  
 SQL_DRIVER_VER返回"01.00.0000"。  
  
## <a name="e"></a>E  
 SQL_EXPRESSIONS_IN_ORDERBY返回"N"。  
  
## <a name="f"></a>F  
 SQL_FETCH_DIRECTION返回：  
  
-   SQL_FD_FETCH_NEXT  
  
-   SQL_FD_FETCH_FIRST  
  
-   SQL_FD_FETCH_LAST  
  
-   SQL_FD_FETCH_PRIOR  
  
-   SQL_FD_FETCH_ABSOLUTE  
  
-   SQL_FD_FETCH_RELATIVE  
  
-   SQL_FD_FETCH_BOOKMARK  
  
 SQL_FILE_USAGE返回数据库 （.dbc 文件） 和可用表 （.dbf 文件） 数据源SQL_FILE_QUALIFIER。  
  
## <a name="g-h"></a>G-H  
 SQL_GETDATA_EXENSIONS返回：  
  
-   SQL_GD_ANY_COLUMN  
  
-   SQL_GD_ANY_BLOCK  
  
-   SQL_GD_ANY_BOUND  
  
-   SQL_GD_ANY_ORDER  
  
 SQL_GROUP_BY返回SQL_GB_NO_RELATION。  
  
## <a name="i-j"></a>I-J  
 SQL_IDENTIFIER_CASE返回SQL_IC_MIXED。  
  
 SQL_IDENTIFIER_QUOTE_CHAR返回'  
  
## <a name="k"></a>K  
 SQL_KEYWORDS返回""。  
  
## <a name="l"></a>L  
 SQL_LIKE_ESCAPE_CLAUSE返回"N"。  
  
 SQL_LOCK_TYPES返回SQL_LCK_NO_CHANGE。  
  
## <a name="m"></a>M  
 SQL_MAX_BINARY_LITERAL_LEN返回 0。  
  
 SQL_MAX_CHAR_LITERAL_LEN返回 254。  
  
 SQL_MAX_COLUMN_NAME_LEN返回 128。  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY返回 16。  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY返回 16。  
  
 SQL_MAX_COLUMNS_IN_INDEX返回 0。  
  
 SQL_MAX_COLUMNS_IN_SELECT返回 254。  
  
 SQL_MAX_COLUMNS_IN_TABLE返回 254。  
  
 SQL_MAX_CURSOR_NAME_LEN返回 254。  
  
 SQL_MAX_INDEX_SIZE返回 0。  
  
 SQL_MAX_OWNER_NAME_LEN返回 0。  
  
 SQL_MAX_PROCEDURE_NAME_LEN返回 0。 Visual FoxPro ODBC 驱动程序不允许直接访问 Visual FoxPro 存储过程。  
  
 SQL_MAX_QUALIFIER_NAME_LEN返回最大操作系统路径长度。  
  
 SQL_MAX_ROW_SIZE返回 254⁄2。  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG返回"N"。  
  
 SQL_MAX_STATEMENT_LEN返回 8192。  
  
 SQL_MAX_TABLE_NAME_LEN返回 128。  
  
 SQL_MAX_TABLES_IN_SELECT返回 16。  
  
 SQL_MAX_USER_NAME_LEN返回 0。  
  
 SQL_MULT_RESULT_SETS返回"Y"。  
  
 SQL_MULTIPLE_ACTIVE_TXN返回"Y"。 多个连接可以同时打开多个事务。  
  
## <a name="n"></a>N  
 SQL_NEED_LONG_DATA_LEN返回"N"。  
  
 SQL_NON_NULLABLE_COLUMNS返回SQL_NNC_NON_NULL。  
  
 SQL_NULL_COLLATION返回SQL_NC_LOW。  
  
 SQL_NUMERIC_FUNCTIONS返回除 SQL_FN_NUM_POWER之外的所有功能，该功能不受 Visual FoxPro ODBC 驱动程序的支持。 支持以下功能：  
  
-   SQL_FN_NUM_ABS  
  
-   SQL_FN_NUM_ACOS  
  
-   SQL_FN_NUM_ASIN  
  
-   SQL_FN_NUM_ATAN  
  
-   SQL_FN_NUM_ATAN2  
  
-   SQL_FN_NUM_CELING  
  
-   SQL_FN_NUM_COS  
  
-   SQL_FN_NUM_COT  
  
-   SQL_FN_NUM_DEGREES  
  
-   SQL_FN_NUM_EXP  
  
-   SQL_FN_NUM_FLOOR  
  
-   SQL_FN_NUM_LOG  
  
-   SQL_FN_NUM_LOG10  
  
-   SQL_FN_NUM_MOD  
  
-   SQL_FN_NUM_PI  
  
-   SQL_FN_NUM_RADIANS  
  
-   SQL_FN_NUM_RAND  
  
-   SQL_FN_NUM_ROUND  
  
-   SQL_FN_NUM_SIGN  
  
-   SQL_FN_NUM_SIN  
  
-   SQL_FN_NUM_SQRT  
  
-   SQL_FN_NUM_TAN  
  
## <a name="o"></a>O  
 SQL_ODBC_API_CONFORMANCE返回SQL_OAC_LEVEL1。  
  
 SQL_ODBC_SAG_CLI_CONFORMANCE返回SQL_OSCC_COMPLIANT。  
  
 SQL_ODBC_SQL_CONFORMANCE返回SQL_OSC_MINIMUM。 支持最小 SQL 语法。  
  
 SQL_ODBC_SQL_OPT_IEF返回"N"。  
  
 SQL_ODBC_VER由驱动程序管理器实施。  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT返回"N"。  
  
 SQL_OUTER_JOINS返回"N"。  
  
 SQL_OWNER_TERM返回""。 Visual FoxPro ODBC 驱动程序不支持其对象的所有者。  
  
 SQL_OWNER_USAGE返回 0。 Visual FoxPro ODBC 驱动程序不支持其对象的所有者。  
  
## <a name="p"></a>P  
 SQL_POS_OPERATIONS返回SQL_POS_POSITION。  
  
 SQL_POSITIONED_STATEMENTS返回 0。  
  
 SQL_PROCEDURE_TERM返回""。  
  
 SQL_PROCEDURES返回"N"。  
  
## <a name="q"></a>Q  
 SQL_QUALIFIER_LOCATION返回SQL_QL_START。  
  
 SQL_QUALIFIER_NAME_SEPARATOR返回"！"或""。\\ 数据库和表之间的分隔符是连接到[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)的数据源的"！"，对于作为[可用表](../../odbc/microsoft/visual-foxpro-terminology.md)目录的数据源\\的"！"。  
  
 SQL_QUALIFIER_TERM返回"数据库"或"目录"。 限定符是连接到[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)的数据源的"数据库"，是[作为可用表](../../odbc/microsoft/visual-foxpro-terminology.md)目录的数据源的"目录"。  
  
 SQL_QUALIFIER_USAGE不支持SQL_QU_PRIVILEGE_DEFINITION;它返回SQL_QU_DML_STATEMENT或SQL_QU_TABLE_DEFINITION。  
  
 SQL_QUOTED_IDENTIFIER_CASE返回SQL_IC_MIXED。  
  
## <a name="r"></a>R  
 SQL_ROW_UPDATES返回"N"。 可视化 FoxPro ODBC 驱动程序仅支持静态和正向光标。  
  
## <a name="s"></a>S  
 SQL_SCROLL_CONCURRENCY返回SQL_SCCO_READ_ONLY。  
  
 SQL_SCROLL_OPTIONS返回SQL_SO_STATIC或SQL_SO_READONLY。  
  
 SQL_SEARCH_PATTERN_ESCAPE返回"\\  
  
 SQL_SERVER_NAME返回""。  
  
 SQL_SPECIAL_CHARACTERS返回"[$%]"。  
  
 SQL_STATIC_SENSITIVITY返回 0。 可视化 FoxPro ODBC 驱动程序不支持位置更新。  
  
 SQL_STRING_FUNCTIONS不支持SQL_FN_STR_INSERT、SQL_FN_STR_LOCATE、SQL_FN_STR_LOCATE_2或SQL_FN_STR_SOUNDEX。  
  
 将返回：  
  
-   SQL_FN_STR_ASCII  
  
-   SQL_FN_STR_CHAR  
  
-   SQL_FN_STR_CONCAT  
  
-   SQL_FN_STR_DIFFERENCE  
  
-   SQL_FN_STR_LCASE  
  
-   SQL_FN_STR_LEFT  
  
-   SQL_FN_STR_LENGTH  
  
-   SQL_FN_STR_LTRIM  
  
-   SQL_FN_STR_REPEAT  
  
-   SQL_FN_STR_REPLACE  
  
-   SQL_FN_STR_RIGHT  
  
-   SQL_FN_STR_RTRIM  
  
-   SQL_FN_STR_SUBSTRING  
  
-   SQL_FN_STR_UCASE  
  
-   SQL_FN_STR_SPACE  
  
 SQL_SUBQUERIES返回：  
  
-   SQL_SQ_CORRELATED_SUBQUERIES  
  
-   SQL_SQ_COMPARISON  
  
-   SQL_SQ_EXISTS  
  
-   SQL_SQ_IN  
  
-   SQL_SQ_QUANTIFIED  
  
 SQL_SYSTEM_FUNCTIONS返回：  
  
-   SQL_FN_SYS_DBNAME  
  
-   SQL_FN_SYS_IFNULL  
  
 但不是：  
  
-   SQL_FN_SYS_USERNAME  
  
## <a name="t"></a>T  
 SQL_TABLE_TERM返回"表"。  
  
 SQL_TIMEDATE_ADD_INTERVALS返回：  
  
-   SQL_FN_TSI_秒  
  
-   SQL_FN_TSI_MINUTE  
  
-   SQL_FN_TSI_HOUR  
  
-   SQL_FN_TSI_DAY  
  
-   SQL_FN_TSI_MONTH  
  
-   SQL_FN_TSI_YEAR  
  
 但不是：  
  
-   SQL_FN_TSI_FRAC_SECOND  
  
-   SQL_FN_TSI_WEEK  
  
-   SQL_FN_TSI_QUARTER  
  
 SQL_TIMEDATE_DIFF_INTERVALS返回：  
  
-   SQL_FN_TSI_秒  
  
-   SQL_FN_TSI_MINUTE  
  
-   SQL_FN_TSI_HOUR  
  
-   SQL_FN_TSI_DAY  
  
-   SQL_FN_TSI_MONTH  
  
-   SQL_FN_TSI_YEAR  
  
 SQL_TIMEDATE_FUNCTIONS不支持SQL_FN_TD_QUARTER、SQL_FN_TD_TIMESTAMPADD、SQL_FN_TD_DAYOFYEAR或SQL_FN_TD_WEEK。  
  
 将返回：  
  
-   SQL_FN_TD_CURDATE  
  
-   SQL_FN_TD_CURTIME  
  
-   SQL_FN_TD_DAYNAME  
  
-   SQL_FN_TD_DAYOFMONTH  
  
-   SQL_FN_TD_DAYOFWEEK  
  
-   SQL_FN_TD_HOUR  
  
-   SQL_FN_TD_MINUTE  
  
-   SQL_FN_TD_MONTH  
  
-   SQL_FN_TD_MONTHNAME  
  
-   SQL_FN_TD_NOW  
  
-   SQL_FN_TD_SECOND  
  
-   SQL_FN_TD_TIMESTAMPDIFF  
  
-   SQL_FN_TD_YEAR 。  
  
 SQL_TXN_CAPABLE返回SQL_TC_DML。  
  
 SQL_TXN_ISOLATION_OPTION返回SQL_TXN_READ_COMMITTED。  
  
## <a name="u-z"></a>U-Z  
 SQL_UNION返回SQL_U_UNION或SQL_U_UNION_ALL。  
  
 SQL_USER_NAME返回\<空>。
