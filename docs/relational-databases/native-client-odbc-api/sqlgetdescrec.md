---
title: SQLGetDescRec |微软文档
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLGetDescRec function
ms.assetid: f3389ff2-f3be-4035-9fb5-c9ebc2f15025
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 42c8a45bb50e5fda8946cc3819aa4702f5c2fb3f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299557"
---
# <a name="sqlgetdescrec"></a>SQLGetDescRec
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本主题讨论特定于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端的 SQLGetDescRec 功能。  
  
## <a name="sqlgetdescrec-and-table-valued-parameters"></a>SQLGetDescRec 和表值参数  
 SQLGetDescRec 可用于获取表值参数和表值参数列的属性的值。 SQLGetDescRec 的*RecNumber*参数对应于 SQLBind 参数的*参数编号*参数。  
  
 表值参数列仅在将描述符标头字段 SQL_SOPT_SS_PARAM_FOCUS 设置为特定记录（其 SQL_DESC_TYPE 设置为 SQL_SS_TABLE）的序数时可用。 有关有关SQL_SOPT_SS_PARAM_FOCUS的详细信息，请参阅[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
 SQLGetDescRec 返回以下数据：  
  
|参数|表值参数|表值参数列和其他参数|  
|---------------|-----------------------------|----------------------------------------------------------|  
|*名称*|存储过程调用的正式参数名称；否则是长度为 0 的字符串。|表值参数列名称。|  
|*类型 Ptr*|SQL_DESC_TYPE。 对于表值参数，这是 SQL_SS_TABLE。|SQL_DESC_TYPE|  
|*子类型 Ptr*|Undefined|SQL_DESC_DATETIME_INTERVAL_CODE（对于 SQL_DATETIME 或 SQL_INTERVAL 类型的记录。）|  
|*长度Ptr*|0|SQL_DESC_OCTET_LENGTH|  
|*精密Ptr*|0|SQL_DESC_PRECISION|  
|*缩放器*|0|SQL_DESC_SCALE|  
|*空可点*|1|SQL_DESC_NULLABLE|  
  
 有关表值参数的详细信息，请参阅[&#40;ODBC&#41;的表值参数](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlgetdescrec-support-for-enhanced-date-and-time-features"></a>SQLGetDescRec 对日期和时间增强功能的支持  
 日期/时间类型返回以下值：  
  
||*类型 Ptr*|*子类型 Ptr*|*长度Ptr*|*精密Ptr*|*缩放器*|  
|-|---------------|------------------|-----------------|--------------------|----------------|  
|datetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|4|3|3|  
|smalldatetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|8|0|0|  
|date|SQL_DATETIME|SQL_CODE_DATE|6|0|0|  
|time|SQL_SS_TIME2|0|10|0..7|0..7|  
|datetime2|SQL_DATETIME|SQL_CODE_TIMESTAMP|16|0..7|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|0|20|0..7|0..7|  
  
 有关详细信息，请参阅[&#40;ODBC&#41;的日期和时间改进](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlgetdescrec-support-for-large-clr-udts"></a>SQLGetDescRec 对大型 CLR UDT 的支持  
 **SQLGetDescRec**支持大型 CLR 用户定义类型 （UDT）。 有关详细信息，请参阅[&#40;ODBC&#41;的大型 CLR 用户定义类型](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLGetDescRec](https://go.microsoft.com/fwlink/?LinkId=80707)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
