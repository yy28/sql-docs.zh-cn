---
title: 新的日期和时间功能与 SQL Server 早期版本 (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 96976bac-018c-47cc-b1b2-fa9605eb55e5
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6757868bf492a08caec1b8062776d6634331f868
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47666725"
---
# <a name="new-date-and-time-features-with-previous-sql-server-versions-ole-db"></a>SQL Server 早期版本的新日期和时间功能 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  本主题介绍预期的行为时使用增强的日期和时间功能的客户端应用程序的版本与通信[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]早于[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]，并在客户端使用的版本进行编译时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端早于[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]发送到服务器的命令支持增强的日期和时间功能。  
  
## <a name="down-level-client-behavior"></a>下级客户端行为  
 客户端应用程序使用的版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端早于[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]请参阅新的日期/时间类型作为**nvarchar**列。 这些列内容是文字表示。 有关详细信息，请参阅的"数据格式： 字符串和文字"部分[OLE DB 日期和时间改进的数据类型支持](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)。 列大小是为列指定的精度的最大文字长度。  
  
 目录 Api 将返回与返回给客户端的下级数据类型代码保持一致的元数据 (例如， **nvarchar**) 和关联的下级表示形式 （例如，相应的文字格式）。 不过，返回的数据类型名称将为 real [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 类型名称。  
  
 下级客户端应用程序针对的运行时[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]（或更高版本） 服务器已进行日期/时间的架构更改类型，预期的行为是按如下所示：  
  
|OLE DB 客户端类型|SQL Server 2005 类型|SQL Server 2008 （或更高版本） 类型|结果转换（服务器到客户端）|参数转换（客户端到服务器）|  
|------------------------|--------------------------|---------------------------------------|--------------------------------------------|-----------------------------------------------|  
|DBTYPE_DBDATE|DATETIME|date|“确定”|“确定”|  
|DBTYPE_DBTIMESTAMP|||时间字段设置为零。|如果时间字段非零值，则由于字符串截断将失败 IRowsetChange。|  
|DBTYPE_DBTIME||Time(0)|“确定”|“确定”|  
|DBTYPE_DBTIMESTAMP|||日期字段设置为当前日期。|如果秒的小数部分为非零值，则由于字符串截断将失败 IRowsetChange。<br /><br /> 忽略日期。|  
|DBTYPE_DBTIME||Time(7)|失败 – 无效的时间文字。|“确定”|  
|DBTYPE_DBTIMESTAMP|||失败 – 无效的时间文字。|“确定”|  
|DBTYPE_DBTIMESTAMP||Datetime2(3)|“确定”|“确定”|  
|DBTYPE_DBTIMESTAMP||datetime2(7)|“确定”|“确定”|  
|DBTYPE_DBDATE|Smalldatetime|date|“确定”|“确定”|  
|DBTYPE_DBTIMESTAMP|||时间字段设置为零。|如果时间字段非零值，则由于字符串截断将失败 IRowsetChange。|  
|DBTYPE_DBTIME||Time(0)|“确定”|“确定”|  
|DBTYPE_DBTIMESTAMP|||日期字段设置为当前日期。|如果秒的小数部分为非零值，则由于字符串截断将失败 IRowsetChange。<br /><br /> 忽略日期。|  
|DBTYPE_DBTIMESTAMP||Datetime2(0)|“确定”|“确定”|  
  
 “可以”表示如果已适用于 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，应继续适用于 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]（或更高版本）。  
  
 只考虑了以下常见的架构更改：  
  
-   使用新类型，这种情况下在逻辑上应用程序只需要一个日期或时间值。 但是，强制应用程序以使用**datetime**或**smalldatetime**因为均不提供单独的日期和时间类型。  
  
-   使用新类型以获得其他秒小数精度或准确性。  
  
-   切换到**datetime2**由于这是首选的数据类型的日期和时间。  
  
 使用通过 icommandwithparameters:: Getparameterinfo 或架构行集获取的服务器元数据来设置通过 icommandwithparameters:: Setparameterinfo 参数类型信息的应用程序将在客户端转换期间失败的字符串源类型的表示形式大于目标类型的字符串表示形式。 例如，如果客户端绑定使用 DBTYPE_DBTIMESTAMP，且服务器列为日期[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 将值转换为"yyyy dd mm hh:mm:ss.fff"，但服务器元数据将作为返回**nvarchar(10)**。 生成的溢出会导致 DBSTATUS_E_CATCONVERTVALUE。 因为从结果集元数据设置行集元数据时，由 IRowsetChange 中的数据转换出现类似问题。  
  
### <a name="parameter-and-rowset-metadata"></a>参数和行集元数据  
 本部分介绍对使用的版本编译的客户端的参数、 结果列和架构行集元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端早于[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]。  
  
#### <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 DBPARAMINFO 结构返回以下信息通过*prgParamInfo*参数：  
  
|参数类型|wType|ulParamSize|bPrecision|bScale|  
|--------------------|-----------|-----------------|----------------|------------|  
|日期|DBTYPE_WSTR|10|~0|~0|  
|time|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|~0|~0|  
  
 请注意，某些值范围不是连续的，例如，8,10..16 中缺少 9。 这是因为当小数精度大于零时添加了小数点。  
  
#### <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 会返回以下列：  
  
|列类型|DBCOLUMN_TYPE|DBCOLUMN_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE、DBCOLUMN_DATETIMEPRECISION|  
|-----------------|--------------------|--------------------------|-------------------------|--------------------------------------------------|  
|日期|DBTYPE_WSTR|10|NULL|NULL|  
|time|DBTYPE_WSTR|8, 10..16|NULL|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|NULL|NULL|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|NULL|NULL|  
  
#### <a name="columnsinfogetcolumninfo"></a>ColumnsInfo::GetColumnInfo  
 DBCOLUMNINFO 结构返回以下信息：  
  
|参数类型|wType|ulColumnSize|bPrecision|bScale|  
|--------------------|-----------|------------------|----------------|------------|  
|日期|DBTYPE_WSTR|10|~0|~0|  
|time(1..7)|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|~0|~0|  
  
### <a name="schema-rowsets"></a>架构行集  
 本部分论述了新数据类型的参数、结果列以及架构行集的元数据。 此信息很有用是具有客户端提供程序使用工具开发早于[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端。  
  
#### <a name="columns-rowset"></a>COLUMNS 行集  
 对于日期/时间类型将返回以下列值：  
  
|列类型|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|DATETIME_PRECISION|  
|-----------------|----------------|--------------------------------|------------------------------|-------------------------|  
|日期|DBTYPE_WSTR|10|20|NULL|  
|time|DBTYPE_WSTR|8, 10..16|16,20..32|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|0|  
|DATETIME|DBTYPE_DBTIMESTAMP|NULL|NULL|3|  
|datetime2|DBTYPE_WSTR|19,21..27|38,42..54|NULL|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|52, 56..68|NULL|  
  
#### <a name="procedureparameters-rowset"></a>PROCEDURE_PARAMETERS 行集  
 对于日期/时间类型将返回以下列值：  
  
|列类型|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|TYPE_NAME<br /><br /> LOCAL_TYPE_NAME|  
|-----------------|----------------|--------------------------------|------------------------------|--------------------------------------|  
|日期|DBTYPE_WSTR|10|20|日期|  
|time|DBTYPE_WSTR|8, 10..16|16,20..32|time|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|smalldatetime|  
|DATETIME|DBTYPE_DBTIMESTAMP|NULL|NULL|DATETIME|  
|datetime2|DBTYPE_WSTR|19,21..27|38,42..54|datetime2|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|52, 56..68|datetimeoffset|  
  
#### <a name="providertypes-rowset"></a>PROVIDER_TYPES 行集  
 对于日期/时间类型将返回以下行：  
  
|类型 -><br /><br /> “列”|日期|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|日期|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|DATA_TYPE|DBTYPE_WSTR|DBTYPE_WSTR|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_WSTR|DBTYPE_WSTR|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|‘|‘|‘|‘|‘|‘|  
|LITERAL_SUFFIX|‘|‘|‘|‘|‘|‘|  
|CREATE_PARAMS|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_NULLABLE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
|CASE_SENSITIVE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FIXED_PREC_SCALE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|AUTO_UNIQUE_VALUE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|LOCAL_TYPE_NAME|日期|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|NULL|NULL|NULL|NULL|NULL|  
|MAXIMUM_SCALE|NULL|NULL|NULL|NULL|NULL|NULL|  
|GUID|NULL|NULL|NULL|NULL|NULL|NULL|  
|TYPELIB|NULL|NULL|NULL|NULL|NULL|NULL|  
|VERSION|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_LONG|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|BEST_MATCH|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_TRUE|VARIANT_FALSE|VARIANT_FALSE|  
|IS_FIXEDLENGTH|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
  
## <a name="down-level-server-behavior"></a>下级服务器行为  
 在连接到服务器的版本早于[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]，任何尝试使用新的服务器类型名称 （例如，使用 icommandwithparameters:: Setparameterinfo 或 itabledefinition:: Createtable） 将导致 DB_E_BADTYPENAME。  
  
 如果在不使用类型名称的情况下针对参数或结果绑定新类型，且新类型用于隐式指定服务器类型，或服务器类型到客户端类型之间没有有效的转换，则将返回 DB_E_ERRORSOCCURRED，且 DBBINDSTATUS_UNSUPPORTED_CONVERSION 设置为在执行时使用的取值函数的绑定状态。  
  
 如果在连接时支持从缓冲区类型到服务器版本的服务器类型之间的客户端转换，则可以使用所有客户端缓冲区类型。 在此上下文中，*服务器类型*意味着指定 icommandwithparameters:: Setparameterinfo，或如果尚未调用 icommandwithparameters:: Setparameterinfo 权限隐含的缓冲区类型的类型。 这意味着 DBTYPE_DBTIME2 和 DBTYPE_DBTIMESTAMPOFFSET 可用于下级服务器，或在 DataTypeCompatibility=80 时，对支持的服务器类型的客户端转换成功的情况下，也可使用。 当然，如果服务器类型不正确，且该服务器类型不能执行对实际服务器类型的隐式转换，则服务器仍可能报告错误。  
  
## <a name="sspropinitdatatypecompatibility-behavior"></a>SSPROP_INIT_DATATYPECOMPATIBILITY 行为  
 如果 SSPROP_INIT_DATATYPECOMPATIBILITY 设置为 SSPROPVAL_DATATYPECOMPATIBILITY_SQL2000，新的日期/时间类型和关联的元数据显示到客户端与它们对下级客户端，如中所述[的大容量复制更改增强的日期和时间类型&#40;OLE DB 和 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。  
  
## <a name="comparability-for-irowsetfind"></a>IRowsetFind 的可比性  
 允许对新的日期/时间类型使用所有比较运算符，因为这些比较运算符显示为字符串类型，而不是显示为日期/时间类型。  
  
## <a name="see-also"></a>请参阅  
 [日期和时间改进 (OLE DB)](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
