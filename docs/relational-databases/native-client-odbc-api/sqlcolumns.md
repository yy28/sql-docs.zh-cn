---
title: SQL柱 |微软文档
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLColumns function
ms.assetid: 69d3af44-8196-43ab-8037-cdd06207b171
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: abce98b64da8de6039f81025201cce25269763a6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302602"
---
# <a name="sqlcolumns"></a>SQLColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **SQLColumn**返回SQL_SUCCESS*目录名称*、*表名*或*列名*参数是否存在值。 当在这些参数中使用无效值时 **，SQLFetch**将返回SQL_NO_DATA。  
  
> [!NOTE]  
>  对于大值类型，将返回值为 SQL_SS_LENGTH_UNLIMITED 的所有长度参数。  
  
 **SQLColumns**可以在静态服务器游标上执行。 尝试在可上升（动态或键集）游标上执行**SQLColumns**将返回SQL_SUCCESS_WITH_INFO指示游标类型已更改。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序通过接受*目录名称*参数的两部分名称 *（Linked_Server_Name.Catalog_Name*）支持报告链接服务器上的表的信息。  
  
 对于 ODBC 2。*x*应用程序不使用*表名*中的通配符 **，SQLColumns**返回有关名称与*表Name*匹配且归当前用户拥有的任何表的信息。 如果当前用户没有名称与*表Name*参数匹配的表 **，SQLColumns**将返回有关表名称与*表Name*参数匹配的其他用户拥有的任何表的信息。 对于 ODBC 2。*x*应用程序使用通配符 **，SQLColumns**返回名称与*表名称*匹配的所有表。 对于 ODBC 3。*x*应用程序**SQLColumns**返回名称与*表Name*匹配的所有表，而不考虑所有者或是否使用通配符。  
  
 下表列出了结果集返回的列：  
  
|列名称|描述|  
|-----------------|-----------------|  
|DATA_TYPE|返回**varchar（最大）** 数据类型的SQL_VARCHAR、SQL_VARBINARY或SQL_WVARCHAR。|  
|TYPE_NAME|返回**varchar（最大值）、varbinary（max）** 和**nvarchar（max）** 数据类型的**varbinary(max)**"varchar"、"varbinary"或"nvarchar"。|  
|COLUMN_SIZE|返回**SQL_SS_LENGTH_UNLIMITED varchar（max）** 数据类型，指示列的大小不受限制。|  
|BUFFER_LENGTH|返回**varchar（max）** 数据类型的SQL_SS_LENGTH_UNLIMITED，指示缓冲区的大小不受限制。|  
|SQL_DATA_TYPE|返回**varchar（最大）** 数据类型的SQL_VARCHAR、SQL_VARBINARY或SQL_WVARCHAR。|  
|CHAR_OCTET_LENGTH|返回字符或二进制列的最大长度。 返回 0 表示大小不受限制。|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|返回在其中定义 XML 架构集合名称的目录的名称。 如果找不到目录名称，则此变量包含空字符串。|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|返回在其中定义 XML 架构集合名称的架构的名称。 如果找不到架构名称，则此变量包含空字符串。|  
|SS_XML_SCHEMACOLLECTION_NAME|返回 XML 架构集合的名称。 如果找不到此名称，则此变量包含空字符串。|  
|SS_UDT_CATALOG_NAME|包含 UDT（用户定义类型）的目录的名称。|  
|SS_UDT_SCHEMA_NAME|包含 UDT 的架构的名称。|  
|SS_UDT_ASSEMBLY_TYPE_NAME|UDT 的程序集限定名称。|  
  
 对于 UDT，现有的TYPE_NAME列用于指示 UDT 的名称;对于 UDT，则使用"已使用"列"来指示 UDT 的名称。因此，不应将其附加列添加到**SQLColumn**或[SQLAColumn](../../relational-databases/native-client-odbc-api/sqlprocedurecolumns.md)的结果集中。 UDT 列或参数的 DATA_TYPE 为 SQL_SS_UDT。  
  
 对于 UDT 参数，您可以使用上面定义的特定于驱动程序的新描述符来获取或设置 UDT 的额外元数据数据，条件是服务器返回或需要此信息。  
  
 当客户端连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SQLColumns 并调用 SQLColumns 时，使用目录输入参数的 NULL 或通配符值将不会从其他目录中返回信息。 而只返回有关当前目录的信息。 客户端可以首先调用 SQLTables 以确定所需表所在的目录中。 然后，客户端可以在对 SQLColumns 的调用中使用目录输入参数的目录值来检索有关该表中列的信息。  
  
## <a name="sqlcolumns-and-table-valued-parameters"></a>SQLColumns 和表值参数  
 SQLColumns 返回的结果集取决于SQL_SOPT_SS_NAME_SCOPE设置。 有关详细信息，请参阅[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。 已针对表值参数添加以下列：  
  
|列名称|数据类型|目录|  
|-----------------|---------------|--------------|  
|SS_IS_COMPUTED|Smallint|对于 TABLE_TYPE 中的列，如果该列是一个计算列，则为 SQL_TRUE；否则为 SQL_FALSE。|  
|SS_IS_IDENTITY|Smallint|如果该列为标识列，则为 SQL_TRUE；否则为 SQL_FALSE。|  
  
 有关表值参数的详细信息，请参阅[&#40;ODBC&#41;的表值参数](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlcolumns-support-for-enhanced-date-and-time-features"></a>SQLColumns 对日期和时间增强功能的支持  
 有关日期/时间类型返回的值的信息，请参阅[目录元数据](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md)。  
  
 有关详细信息，请参阅[&#40;ODBC&#41;的日期和时间改进](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlcolumns-support-for-large-clr-udts"></a>SQLColumns 对大型 CLR UDT 的支持  
 **SQLColumns**支持大型 CLR 用户定义类型 （UDT）。 有关详细信息，请参阅[&#40;ODBC&#41;的大型 CLR 用户定义类型](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="sqlcolumns-support-for-sparse-columns"></a>SQLColumns 对稀疏列的支持  
 已[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将两个特定列添加到 SQLColumns 的结果集中：  
  
|列名称|数据类型|描述|  
|-----------------|---------------|-----------------|  
|SS_IS_SPARSE|**斯莫尔因特**|如果该列为稀疏列，则为 SQL_TRUE；否则为 SQL_FALSE。|  
|SS_IS_COLUMN_SET|**斯莫尔因特**|如果列是**column_set**列，则SQL_TRUE;否则，SQL_FALSE。|  
  
 与 ODBC 规范一致，SS_IS_SPARSE和SS_IS_COLUMN_SET出现在所有驱动程序特定的列之前，这些列添加到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本早于[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]之前，并在 ODBC 本身要求的所有列之后。  
  
 SQLColumns 返回的结果集取决于SQL_SOPT_SS_NAME_SCOPE设置。 有关详细信息，请参阅[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
 有关 ODBC 中的稀疏列的详细信息，请参阅[稀疏列支持&#40;ODBC&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLColumns 函数](https://go.microsoft.com/fwlink/?LinkId=59336)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
