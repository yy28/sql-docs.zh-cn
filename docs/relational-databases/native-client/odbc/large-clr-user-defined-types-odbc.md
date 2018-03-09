---
title: "大型 CLR 用户定义类型 (ODBC) |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|ODBC
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ODBC, large user-defined types
- large user-defined types [ODBC]
ms.assetid: ddce337e-bb6e-4a30-b7cc-4969bb1520a9
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4da32a24c00ca9539cca04c3886d19f73f9ab578
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="large-clr-user-defined-types-odbc"></a>大型 CLR 用户定义类型 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  本主题讨论 SQL Server Native Client 中为支持大型公共语言运行时 (CLR) 用户定义类型 (UDT) 而对 ODBC 进行的更改。  
  
 显示针对大型 CLR Udt 的 ODBC 支持的示例，请参阅[支持大型 udt](../../../relational-databases/native-client-odbc-how-to/support-for-large-udts.md)。  
  
 有关 SQL Server 本机客户端中的大型 CLR Udt 支持的详细信息，请参阅[Large CLR User-Defined 类型](../../../relational-databases/native-client/features/large-clr-user-defined-types.md)。  
  
## <a name="data-format"></a>数据格式  
 SQL Server Native Client 使用 SQL_SS_LENGTH_UNLIMITED 来指示大型对象 (LOB) 类型的列大小大于 8,000 个字节。 从 SQL Server 2008 开始，在其大小大于 8,000 个字节时将相同的值用于 CLR UDT。  
  
 UDT 值表示为字节数组。 支持与十六进制字符串之间的转换。 文字值表示为带有“0x”前缀的十六进制字符串。  
  
 下表显示了参数和结果集中的数据类型映射：  
  
|SQL Server 数据类型|SQL 数据类型|“值”|  
|--------------------------|-------------------|-----------|  
|CLR UDT|SQL_SS_UDT|-151 (sqlncli.h)|  
  
 下表介绍相应的结构和 ODBC C 类型。 从根本上讲，CLR UDT 是**varbinary**使用其他元数据的类型。  
  
|SQL 数据类型|内存布局|C 数据类型|值 (sqlext.h)|  
|-------------------|-------------------|-----------------|------------------------|  
|SQL_SS_UDT|SQLCHAR * (无符号 char \*)|SQL_C_BINARY|SQL_BINARY (-2)|  
  
## <a name="descriptor-fields-for-parameters"></a>参数的描述符字段  
 IPD 字段中返回的信息如下所示：  
  
|描述符字段|SQL_SS_UDT<br /><br /> （长度小于或等于 8,000 个字节）|SQL_SS_UDT<br /><br /> （长度大于 8000 个字节）|  
|----------------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CONCISE_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_DATETIME_INTERVAL_CODE|0|0|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_LOCAL_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_OCTET_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_SCALE|0|0|  
|SQL_DESC_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_UNSIGNED|SQL_TRUE|SQL_TRUE|  
|SQL_CA_SS_UDT_CATALOG_NAME|包含用户定义的类型的目录的名称。|包含用户定义的类型的目录的名称。|  
|SQL_CA_SS_UDT_SCHEMA_NAME|包含 UDT 的架构的名称。|架构的名称包含用户定义的类型。|  
|SQL_CA_SS_UDT_TYPE_NAME|UDT 的名称。|UDT 的名称。|  
|SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME|UDT 的完全限定名称。|UDT 的完全限定名称。|  
  
 对于 UDT 参数，SQL_CA_SS_UDT_TYPE_NAME 必须始终可以通过设置**SQLSetDescField**。 SQL_CA_SS_UDT_CATALOG_NAME 和 SQL_CA_SS_UDT_SCHEMA_NAME 是可选的。  
  
 如果使用与表不同的架构在同一数据库中定义 UDT，则必须设置 SQL_CA_SS_UDT_SCHEMA_NAME。  
  
 如果在与表不同的数据库中定义 UDT，则必须设置 SQL_CA_SS_UDT_CATALOG_NAME 和 SQL_CA_SS_UDT_SCHEMA_NAME。  
  
 如果在 SQL_CA_SS_UDT_TYPE_NAME、SQL_CA_SS_UDT_CATALOG_NAME 或 SQL_CA_SS_UDT_SCHEMA_NAME 的设置中存在错误或遗漏，则生成具有 SQLSTATE HY000 和服务器特定消息文本的诊断记录。  
  
## <a name="descriptor-fields-for-results"></a>结果的描述符字段  
 IRD 字段中返回的信息如下所示：  
  
