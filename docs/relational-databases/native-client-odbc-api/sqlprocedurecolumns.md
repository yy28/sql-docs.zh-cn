---
title: SQLProcedureColumns |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLProcedureColumns function
ms.assetid: 6671e180-0072-4de5-90f5-314306d2ba9c
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 683df9d5116417ebf31eca7925db908dea9a3070
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47831545"
---
# <a name="sqlprocedurecolumns"></a>SQLProcedureColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLProcedureColumns**返回一个行报告返回值属性的所有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]存储过程。  
  
 **SQLProcedureColumns**是否存在值都返回 SQL_SUCCESS *CatalogName*， *SchemaName*， *ProcName*，或*ColumnName*参数。 **SQLFetch**这些参数中使用的值无效时返回 SQL_NO_DATA。  
  
 **SQLProcedureColumns**可以对静态服务器游标执行。 尝试执行**SQLProcedureColumns**对可更新的 （动态或键集） 游标将返回 sql_success_with_info 以指示游标类型已更改。  
  
 下表列出了结果集和如何它们进行扩展以处理返回的列**udt**并**xml**数据类型通过[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序：  
  
|列名|Description|  
|-----------------|-----------------|  
|SS_UDT_CATALOG_NAME|返回包含 UDT（用户定义类型）的目录的名称。|  
|SS_UDT_SCHEMA_NAME|返回包含 UDT 的架构的名称。|  
|SS_UDT_ASSEMBLY_TYPE_NAME|返回 UDT 的程序集限定名称。|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|返回在其中定义 XML 架构集合名称的目录的名称。 如果找不到目录名称，则此变量包含空字符串。|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|返回在其中定义 XML 架构集合名称的架构的名称。 如果找不到架构名称，则此变量包含空字符串。|  
|SS_XML_SCHEMACOLLECTION_NAME|返回 XML 架构集合的名称。 如果找不到此名称，则此变量包含空字符串。|  
  
## <a name="sqlprocedurecolumns-and-table-valued-parameters"></a>SQLProcedureColumns 和表值参数  
 SQLProcedureColumns 处理方式类似于 CLR 用户定义类型中的表值参数。 在针对表值参数返回的行中，列具有以下值：  
  
|列名|说明/值|  
|-----------------|------------------------|  
|DATA_TYPE|SQL_SS_TABLE|  
|TYPE_NAME|表值参数的表类型的名称。|  
|COLUMN_SIZE|NULL|  
|BUFFER_LENGTH|0|  
|DECIMAL_DIGITS|表值参数中的列数。|  
|NUM_PREC_RADIX|NULL|  
|NULLABLE|SQL_NULLABLE|  
|REMARKS|NULL|  
|COLUMN_DEF|NULL。 表类型可能没有默认值。|  
|SQL_DATA_TYPE|SQL_SS_TABLE|  
|SQL_DATEIME_SUB|NULL|  
|CHAR_OCTET_LENGTH|NULL|  
|IS_NULLABLE|"YES"|  
|SS_TYPE_CATALOG_NAME|返回包含表或 CLR 用户定义类型的目录的名称。|  
|SS_TYPE_SCHEMA_NAME|返回包含表或 CLR 用户定义类型的架构的名称。|  
  
 SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMA_NAME 列在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更高版本中提供，分别用于返回表值参数的目录和架构。 这些列是为表值参数和 CLR 用户定义类型参数填充的。 （CLR 用户定义类型参数的现有架构和目录列不受此附加功能影响。 为保持向后兼容，也会对它们进行填充）。  
  
 为了符合 ODBC 规范，SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMA_NAME 的显示位置位于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 早期版本中添加的所有驱动程序特定列之前，ODBC 自身托管的所有列之后。  
  
 有关表值参数的详细信息，请参阅[表值参数&#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlprocedurecolumns-support-for-enhanced-date-and-time-features"></a>SQLProcedureColumns 对日期和时间增强功能的支持  
 有关为日期/时间类型返回的值，请参阅[目录元数据](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md)。  
  
 有关更多常规信息，请参阅[日期和时间改进&#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlprocedurecolumns-support-for-large-clr-udts"></a>SQLProcedureColumns 对大型 CLR UDT 的支持  
 **SQLProcedureColumns**支持大型 CLR 用户定义类型 (Udt)。 有关详细信息，请参阅[Large CLR User-Defined 类型&#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQLProcedureColumns 函数](http://go.microsoft.com/fwlink/?LinkId=59363)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
