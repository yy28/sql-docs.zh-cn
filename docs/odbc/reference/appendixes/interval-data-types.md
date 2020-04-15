---
title: 间隔数据类型 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ee4a6e845e0bc0830f514b2e768075dd75bcf6e6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304963"
---
# <a name="interval-data-types"></a>间隔数据类型
间隔定义为两个日期和时间之间的差异。 间隔以两种不同的方式之一表示。 一个是*年月*间隔，以年数表示间隔，以月数表示整数。 另一个是以天、分钟和秒表示间隔的*日间*间隔。 这两种类型的间隔是截然不同的，不能混合，因为月份可以有不同的天数。  
  
 间隔由一组字段组成。 字段之间存在隐含排序。 例如，在一年到月之间，年份先到一个，然后是月份。 同样，在一天的到分钟的间隔中，字段按顺序按天、小时和分钟的顺序排列。 间隔类型中的第一个字段称为*前导*字段或*高阶*字段。 最后一个字段称为*尾随*字段。  
  
 在所有间隔中，前导字段不受公历规则的约束。 例如，在小时到分钟的间隔内，小时字段不限制为 0 和 23（包括）之间，因为它通常如此。 前导字段后面的尾随字段遵循公历的通常约束。 有关详细信息，请参阅[公历的约束](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)，请参阅本附录后面的限制。  
  
 有 13 个间隔 SQL 数据类型和 13 个间隔 C 数据类型。 每个间隔 C 数据类型都使用相同的结构，SQL_INTERVAL_STRUCT，以包含间隔数据。 （有关详细信息，请参阅下一节 C[间隔结构](../../../odbc/reference/appendixes/c-interval-structure.md)。有关 SQL 数据类型的详细信息，请参阅[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)。有关 C 数据类型的详细信息，请参阅[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)。  
  
|类型标识符|类|描述|  
|---------------------|-----------|-----------------|  
|MONTH|年月|两个日期之间的月数。|  
|YEAR|年月|两个日期之间的年数。|  
|YEAR_TO_MONTH|年月|两个日期之间的年数和月数。|  
|DAY|白天|两个日期之间的天数。|  
|HOUR|白天|两个日期/时间之间的小时数。|  
|MINUTE|白天|两个日期/时间之间的分钟数。|  
|SECOND|白天|两个日期/时间之间的秒数。|  
|DAY_TO_HOUR|白天|两个日期/时间之间的天数/小时数。|  
|DAY_TO_MINUTE|白天|两个日期/时间之间的天数/小时/分钟数。|  
|DAY_TO_SECOND|白天|两个日期/时间之间的天数/小时/分钟/秒数。|  
|HOUR_TO_MINUTE|白天|两个日期/时间之间的小时/分钟数。|  
|HOUR_TO_SECOND|白天|两个日期/时间之间的小时/分钟/秒数。|  
|MINUTE_TO_SECOND|白天|两个日期/时间之间的分钟/秒数。|  
  
 本部分包含以下主题。  
  
-   [C 间隔结构](../../../odbc/reference/appendixes/c-interval-structure.md)  
  
-   [间隔数据类型精度](../../../odbc/reference/appendixes/interval-data-type-precision.md)  
  
-   [间隔数据类型长度](../../../odbc/reference/appendixes/interval-data-type-length.md)  
  
-   [间隔文本](../../../odbc/reference/appendixes/interval-literals.md)  
  
-   [重写间隔数据类型的默认前导和秒精度](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)
