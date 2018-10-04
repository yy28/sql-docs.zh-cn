---
title: 间隔数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 930a848ea01d128cb248c7929408ce7510937ad9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622215"
---
# <a name="interval-data-types"></a>间隔数据类型
一个时间间隔被指两个日期和时间之间的差异。 在两种不同方式之一表示时间间隔。 一个是*年-月*表示年和整月数方面的时间间隔的间隔。 另一个是*日期时间*表达方面天、 分钟和秒的时间间隔的间隔。 这两种类型的间隔不同，并且不能混用，因为几个月可以具有不同数量的天。  
  
 一个时间间隔包含的一组字段。 没有在字段之间的隐式排序。 例如，年-月间隔年在前后, 跟每月。 同样，在一天分钟间隔中，字段都在订单日期、 小时和分钟。 间隔类型的第一个字段称为*前导*字段中，或*高序位*字段。 最后一个字段称为*尾随*字段。  
  
 在所有时间间隔中的前导字段不受公历日历以来的规则。 例如，小时分钟间隔的小时字段是不受限制必须介于 0 到 23 之间 （含），因为它通常是。 前导字段之后的尾随字段按照常用公历的约束。 有关详细信息，请参阅[公历的约束](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)、 本附录中更高版本。  
  
 有 13 间隔 SQL 数据类型和 13 间隔 C 数据类型。 每个间隔 C 数据类型使用相同的结构，SQL_INTERVAL_STRUCT，以包含数据间隔。 (有关详细信息，请参阅下一部分中， [C 间隔结构](../../../odbc/reference/appendixes/c-interval-structure.md)。)SQL 数据类型的详细信息，请参阅[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md); 有关 C 数据类型的详细信息，请参阅[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)。  
  
|类型标识符|类|Description|  
|---------------------|-----------|-----------------|  
|MONTH|年月|两个日期之间的月数。|  
|YEAR|年月|两个日期之间的年数。|  
|YEAR_TO_MONTH|年月|年和两个日期之间的月数。|  
|DAY|日期时间|两个日期之间天数。|  
|HOUR|日期时间|两个之间的小时数的日期/时间。|  
|MINUTE|日期时间|两个之间的分钟数的日期/时间。|  
|SECOND|日期时间|两个之间的秒数的日期/时间。|  
|DAY_TO_HOUR|日期时间|天/之间的小时数两个日期/时间。|  
|DAY_TO_MINUTE|日期时间|天/小时/之间的分钟数两个日期/时间。|  
|DAY_TO_SECOND|日期时间|天/小时/分钟/之间的秒数两个日期/时间。|  
|HOUR_TO_MINUTE|日期时间|小时/之间的分钟数两个日期/时间。|  
|HOUR_TO_SECOND|日期时间|小时/分钟/之间的秒数两个日期/时间。|  
|MINUTE_TO_SECOND|日期时间|分钟/之间的秒数两个日期/时间。|  
  
 本部分包含以下主题。  
  
-   [C 间隔结构](../../../odbc/reference/appendixes/c-interval-structure.md)  
  
-   [间隔数据类型精度](../../../odbc/reference/appendixes/interval-data-type-precision.md)  
  
-   [间隔数据类型长度](../../../odbc/reference/appendixes/interval-data-type-length.md)  
  
-   [间隔文本](../../../odbc/reference/appendixes/interval-literals.md)  
  
-   [重写间隔数据类型的默认前导和秒精度](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)
