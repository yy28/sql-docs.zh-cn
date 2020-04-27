---
title: sql_variant 对日期和时间类型的支持 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sql_variant data type
ms.assetid: 12ff1ea6-e2cc-40e6-910c-3126974a90b3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0cbde879e2b7f215c5044936dfbdacab9196f02d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63215960"
---
# <a name="sql_variant-support-for-date-and-time-types"></a>sql_variant 对日期和时间类型的支持
  本主题描述 `sql_variant` 数据类型如何支持增强的日期和时间功能。  
  
 列属性 SQL_CA_SS_VARIANT_TYPE 用于返回变体结果列的 C 类型。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 引入了新增的属性 SQL_CA_SS_VARIANT_SQL_TYPE，该属性在实现行描述符 (IRD) 中设置变体结果列的 SQL 类型。 还可以在实现参数描述符 (IPD) 中使用 SQL_CA_SS_VARIANT_SQL_TYPE，以指定将 SQL_C_BINARY C 类型与 SQL_SS_VARIANT 类型绑定的 SQL_SS_TIME2 或 SQL_SS_TIMESTAMPOFFSET 参数的 SQL 类型。  
  
 可以通过 SQLColAttribute 设置 SQL_SS_TIME2 和 SQL_SS_TIMESTAMPOFFSET 的新类型。 SQL_CA_SS_VARIANT_SQL_TYPE 可以通过 SQLGetDescField 返回。  
  
 对于结果列，驱动程序将从变体转换到日期/时间类型。 有关详细信息，请参阅[从 SQL 转换为 C](datetime-data-type-conversions-from-sql-to-c.md)。绑定到 SQL_C_BINARY 时，缓冲区长度必须足够大，以便接收对应于 SQL 类型的结构。  
  
 对于 SQL_SS_TIME2 和 SQL_SS_TIMESTAMPOFFSET 参数，驱动程序会将 C 值转换为 `sql_variant` 值，下表对此进行了描述。 如果参数被绑定为 SQL_C_BINARY 并且服务器类型是 SQL_SS_VARIANT，那么，除非应用程序已将 SQL_CA_SS_VARIANT_SQL_TYPE 设置为其他某个 SQL 类型，否则该参数将被视为二进制值。 这种情况下，SQL_CA_SS_VARIANT_SQL_TYPE 优先；就是说，如果设置 SQL_CA_SS_VARIANT_SQL_TYPE，它将覆盖从 C 类型推导出变体 SQL 类型的默认行为。  
  
|C 类型|服务器类型|说明|  
|------------|-----------------|--------------|  
|SQL_C_CHAR|varchar|忽略 SQL_CA_SS_VARIANT_SQL_TYPE。|  
|SQL_C_WCHAR|nvarcar|忽略 SQL_CA_SS_VARIANT_SQL_TYPE。|  
|SQL_C_TINYINT|smallint|忽略 SQL_CA_SS_VARIANT_SQL_TYPE。|  
|SQL_C_STINYINT|smallint|忽略 SQL_CA_SS_VARIANT_SQL_TYPE。|  
|SQL_C_SHORT|smallint|忽略 SQL_CA_SS_VARIANT_SQL_TYPE。|  
|SQL_C_SSHORT|smallint|忽略 SQL_CA_SS_VARIANT_SQL_TYPE。|  
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
|SQL_C_BINARY|time|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIME2<br /><br /> Scale 设置为 SQL_DESC_PRECISION （的`SQLBindParameter` *DecimalDigits*参数）。|  
|SQL_C_BINARY|datetimeoffset|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIMESTAMPOFFSET<br /><br /> Scale 设置为 SQL_DESC_PRECISION （的`SQLBindParameter` *DecimalDigits*参数）。|  
|SQL_C_TYPE_DATE|date|忽略 SQL_CA_SS_VARIANT_SQL_TYPE。|  
|SQL_C_TYPE_TIME|time(0)|忽略 SQL_CA_SS_VARIANT_SQL_TYPE。|  
|SQL_C_TYPE_TIMESTAMP|datetime2|Scale 设置为 SQL_DESC_PRECISION （的`SQLBindParameter` *DecimalDigits*参数）。|  
|SQL_C_NUMERIC|decimal|精度设置为 SQL_DESC_PRECISION （的`SQLBindParameter` *ColumnSize*参数）。<br /><br /> 规模集设置为 SQL_DESC_SCALE （SQLBindParameter 的*DecimalDigits*参数）。|  
|SQL_C_SS_TIME2|time|忽略 SQL_CA_SS_VARIANT_SQL_TYPE|  
|SQL_C_SS_TIMESTAMPOFFSET|datetimeoffset|忽略 SQL_CA_SS_VARIANT_SQL_TYPE|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC&#41;&#40;的日期和时间改进](date-and-time-improvements-odbc.md)  
  
  
