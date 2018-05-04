---
title: Interval 数据类型 |Microsoft 文档
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
- second intervals [ODBC]
- data types [ODBC], interval data types
- interval data type [ODBC]
- day-time intervals [ODBC]
- intervals [ODBC], about intervals
- minute intervals [ODBC]
- day intervals [ODBC]
- year intervals [ODBC]
- month intervals [ODBC]
- interval data type [ODBC], about interval data types
- SQL data types [ODBC], interval
- year-month intervals [ODBC]
- C data types [ODBC], interval
- interval fields [ODBC]
ms.assetid: fba93f65-c1db-44f4-91ba-532f87241cf7
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ebc6b5d2a8e2277c3bb427053f43ebed4983e0b9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="interval-data-types"></a>Interval 数据类型
一个时间间隔被指两个日期和时间之间的差异。 按两种不同方式之一表示的时间间隔。 其中一个是*年-月*表示年和月八进制整数方面的时间间隔的间隔。 另一种是*一天时间*表示按天、 分钟和秒的间隔的间隔。 这两种类型的间隔不同，并且不能混合，因为月份可以具有不同的天数。  
  
 一个时间间隔包含的一组字段。 没有在字段之间的隐式排序。 例如，年-月的间隔年最先出现后, 跟一个月。 同样，天分钟的间隔，这些字段进行中的订单日、 小时和分钟。 间隔类型的第一个域称为*前导*字段，或*高序位*字段。 调用的最后一个字段*尾随*字段。  
  
 在所有时间间隔，前导字段不受规则的公历。 例如，小时分钟的间隔的小时字段是不受限制为介于 0 到 23 （含） 之间，因为它通常是。 前导字段之后的尾随字段按照公历的常用约束。 有关详细信息，请参阅[约束的公历](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)、 本附录内容更高版本。  
  
 有 13 间隔 SQL 数据类型和 13 interval C 数据类型。 每个间隔 C 数据类型使用相同的结构，SQL_INTERVAL_STRUCT，无法包含间隔的数据。 (有关详细信息，请参阅下一部分中， [C 间隔结构](../../../odbc/reference/appendixes/c-interval-structure.md)。)SQL 数据类型的详细信息，请参阅[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md); 有关 C 数据类型的详细信息，请参阅[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)。  
  
|类型标识符|类|Description|  
|---------------------|-----------|-----------------|  
|MONTH|年-月|两个日期之间的月份数。|  
|YEAR|年-月|两个日期之间的年份数。|  
|YEAR_TO_MONTH|年-月|年和两个日期之间的月数。|  
|DAY|一天时间|数的两个日期之间的天数。|  
|HOUR|一天时间|两个之间的小时数日期/时间。|  
|MINUTE|一天时间|两个之间的分钟数日期/时间。|  
|SECOND|一天时间|两个之间的秒数日期/时间。|  
|DAY_TO_HOUR|一天时间|天/之间的小时数两个日期/时间。|  
|DAY_TO_MINUTE|一天时间|天数/小时/之间的分钟数两个日期/时间。|  
|DAY_TO_SECOND|一天时间|天数/小时/分钟数/秒数之间两个日期/时间。|  
|HOUR_TO_MINUTE|一天时间|小时/之间的分钟数两个日期/时间。|  
|HOUR_TO_SECOND|一天时间|小时数/分钟数/秒数之间两个日期/时间。|  
|MINUTE_TO_SECOND|一天时间|分钟数/秒数之间两个日期/时间。|  
  
 本部分包含以下主题。  
  
-   [C 间隔结构](../../../odbc/reference/appendixes/c-interval-structure.md)  
  
-   [间隔数据类型精度](../../../odbc/reference/appendixes/interval-data-type-precision.md)  
  
-   [间隔数据类型长度](../../../odbc/reference/appendixes/interval-data-type-length.md)  
  
-   [间隔文本](../../../odbc/reference/appendixes/interval-literals.md)  
  
-   [重写间隔数据类型的默认前导和秒精度](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)