|描述符字段|SQL_SS_UDT<br /><br /> （长度小于或等于 8,000 个字节）|SQL_SS_UDT<br /><br /> （长度大于 8000 个字节）|  
|----------------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CONCISE_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_DATETIME_INTERVAL_CODE|0|0|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_DISPLAY_SIZE|2*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_LITERAL_PREFIX|"0x"|"0x"|  
|SQL_DESC_LITERAL_SUFFIX|""|""|  
|SQL_DESC_LOCAL_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_OCTET_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_SCALE|0|0|  
|SQL_DESC_SEARCHABLE|SQL_PRED_NONE|SQL_PRED_NONE|  
|SQL_DESC_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_UNSIGNED|SQL_TRUE|SQL_TRUE|  
|SQL_CA_SS_UDT_CATALOG_NAME|包含用户定义的类型的目录的名称。|包含用户定义的类型的目录的名称。|  
|SQL_CA_SS_UDT_SCHEMA_NAME|包含 UDT 的架构的名称。|包含 UDT 的架构的名称。|  
|SQL_CA_SS_UDT_TYPE_NAME|UDT 的名称。|UDT 的名称。|  
|SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME|UDT 的完全限定名称。|UDT 的完全限定名称。|  
  
## <a name="column-metadata-returned-by-sqlcolumns-and-sqlprocedurecolumns-catalog-metadata"></a>SQLColumns 和 SQLProcedureColumns 返回的列元数据（目录元数据）  
 为 UDT 返回以下列值：  
  
|列名|SQL_SS_UDT<br /><br /> （长度小于或等于 8,000 个字节）|SQL_SS_UDT<br /><br /> （长度大于 8000 个字节）|  
|-----------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|DATA_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|TYPE_NAME|UDT 的名称。|UDT 的名称。|  
|COLUMN_SIZE|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|BUFFER_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|DECIMAL_DIGITS|NULL|NULL|  
|SQL_DATA_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DATETIME_SUB|NULL|NULL|  
|CHAR_OCTET_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SS_UDT_CATALOG_NAME|包含用户定义的类型的目录的名称。|包含用户定义的类型的目录的名称。|  
|SS_UDT_SCHEMA_NAME|包含 UDT 的架构的名称。|包含 UDT 的架构的名称。|  
|SS_UDT_ASSEMBLY_TYPE_NAME|UDT 的完全限定名称。|UDT 的完全限定名称。|  
  
 最后三列是驱动程序特定的列。 它们将添加之后任何 ODBC 定义的列，但之前 SQLColumns 或 SQLProcedureColumns 的结果集的任何现有驱动程序的特定列。  
  
 为单个 Udt 或泛型类型"udt"，SQLGetTypeInfo，会不返回任何行。  
  
## <a name="bindings-and-conversions"></a>绑定和转换  
 支持的从 SQL 到 C 数据类型的转换如下所示：  
  
|转换的目标和源：|SQL_SS_UDT|  
|-----------------------------|------------------|  
|SQL_C_WCHAR|支持 *|  
|SQL_C_BINARY|Supported|  
|SQL_C_CHAR|支持 *|  
  
 \*二进制数据转换为十六进制字符串。  
  
 支持的从 C 到 SQL 数据类型的转换如下所示：  
  
|转换的目标和源：|SQL_SS_UDT|  
|-----------------------------|------------------|  
|SQL_C_WCHAR|支持 *|  
|SQL_C_BINARY|Supported|  
|SQL_C_CHAR|支持 *|  
  
 \*二进制数据转换为十六进制字符串时发生。  
  
## <a name="sqlvariant-support-for-udts"></a>对 UDT 的 SQL_VARIANT 支持  
 在 SQL_VARIANT 列中不支持 UDT。  
  
## <a name="bcp-support-for-udts"></a>对 UDT 的 BCP 支持  
 UDT 值只能作为字符值或二进制值导入和导出。  
  
## <a name="downlevel-client-behavior-for-udts"></a>UDT 的下级客户端行为  
 对于下级客户端，UDT 会进行类型映射，如下所示：  
  
|服务器版本|SQL_SS_UDT<br /><br /> （长度小于或等于 8,000 个字节）|SQL_SS_UDT<br /><br /> （长度大于 8000 个字节）|  
|--------------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|SQL Server 2005|**UDT**|**varbinary(max)**|  
|SQL Server 2008 和更高版本|**UDT**|**UDT**|  
  
## <a name="odbc-functions-supporting-large-clr-udts"></a>支持大型 CLR UDT 的 ODBC 函数  
 本节讨论为支持大型 CLR UDT 而对 SQL Server Native Client ODBC 函数进行的更改。  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 按本主题前面的章节“绑定和转换”中所述，将 UDT 结果列值从 SQL 数据类型转换为 C 数据类型。  
  
### <a name="sqlbindparameter"></a>SQLBindParameter  
 UDT 所需的值如下所示：  
  
