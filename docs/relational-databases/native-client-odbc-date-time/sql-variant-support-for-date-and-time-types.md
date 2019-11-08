---
title: sql_variant 对日期和时间类型的支持 |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sql_variant data type
ms.assetid: 12ff1ea6-e2cc-40e6-910c-3126974a90b3
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f795f1848f3e4c9fe1239df79677c35c38ba3b58
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2019
ms.locfileid: "73783512"
---
# <a name="sql_variant-support-for-date-and-time-types"></a>sql_variant 对日期和时间类型的支持
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本主题介绍**sql_variant**数据类型如何支持增强的日期和时间功能。  
  
 列属性 SQL_CA_SS_VARIANT_TYPE 用于返回变体结果列的 C 类型。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 引入了一个附加属性，SQL_CA_SS_VARIANT_SQL_TYPE，该属性在实现行描述符（IRD）中设置变体结果列的 SQL 类型。 SQL_CA_SS_VARIANT_SQL_TYPE 还可以在实现参数描述符（IPD）中使用，以指定 SQL_SS_TIME2 或 SQL_SS_TIMESTAMPOFFSET 参数的 SQL 类型，该类型具有与类型 SQL_SS_VARIANT 绑定的 SQL_C_BINARY C 类型。  
  
 可以通过 SQLColAttribute 设置 SQL_SS_TIME2 和 SQL_SS_TIMESTAMPOFFSET 的新类型。 SQL_CA_SS_VARIANT_SQL_TYPE 可以通过 SQLGetDescField 返回。  
  
 对于结果列，驱动程序将从变体转换到日期/时间类型。 有关详细信息，请参阅[从 SQL 转换为 C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)。绑定到 SQL_C_BINARY 时，缓冲区长度必须足够大，以便接收对应于 SQL 类型的结构。  
  
 对于 SQL_SS_TIME2 和 SQL_SS_TIMESTAMPOFFSET 参数，驱动程序会将 C 值转换为**sql_variant**值，如下表中所述。 如果参数被绑定为 SQL_C_BINARY 并且服务器类型是 SQL_SS_VARIANT，那么，除非应用程序已将 SQL_CA_SS_VARIANT_SQL_TYPE 设置为其他某个 SQL 类型，否则该参数将被视为二进制值。 这种情况下，SQL_CA_SS_VARIANT_SQL_TYPE 优先；就是说，如果设置 SQL_CA_SS_VARIANT_SQL_TYPE，它将覆盖从 C 类型推导出变体 SQL 类型的默认行为。  
  
|C 类型|服务器类型|注释|  
|------------|-----------------|--------------|  
|SQL_C_CHAR|varchar|忽略 SQL_CA_SS_VARIANT_SQL_TYPE。|  
|SQL_C_WCHAR|nvarcar|忽略 SQL_CA_SS_VARIANT_SQL_TYPE。|  
|SQL_C_TINYINT|int|忽略 SQL_CA_SS_VARIANT_SQL_TYPE。|  
|SQL_C_STINYINT|int|忽略 SQL_CA_SS_VARIANT_SQL_TYPE。|  
|SQL_C_SHORT|int|忽略 SQL_CA_SS_VARIANT_SQL_TYPE。|  
|SQL_C_SSHORT|int|忽略 SQL_CA_SS_VARIANT_SQL_TYPE。|  
|SQL_C_USHORT|int|忽略 SQL_CA_SS_VARIANT_SQL_TYPE。|  
|SQL_C_LONG|int|忽略 SQL_CA_SS_VARIANT_SQL_TYPE。|  
|SQL_C_SLONG|int|忽略 SQL_CA_SS_VARIANT_SQL_TYPE。|  
|SQL_C_ULONG|bigint|忽略 SQL_CA_SS_VARIANT_SQL_TYPE。|  
|SQL_C_SBIGINT|bigint|忽略 SQL_CA_SS_VARIANT_SQL_TYPE。|  
|SQL_C_FLOAT|real|忽略 SQL_CA_SS_VARIANT_SQL_TYPE。|  
|SQL_C_DOUBLE|float|忽略 SQL_CA_SS_VARIANT_SQL_TYPE。|  
|SQL_C_BIT|bit|忽略 SQL_CA_SS_VARIANT_SQL_TYPE。|  
|SQL_C_UTINYINT|tinyint|忽略 SQL_CA_SS_VARIANT_SQL_TYPE。|  
|SQL_C_BINARY|varbinary|SQL_CA_SS_VARIANT_SQL_TYPE 未设置。|  
|SQL_C_BINARY|time|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIME2<br /><br /> Scale 设置为 SQL_DESC_PRECISION （ **SQLBindParameter**的*DecimalDigits*参数）。|  
|SQL_C_BINARY|datetimeoffset|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIMESTAMPOFFSET<br /><br /> Scale 设置为 SQL_DESC_PRECISION （ **SQLBindParameter**的*DecimalDigits*参数）。|  
|SQL_C_TYPE_DATE|date|忽略 SQL_CA_SS_VARIANT_SQL_TYPE。|  
|SQL_C_TYPE_TIME|time(0)|忽略 SQL_CA_SS_VARIANT_SQL_TYPE。|  
|SQL_C_TYPE_TIMESTAMP|datetime2|Scale 设置为 SQL_DESC_PRECISION （ **SQLBindParameter**的*DecimalDigits*参数）。|  
|SQL_C_NUMERIC|DECIMAL|精度设置为 SQL_DESC_PRECISION （ **SQLBindParameter**的*ColumnSize*参数）。<br /><br /> 规模集设置为 SQL_DESC_SCALE （SQLBindParameter 的*DecimalDigits*参数）。|  
|SQL_C_SS_TIME2|time|忽略 SQL_CA_SS_VARIANT_SQL_TYPE|  
|SQL_C_SS_TIMESTAMPOFFSET|datetimeoffset|忽略 SQL_CA_SS_VARIANT_SQL_TYPE|  
  
## <a name="see-also"></a>另请参阅  
 [日期和时间改进&#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
