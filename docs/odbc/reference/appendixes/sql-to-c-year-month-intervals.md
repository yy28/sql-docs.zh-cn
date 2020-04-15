---
title: SQL 到 C：年月间隔 |微软文档
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], about converting
- data conversions from SQL to C types [ODBC], year-month intervals
- intervals [ODBC], converting
- year-month intervals [ODBC]
ms.assetid: 1233634b-8214-420f-b872-3b2630105ba4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ba79a4d6165a43676634a6b79db56b88f5bcc234
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296387"
---
# <a name="sql-to-c-year-month-intervals"></a>从 SQL 到 C：年月间隔

年月间隔 ODBC SQL 数据类型的标识符如下：

- SQL_INTERVAL_MONTH
- SQL_INTERVAL_YEAR
- SQL_INTERVAL_YEAR_TO_MONTH

下表显示了可转换为年月间隔 SQL 数据的 ODBC C 数据类型。 有关表中列和术语的说明，请参阅[将数据从 SQL 转换为 C 数据类型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  

|C 类型标识符|测试|目标价值Ptr|StrLen_or_IndPtr|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_INTERVAL_MONTH[a]<br /><br /> SQL_C_INTERVAL_YEAR[a]<br /><br /> SQL_C_INTERVAL_YEAR_TO_MONTH[a]|尾随字段部分未截断<br /><br /> 尾随字段部分截断<br /><br /> 目标的领先精度不足以保存来自源的数据|数据<br /><br /> 截断的数据<br /><br /> Undefined|以字节为单位的数据长度<br /><br /> 以字节为单位的数据长度<br /><br /> Undefined|不适用<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT[b]<br /><br /> SQL_C_UTINYINT[b]<br /><br /> SQL_C_USHORT[b]<br /><br /> SQL_C_SHORT[b]<br /><br /> SQL_C_SLONG[b]<br /><br /> SQL_C_ULONG[b]<br /><br /> SQL_C_NUMERIC[b]<br /><br /> SQL_C_BIGINT[b]|间隔精度是单个字段，数据在不截断的情况下被转换<br /><br /> 间隔精度是单个字段，并截断整个<br /><br /> 间隔精度不是单个字段|数据<br /><br /> 截断的数据<br /><br /> Undefined|C 数据类型的大小<br /><br /> 以字节为单位的数据长度<br /><br /> C 数据类型的大小|不适用<br /><br /> 22003<br /><br /> 22015|  
|SQL_C_BINARY|数据<字节长度 =*缓冲区长度*<br /><br /> >*缓冲区长度*的数据字节长度|数据<br /><br /> Undefined|以字节为单位的数据长度<br /><br /> Undefined|不适用<br /><br /> 22003|  
|SQL_C_CHAR|字符字节长度<*缓冲区长度*<br /><br /> *缓冲区长度*<整数（与小数）位数<br /><br /> >=*缓冲区长度*的整个（与小数）数字数|数据<br /><br /> 截断的数据<br /><br /> Undefined|C 数据类型的大小<br /><br /> C 数据类型的大小<br /><br /> Undefined|不适用<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|字符长度<*缓冲区长度*<br /><br /> *缓冲区长度*<整数（与小数）位数<br /><br /> >=*缓冲区长度*的整个（与小数）数字数|数据<br /><br /> 截断的数据<br /><br /> Undefined|C 数据类型的大小<br /><br /> C 数据类型的大小<br /><br /> Undefined|不适用<br /><br /> 01004<br /><br /> 22003|  
  
 [a] 年月间隔 SQL 类型可以转换为任何年月间隔 C 类型。  
  
 [b] 如果间隔精度是单个字段（YEAR 或 MONTH 之一），则可以将间隔 SQL 类型转换为任何精确数值（SQL_C_STINYINT、SQL_C_UTINYINT、SQL_C_USHORT、SQL_C_SHORT、SQL_C_SLONG、SQL_C_ULONG或SQL_C_NUMERIC）。  

## <a name="default-conversions"></a>默认转换

间隔 SQL 类型的默认转换为相应的 C 间隔数据类型。 然后，应用程序绑定列或参数（或在 ARD 的适当记录中设置SQL_DESC_DATA_PTR字段），以指向初始化SQL_INTERVAL_STRUCT结构（或将指向SQL_INTERVAL_STRUCT结构的指针作为对**SQLGetData**调用中的*TargetValuePtr*参数）。