|SQL 数据类型|*Parametertype*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-------------------|---------------------|---------------------|------------------------|  
|SQL_SS_UDT<br /><br /> （长度小于或等于 8,000 个字节）|SQL_SS_UDT|*n*|0|  
|SQL_SS_UDT<br /><br /> （长度大于 8000 个字节）|SQL_SS_UDT|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 为 UDT 返回的值如本主题前面的章节“结果的描述符字段”中所述。  
  
### <a name="sqlcolumns"></a>SQLColumns  
 Udt 返回的值是在"列按 SQLColumns 和 SQLProcedureColumns （目录元数据） 返回元数据"部分中，本主题中前面所述。  
  
### <a name="sqldescribecol"></a>SQLDescribeCol  
 为 UDT 返回的值如下所示：  
  
|SQL 数据类型|*DataTypePtr*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-------------------|-------------------|---------------------|------------------------|  
|SQL_SS_UDT<br /><br /> （长度小于或等于 8,000 个字节）|SQL_SS_UDT|*n*|0|  
|SQL_SS_UDT<br /><br /> （长度大于 8000 个字节）|SQL_SS_UDT|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqldescribeparam"></a>SQLDescribeParam  
 为 UDT 返回的值如下所示：  
  
|SQL 数据类型|*DataTypePtr*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-------------------|-------------------|---------------------|------------------------|  
|SQL_SS_UDT<br /><br /> （长度小于或等于 8,000 个字节）|SQL_SS_UDT|*n*|0|  
|SQL_SS_UDT<br /><br /> （长度大于 8000 个字节）|SQL_SS_UDT|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlfetch"></a>SQLFetch  
 按本主题前面的章节“绑定和转换”中所述，将 UDT 结果列值从 SQL 数据类型转换为 C 数据类型。  
  
### <a name="sqlfetchscroll"></a>SQLFetchScroll  
 按本主题前面的章节“绑定和转换”中所述，将 UDT 结果列值从 SQL 数据类型转换为 C 数据类型。  
  
### <a name="sqlgetdata"></a>SQLGetData  
 按本主题前面的章节“绑定和转换”中所述，将 UDT 结果列值从 SQL 数据类型转换为 C 数据类型。  
  
### <a name="sqlgetdescfield"></a>SQLGetDescField  
 新类型可用的描述符字段如本主题前面的章节“参数的描述符字段”和“结果的描述符字段”中所述。  
  
### <a name="sqlgetdescrec"></a>SQLGetDescRec  
 为 UDT 返回的值如下所示：  
  
|SQL 数据类型|类型|子类型|长度|精度|小数位数|  
|-------------------|----------|-------------|------------|---------------|-----------|  
|SQL_SS_UDT<br /><br /> （长度小于或等于 8,000 个字节）|SQL_SS_UDT|0|*n*|n|0|  
|SQL_SS_UDT<br /><br /> （长度大于 8000 个字节）|SQL_SS_UDT|0|SQL_SS_LENGTH_UNLIMITED (0)|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlgettypeinfo"></a>SQLGetTypeInfo  
 为 UDT 返回的值如本主题前面的章节“SQLColumns 和 SQLProcedureColumns 返回的列元数据（目录元数据）”中所述。  
  
### <a name="sqlprocedurecolumns"></a>SQLProcedureColumns  
 为 UDT 返回的值如本主题前面的章节“SQLColumns 和 SQLProcedureColumns 返回的列元数据（目录元数据）”中所述。  
  
### <a name="sqlputdata"></a>SQLPutData  
 按本主题前面的章节“绑定和转换”中所述，将 UDT 参数值从 C 数据类型转换为 SQL 数据类型。  
  
### <a name="sqlsetdescfield"></a>SQLSetDescField  
 中的"第字段的 Parameters 描述符"和"的字段的结果描述符"部分中，本主题前面的描述了适用于新类型描述符字段。  
  
### <a name="sqlsetdescrec"></a>SQLSetDescRec  
 UDT 允许的值如下所示：  
  
|SQL 数据类型|类型|子类型|长度|精度|小数位数|  
|-------------------|----------|-------------|------------|---------------|-----------|  
|SQL_SS_UDT<br /><br /> （长度小于或等于 8,000 个字节）|SQL_SS_UDT|0|*n*|*n*|0|  
|SQL_SS_UDT<br /><br /> （长度大于 8000 个字节）|SQL_SS_UDT|0|SQL_SS_LENGTH_UNLIMITED (0)|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlspecialcolumns"></a>SQLSpecialColumns  
 为列 DATA_TYPE、TYPE_NAME、COLUMN_SIZE、BUFFER_LENGTH 和 DECIMAL_DIGTS UDT 返回的值如本主题前面的章节“SQLColumns 和 SQLProcedureColumns 返回的列元数据（目录元数据）”中所述。  
  
## <a name="see-also"></a>另请参阅  
 [大型 CLR 用户定义类型](../../../relational-databases/native-client/features/large-clr-user-defined-types.md)  
  
  
