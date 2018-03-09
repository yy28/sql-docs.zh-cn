---
title: SQLColumns | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLColumns function
ms.assetid: 69d3af44-8196-43ab-8037-cdd06207b171
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 661c678e8d98d1b4d3f88c29d6d0b786b4e686d4
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="sqlcolumns"></a>SQLColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLColumns**是否值已存在，则返回 SQL_SUCCESS *CatalogName*， *TableName*，或*ColumnName*参数。 **SQLFetch**返回 SQL_NO_DATA，在这些参数中使用了无效值。  
  
> [!NOTE]  
>  对于大值类型，将返回值为 SQL_SS_LENGTH_UNLIMITED 的所有长度参数。  
  
 **SQLColumns**可以执行对静态服务器游标。 尝试执行**SQLColumns**上的可更新的 （动态或键集） 游标，则将返回 SQL_SUCCESS_WITH_INFO 指示游标类型已更改。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序支持为链接服务器上的表报表信息由接受的两部分名称*CatalogName*参数： *Linked_Server_Name.Catalog_Name*.  
  
 适用于 ODBC 2。*x*应用程序不使用中的通配符*TableName*， **SQLColumns**返回有关任何信息表的名称匹配*TableName*且由当前用户拥有。 如果当前用户拥有其名称与匹配任何表*TableName*参数， **SQLColumns**返回有关其他用户拥有的任何表的信息的表名称与匹配之处*TableName*参数。 适用于 ODBC 2。*x*应用程序使用通配符， **SQLColumns**返回所有表的名称匹配*TableName*。 适用于 ODBC 3。*x*应用程序**SQLColumns**返回所有表的名称匹配*TableName*而不考虑所有者或是否使用通配符。  
  
 下表列出了结果集返回的列：  
  
|列名|Description|  
|-----------------|-----------------|  
|DATA_TYPE|返回 SQL_VARCHAR、 SQL_VARBINARY 或为 SQL_WVARCHAR **varchar （max)**数据类型。|  
|TYPE_NAME|返回"varchar"、"varbinary"或"nvarchar" **varchar （max)**， **varbinary （max)**，和**nvarchar (max)**数据类型。|  
|COLUMN_SIZE|返回有关 SQL_SS_LENGTH_UNLIMITED **varchar （max)**数据类型，该值指示列的大小不受限制。|  
|BUFFER_LENGTH|返回有关 SQL_SS_LENGTH_UNLIMITED **varchar （max)**数据类型，该值指示缓冲区的大小不受限制。|  
|SQL_DATA_TYPE|返回 SQL_VARCHAR、 SQL_VARBINARY 或为 SQL_WVARCHAR **varchar （max)**数据类型。|  
|CHAR_OCTET_LENGTH|返回字符或二进制列的最大长度。 返回 0 表示大小不受限制。|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|返回在其中定义 XML 架构集合名称的目录的名称。 如果找不到目录名称，则此变量包含空字符串。|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|返回在其中定义 XML 架构集合名称的架构的名称。 如果找不到架构名称，则此变量包含空字符串。|  
|SS_XML_SCHEMACOLLECTION_NAME|返回 XML 架构集合的名称。 如果找不到此名称，则此变量包含空字符串。|  
|SS_UDT_CATALOG_NAME|包含 UDT（用户定义类型）的目录的名称。|  
|SS_UDT_SCHEMA_NAME|包含用户定义的类型的架构的名称。|  
|SS_UDT_ASSEMBLY_TYPE_NAME|UDT 的程序集限定名称。|  
  
 对于 Udt，现有的 TYPE_NAME 列用于指示 UDT; 的名称因此应将为其任何其他列添加到结果集的**SQLColumns**或[SQLProcedureColumns](../../relational-databases/native-client-odbc-api/sqlprocedurecolumns.md)。 UDT 列或参数的 DATA_TYPE 为 SQL_SS_UDT。  
  
 对于 UDT 参数，您可以使用上面定义的特定于驱动程序的新描述符来获取或设置 UDT 的额外元数据数据，条件是服务器返回或需要此信息。  
  
 当客户端连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和调用 SQLColumns、 对目录输入的参数不会从其他编录返回信息使用 NULL 或通配符值。 而只返回有关当前目录的信息。 首先，客户端可以调用 SQLTables 以确定所需的表所在的目录中。 客户端可以然后使用目录该值目录 SQLColumns 对其调用中的输入参数来检索有关此表中列的信息。  
  
## <a name="sqlcolumns-and-table-valued-parameters"></a>SQLColumns 和表值参数  
 SQLColumns 所返回的结果集取决于 SQL_SOPT_SS_NAME_SCOPE 的设置。 有关详细信息，请参阅[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。 已针对表值参数添加以下列：  
  
|列名|数据类型|目录|  
|-----------------|---------------|--------------|  
|SS_IS_COMPUTED|Smallint|对于 TABLE_TYPE 中的列，如果该列是一个计算列，则为 SQL_TRUE；否则为 SQL_FALSE。|  
|SS_IS_IDENTITY|Smallint|如果该列为标识列，则为 SQL_TRUE；否则为 SQL_FALSE。|  
  
 有关表值参数的详细信息，请参阅[表值参数 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlcolumns-support-for-enhanced-date-and-time-features"></a>SQLColumns 对日期和时间增强功能的支持  
 有关为日期/时间类型返回的值的信息，请参阅[目录元数据](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md)。  
  
 有关详细信息，请参阅[日期和时间改进 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlcolumns-support-for-large-clr-udts"></a>SQLColumns 对大型 CLR UDT 的支持  
 **SQLColumns**支持大型 CLR 用户定义类型 (Udt)。 有关详细信息，请参阅[Large CLR User-Defined 类型 &#40; ODBC &#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="sqlcolumns-support-for-sparse-columns"></a>SQLColumns 对稀疏列的支持  
 两个[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]特定列已添加到结果集中为 SQLColumns:  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|SS_IS_SPARSE|**Smallint**|如果该列为稀疏列，则为 SQL_TRUE；否则为 SQL_FALSE。|  
|SS_IS_COLUMN_SET|**Smallint**|如果该列为**column_set**列中，这是 SQL_TRUE; 否则为 SQL_FALSE。|  
  
 符合 ODBC 规范，SS_IS_SPARSE 和 SS_IS_COLUMN_SET 出现在之前已添加到的所有驱动程序的特定列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本早于[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]，和之后由 ODBC 本身规定的所有列。  
  
 SQLColumns 所返回的结果集取决于 SQL_SOPT_SS_NAME_SCOPE 的设置。 有关详细信息，请参阅[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
 有关 ODBC 中的稀疏列的详细信息，请参阅[稀疏列支持 &#40; ODBC &#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLColumns 函数](http://go.microsoft.com/fwlink/?LinkId=59336)   
 [ODBC API 实现详细信息](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
