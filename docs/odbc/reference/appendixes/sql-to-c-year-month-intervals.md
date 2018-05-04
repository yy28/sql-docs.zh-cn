---
title: 为 c： 年-月间隔 SQL |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], about converting
- data conversions from SQL to C types [ODBC], year-month intervals
- intervals [ODBC], converting
- year-month intervals [ODBC]
ms.assetid: 1233634b-8214-420f-b872-3b2630105ba4
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da1a3378ba16a360ff2e307219ea350fa6ed1efd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sql-to-c-year-month-intervals"></a>为 c： 年-月间隔的 SQL
年-月间隔 ODBC SQL 数据类型的标识符都是：  
  
 SQL_INTERVAL_YEAR  
  
 SQL_INTERVAL_MONTH  
  
 SQL_INTERVAL_YEAR_TO_MONTH  
  
 下表显示 ODBC C 数据类型到哪些年-月间隔 SQL 数据可能转换。 列和表中的条款的说明，请参阅[转换数据从 SQL C 数据类型到](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 类型标识符|测试|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_INTERVAL_MONTH [a]<br /><br /> SQL_C_INTERVAL_YEAR [a]<br /><br /> SQL_C_INTERVAL_YEAR_TO_MONTH [a]|不会被截断的尾随字段部分<br /><br /> 尾随字段部分被截断<br /><br /> 前导精度不是目标的不够大，无法从源中保存数据|Data<br /><br /> 截断的数据<br /><br /> 未定义|以字节为单位的数据的长度<br /><br /> 以字节为单位的数据的长度<br /><br /> 未定义|不适用<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT [b]<br /><br /> SQL_C_UTINYINT [b]<br /><br /> SQL_C_USHORT [b]<br /><br /> SQL_C_SHORT [b]<br /><br /> SQL_C_SLONG [b]<br /><br /> SQL_C_ULONG [b]<br /><br /> SQL_C_NUMERIC [b]<br /><br /> SQL_C_BIGINT [b]|间隔精度是单个字段和数据转换而不发生截断<br /><br /> 间隔精度是单个字段的和已截断整个<br /><br /> 间隔精度不是单个字段|Data<br /><br /> 截断的数据<br /><br /> 未定义|C 数据类型的大小<br /><br /> 以字节为单位的数据的长度<br /><br /> C 数据类型的大小|不适用<br /><br /> 22003<br /><br /> 22015|  
_C_BINARY|数据的字节长度 < = *BufferLength*<br /><br /> 数据的字节长度 > *BufferLength*|Data<br /><br /> 未定义|以字节为单位的数据的长度<br /><br /> 未定义|不适用<br /><br /> 22003|  
|SQL_C_CHAR|字符字节长度 < *BufferLength*<br /><br /> 整体 （而不是小数） 数字个数 < *BufferLength*<br /><br /> 整体 （而不是小数） 数字个数 > = *BufferLength*|Data<br /><br /> 截断的数据<br /><br /> 未定义|C 数据类型的大小<br /><br /> C 数据类型的大小<br /><br /> 未定义|不适用<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|字符长度 < *BufferLength*<br /><br /> 整体 （而不是小数） 数字个数 < *BufferLength*<br /><br /> 整体 （而不是小数） 数字个数 > = *BufferLength*|Data<br /><br /> 截断的数据<br /><br /> 未定义|C 数据类型的大小<br /><br /> C 数据类型的大小<br /><br /> 未定义|不适用<br /><br /> 01004<br /><br /> 22003|  
  
 可以为任何年-月间隔 C 类型转换 [a] 的年-月间隔 SQL 类型。  
  
 [b] 如果间隔精度，单个字段 （一个月或年的） 间隔 SQL 类型可转换为任何具体的数字 （SQL_C_STINYINT、 SQL_C_UTINYINT、 SQL_C_USHORT、 SQL_C_SHORT、 SQL_C_SLONG、 SQL_C_ULONG 或 SQL_C_NUMERIC）。  
  
 一个时间间隔 SQL 类型的默认转换是相应的 C 间隔数据类型。 应用程序然后将绑定的列或参数 （或设置 SQL_DESC_DATA_PTR 字段中的 ARD 相应的记录） 以指向初始化 SQL_INTERVAL_STRUCT 结构 (或将指针传递给 SQL_ INTERVAL_STRUCT 结构用作*TargetValuePtr*对的调用中的自变量**SQLGetData**)。
