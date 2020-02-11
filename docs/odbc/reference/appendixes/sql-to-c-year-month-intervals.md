---
title: SQL 到 C：年-月间隔 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2c7412226dd0674022da022b0a0a63e5bf2063cf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68065037"
---
# <a name="sql-to-c-year-month-intervals"></a>从 SQL 到 C：年月间隔

每月间隔 ODBC SQL 数据类型的标识符如下：

- SQL_INTERVAL_MONTH
- SQL_INTERVAL_YEAR
- SQL_INTERVAL_YEAR_TO_MONTH

下表显示了每个月的 SQL 数据可转换为的 ODBC C 数据类型。 有关表中的列和字词的说明，请参阅将[数据从 SQL 转换为 C 数据类型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  

|C 类型标识符|测试|TargetValuePtr|StrLen_or_IndPtr|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_INTERVAL_MONTH [a]<br /><br /> SQL_C_INTERVAL_YEAR [a]<br /><br /> SQL_C_INTERVAL_YEAR_TO_MONTH [a]|不截断尾部字段部分<br /><br /> 尾随字段部分已截断<br /><br /> 目标的前导精度不够大，无法保存源中的数据|data<br /><br /> 截断的数据<br /><br /> 未定义|数据的长度（以字节为单位）<br /><br /> 数据的长度（以字节为单位）<br /><br /> 未定义|不适用<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT [b]<br /><br /> SQL_C_UTINYINT [b]<br /><br /> SQL_C_USHORT [b]<br /><br /> SQL_C_SHORT [b]<br /><br /> SQL_C_SLONG [b]<br /><br /> SQL_C_ULONG [b]<br /><br /> SQL_C_NUMERIC [b]<br /><br /> SQL_C_BIGINT [b]|间隔精度是单个字段，数据已转换但未截断<br /><br /> 间隔精度是单个字段并且截断了整个<br /><br /> 间隔精度不是单个字段|data<br /><br /> 截断的数据<br /><br /> 未定义|C 数据类型的大小<br /><br /> 数据的长度（以字节为单位）<br /><br /> C 数据类型的大小|不适用<br /><br /> 22003<br /><br /> 22015|  
|SQL_C_BINARY|Data <的字节长度 = *BufferLength*<br /><br /> 数据 > 的字节长度*BufferLength*|data<br /><br /> 未定义|数据的长度（以字节为单位）<br /><br /> 未定义|不适用<br /><br /> 22003|  
|SQL_C_CHAR|字符字节长度 < *BufferLength*<br /><br /> < *BufferLength*的整个数字（相对于小数部分）<br /><br /> 整数位数（相对于小数） >= *BufferLength*|data<br /><br /> 截断的数据<br /><br /> 未定义|C 数据类型的大小<br /><br /> C 数据类型的大小<br /><br /> 未定义|不适用<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|字符长度 < *BufferLength*<br /><br /> < *BufferLength*的整个数字（相对于小数部分）<br /><br /> 整数位数（相对于小数） >= *BufferLength*|data<br /><br /> 截断的数据<br /><br /> 未定义|C 数据类型的大小<br /><br /> C 数据类型的大小<br /><br /> 未定义|不适用<br /><br /> 01004<br /><br /> 22003|  
  
 [a] 每月间隔 SQL 类型可以转换为任何年间隔 C 类型。  
  
 [b] 如果间隔精度是单个字段（一年或一个月），则间隔 SQL 类型可以转换为任何精确数值（SQL_C_STINYINT、SQL_C_UTINYINT、SQL_C_USHORT、SQL_C_SHORT、SQL_C_SLONG、SQL_C_ULONG 或 SQL_C_NUMERIC）。  

## <a name="default-conversions"></a>默认转换

间隔 SQL 类型的默认转换为相应的 C 间隔数据类型。 然后，应用程序绑定列或参数（或将 ARD 的适当记录中的 SQL_DESC_DATA_PTR 字段设置为），以指向已初始化的 SQL_INTERVAL_STRUCT 结构（或将指向 INTERVAL_STRUCT SQL_ 的指针作为*TargetValuePtr*参数传递到对**SQLGetData**的调用中）。
