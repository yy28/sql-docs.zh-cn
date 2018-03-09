---
title: "增强的日期和时间类型与以前的 SQL Server 版本 (ODBC) 的行为 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-date-time
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- date/time [ODBC], enhanced behavior with earlier SQL Server versions
ms.assetid: cd4e137f-dc5e-4df7-bc95-51fe18c587e0
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f2acc8c52d6e16cf17c05cc421faf5ea52b20e71
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="enhanced-date-and-time-type-behavior-with-previous-sql-server-versions-odbc"></a>与 SQL Server 早期版本的增强日期和时间类型行为 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  本主题说明当使用增强的日期和时间功能的客户端应用程序与早于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 版本通信时的预期行为，以及使用 Microsoft 数据访问组件、Windows 数据访问组件或早于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Native Client 版本的客户端应用程序向支持增强的日期和时间功能的服务器发送命令时的预期行为。  
  
## <a name="down-level-client-behavior"></a>下级客户端行为  
 使用早于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Native Client 版本编译的客户端应用程序将新的日期/时间类型看作 nvarchar 列。 列内容将文本表示形式，"数据格式:: 字符串和文本"一节中所述[ODBC 日期和时间的改进的数据类型支持](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)。 列大小是为列指定的秒小数精度的最大文字长度。  
  
 目录 API 将返回与返回给客户端的下级数据类型代码（例如 nvarchar）和相关的下级表示法（例如相应的文字格式）一致的元数据。 不过，返回的数据类型名称将为 real [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 类型名称。  
  
 返回 SQLDescribeCol、 SQLDescribeParam、 SQGetDescField 和 SQLColAttribute 语句元数据将返回与在所有方面，包括类型名称的低级别类型一致的元数据。 这样一个低级别类型的一个示例是**nvarchar**。  
  
 对下层客户端应用程序的运行时[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]（或更高版本） 服务器的架构更改，以日期/时间类型进行了，预期的行为是，如下所示：  
  
|SQL Server 2005 类型|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]（或更高版本）类型|ODBC 客户端类型|结果转换（SQL 到 C）|参数转换（C 到 SQL）|  
|--------------------------|----------------------------------------------|----------------------|------------------------------------|---------------------------------------|  
|日期时间|日期|SQL_C_TYPE_DATE|确定|确定 (1)|  
|||SQL_C_TYPE_TIMESTAMP|时间字段设置为零。|成功 (2)<br /><br /> 如果时间字段非零，则失败。 适用于[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。|  
||Time(0)|SQL_C_TYPE_TIME|确定|确定 (1)|  
|||SQL_C_TYPE_TIMESTAMP|日期字段设置为当前日期。|成功 (2)<br /><br /> 忽略日期。 如果秒的小数部分都为非零，则将失败。 适用于[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。|  
||Time(7)|SQL_C_TIME|失败 – 无效的时间文字。|确定 (1)|  
|||SQL_C_TYPE_TIMESTAMP|失败 – 无效的时间文字。|确定 (1)|  
||Datetime2(3)|SQL_C_TYPE_TIMESTAMP|确定|确定 (1)|  
||Datetime2(7)|SQL_C_TYPE_TIMESTAMP|确定|由客户端转换将值舍入到 1/300 秒。|  
|Smalldatetime|日期|SQL_C_TYPE_DATE|确定|确定|  
|||SQL_C_TYPE_TIMESTAMP|时间字段设置为零。|成功 (2)<br /><br /> 如果时间字段非零，则失败。 适用于[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。|  
||Time(0)|SQL_C_TYPE_TIME|确定|确定|  
|||SQL_C_TYPE_TIMESTAMP|日期字段设置为当前日期。|成功 (2)<br /><br /> 忽略日期。 如果秒的小数部分非零，则失败。<br /><br /> 适用于[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。|  
||Datetime2(0)|SQL_C_TYPE_TIMESTAMP|确定|确定|  
  
## <a name="key-to-symbols"></a>符号含义  
  
|符号|含义|  
|------------|-------------|  
|1|如果已适用于 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，应继续适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的更新版本。|  
|2|已与 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 一起使用的应用程序在与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的更新版本一起使用时，可能失败。|  
  
 请注意只考虑了常见的架构更改。 以下是常见的更改：  
  
-   使用新类型，这种情况下在逻辑上应用程序只需要一个日期或时间值。 但是，由于缺乏单独的日期和时间类型，会强制应用程序使用 datetime 或 smalldatetime。  
  
-   使用新类型以获得其他秒小数精度或准确性。  
  
-   转换到 datetime2，因为这是首选的日期和时间数据类型。  
  
### <a name="column-metadata-returned-by-sqlcolumns-sqlprocedurecolumns-and-sqlspecialcolumns"></a>SQLColumns、SQLProcedureColumns 和 SQLSpecialColumns 返回的列元数据  
 对于日期/时间类型将返回以下列值：  
  
|列类型|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|-----------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|DATA_TYPE|SQL_WVARCHAR|SQL_WVARCHAR|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_WVARCHAR|SQL_WVARCHAR|  
|TYPE_NAME|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|COLUMN_SIZE|10|8,10..16|16|23|19, 21..27|26, 28..34|  
|BUFFER_LENGTH|20|16, 20..32|16|16|38, 42..54|52, 56..68|  
|DECIMAL_DIGITS|NULL|NULL|0|3|NULL|NULL|  
|SQL_DATA_TYPE|SQL_WVARCHAR|SQL_WVARCHAR|SQL_DATETIME|SQL_DATETIME|SQL_WVARCHAR|SQL_WVARCHAR|  
|SQL_DATETIME_SUB|NULL|NULL|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|NULL|NULL|  
|CHAR_OCTET_LENGTH|NULL|NULL|NULL|NULL|NULL|NULL|  
|SS_DATA_TYPE|0|0|111|111|0|0|  
  
 SQLSpecialColumns 不返回 SQL_DATA_TYPE、SQL_DATETIME_SUB、CHAR_OCTET_LENGTH 或 SS_DATA_TYPE。  
  
### <a name="data-type-metadata-returned-by-sqlgettypeinfo"></a>SQLGetTypeInfo 返回的数据类型元数据  
 对于日期/时间类型将返回以下列值：  
  
|列类型|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|-----------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|DATA_TYPE|SQL_WVARCHAR|SQL_WVARCHAR|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_WVARCHAR|SQL_WVARCHAR|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|‘|‘|‘|‘|‘|‘|  
|LITERAL_SUFFIX|‘|‘|‘|‘|‘|‘|  
|CREATE_PARAMS|NULL|NULL|NULL|NULL|NULL|NULL|  
|NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|  
|CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|AUTO_UNIQUE_VALUE|NULL|NULL|NULL|NULL|NULL|NULL|  
|LOCAL_TYPE_NAME|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|NULL|0|3|NULL|NULL|  
|MAXIMUM_SCALE|NULL|NULL|0|3|NULL|NULL|  
|SQL_DATA_TYPE|SQL_WVARCHAR|SQL_WVARCHAR|SQL_DATETIME|SQL_DATETIME|SQL_WVARCHAR|SQL_WVARCHAR|  
|SQL_DATETIME_SUB|NULL|NULL|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|NULL|NULL|  
|NUM_PREC_RADIX|NULL|NULL|NULL|NULL|NULL|NULL|  
|INTERVAL_PRECISION|NULL|NULL|NULL|NULL|NULL|NULL|  
|USERTYPE|0|0|12|22|0|0|  
  
## <a name="down-level-server-behavior"></a>下级服务器行为  
 连接到版本早于 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 的服务器实例时，只要试图使用新的服务器类型或相关的元数据代码和描述符字段，都将导致返回 SQL_ERROR。 将生成以下诊断记录：具有 SQLSTATE HY004 和消息“SQL 数据类型对于连接的服务器版本无效”，或具有 07006 和消息“受限制的数据类型属性冲突”。  
  
## <a name="see-also"></a>另请参阅  
 [日期和时间改进 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
