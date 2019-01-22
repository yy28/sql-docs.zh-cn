---
title: 从 SQL 到 c:年月间隔 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 01af57739f23db586991f8a54d14b90b47f15933
ms.sourcegitcommit: 480961f14405dc0b096aa8009855dc5a2964f177
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2019
ms.locfileid: "54419932"
---
# <a name="sql-to-c-year-month-intervals"></a>从 SQL 到 c:年月间隔

年-月间隔 ODBC SQL 数据类型的标识符如下所示：

- SQL_INTERVAL_MONTH
- SQL_INTERVAL_YEAR
- SQL_INTERVAL_YEAR_TO_MONTH

下表显示 ODBC C 数据类型到哪些年月间隔 SQL 数据可能转换。 列和表中的条款的说明，请参阅[从 SQL 到 C 数据类型的转换的数据](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  

|C 类型标识符|测试|TargetValuePtr|StrLen_or_IndPtr|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_INTERVAL_MONTH[a]<br /><br /> SQL_C_INTERVAL_YEAR[a]<br /><br /> SQL_C_INTERVAL_YEAR_TO_MONTH[a]|不会被截断尾随的字段部分<br /><br /> 截断尾随的字段部分<br /><br /> 前导精度是目标的不足够大以保存数据源中|数据<br /><br /> 截断的数据<br /><br /> 未定义|以字节为单位的数据的长度<br /><br /> 以字节为单位的数据的长度<br /><br /> 未定义|不适用<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT[b]<br /><br /> SQL_C_UTINYINT[b]<br /><br /> SQL_C_USHORT[b]<br /><br /> SQL_C_SHORT[b]<br /><br /> SQL_C_SLONG[b]<br /><br /> SQL_C_ULONG[b]<br /><br /> SQL_C_NUMERIC[b]<br /><br /> SQL_C_BIGINT[b]|时间间隔精度是单个字段和数据转换而无需截断<br /><br /> 时间间隔精度是单个字段或整个已截断<br /><br /> 时间间隔精度不是单个字段|数据<br /><br /> 截断的数据<br /><br /> 未定义|C 数据类型的大小<br /><br /> 以字节为单位的数据的长度<br /><br /> C 数据类型的大小|不适用<br /><br /> 22003<br /><br /> 22015|  
|SQL_C_BINARY|数据的字节长度 < = *BufferLength*<br /><br /> 数据的字节长度 > *BufferLength*|数据<br /><br /> 未定义|以字节为单位的数据的长度<br /><br /> 未定义|不适用<br /><br /> 22003|  
|SQL_C_CHAR|字符字节长度 < *BufferLength*<br /><br /> 数字位数 （而不是小数部分） 的整个 < *BufferLength*<br /><br /> 数字位数整体 （而不是小数） > = *BufferLength*|数据<br /><br /> 截断的数据<br /><br /> 未定义|C 数据类型的大小<br /><br /> C 数据类型的大小<br /><br /> 未定义|不适用<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|字符长度 < *BufferLength*<br /><br /> 数字位数 （而不是小数部分） 的整个 < *BufferLength*<br /><br /> 数字位数整体 （而不是小数） > = *BufferLength*|数据<br /><br /> 截断的数据<br /><br /> 未定义|C 数据类型的大小<br /><br /> C 数据类型的大小<br /><br /> 未定义|不适用<br /><br /> 01004<br /><br /> 22003|  
  
 [a] 的年月间隔 SQL 类型可以转换为任何年-月间隔 C 类型。  
  
 [b] 如果时间间隔精度为单个字段 （一个年或每月的），可将 SQL 类型的时间间隔转换任何精确数值 （SQL_C_STINYINT、 SQL_C_UTINYINT、 SQL_C_USHORT、 SQL_C_SHORT、 SQL_C_SLONG、 SQL_C_ULONG 或 SQL_C_NUMERIC）。  

## <a name="default-conversions"></a>默认的转换

SQL 类型的时间间隔的默认转换为相应的 C 间隔数据类型。 应用程序然后将列或参数绑定 （或 ARD 的相应记录中设置 SQL_DESC_DATA_PTR 字段） 以指向已初始化 SQL_INTERVAL_STRUCT 结构 (或将指针传递给SQL_INTERVAL_STRUCT结构*TargetValuePtr*的调用中的自变量**SQLGetData**)。
