---
title: "数据类型标识符和描述符 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], identifiers
- identifiers [ODBC], data types
- descriptors [ODBC], data types
- verbose data types [ODBC]
- data types [ODBC], descriptors
- concise data types [ODBC]
ms.assetid: f0077c9b-8eb2-4b5f-8c4c-7436fdef37ab
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0040a426bd11048a993e98015a536c76e1b4381c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="data-type-identifiers-and-descriptors"></a>数据类型标识符和描述符
中列出的数据类型[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)和[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)本附录前面的部分是"简洁"数据类型： 每个标识符是指一种数据类型。 没有标识符和数据类型之间的一一对应关系。 描述符，但是，此未显示在所有情况下使用单个值以确定数据类型。 在某些情况下，它们可以使用"详细"数据类型和类型子代码。 对于除日期时间和间隔数据类型以外的所有数据类型，详细类型标识符等同于简洁类型标识符和 SQL_DESC_DATETIME_INTERVAL_CODE 中的值等于 0。 对于日期时间和间隔的数据类型，但是，详细的类型 （SQL_DATETIME 或 SQL_INTERVAL） 存储在 SQL_DESC_TYPE、 简洁类型存储在 SQL_DESC_CONCISE_TYPE，和为每种简洁的类型的子存储在 SQL_DESC_DATETIME_INTERVAL_CODE。 设置这些字段之一将影响其他。 有关这些字段的详细信息，请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)函数说明。  
  
 当 SQL_DESC_TYPE 或 SQL_DESC_CONCISE_TYPE 字段设置为某些数据类型时，SQL_DESC_DATETIME_INTERVAL_PRECISION、 SQL_DESC_LENGTH、 SQL_DESC_PRECISION 和 SQL_DESC_SCALE 字段将自动设置为默认值，作为适用于数据类型。 有关详细信息，请参阅中的 SQL_DESC_TYPE 字段的说明[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。 如果任何默认值设置不合适，应用程序应显式设置通过调用描述符字段**SQLSetDescField**。  
  
 下表显示简洁类型标识符、 详细类型标识符和类型为每个日期时间和间隔 SQL 和 C 类型标识符的子代码。 SQL_DESC_TYPE 和 SQL_DESC_DATETIME_INTERVAL_CODE 字段，此表所示，对于日期时间和间隔的数据类型，具有相同的清单常量对于 SQL 数据类型 （在实现描述符） 和 （在应用程序的 C 数据类型描述符）。  
  
|简洁 SQL 类型|简洁 C 类型|详细的类型|DATETIME_INTERVAL_CODE|  
|----------------------|--------------------|------------------|------------------------------|  
|SQL_TYPE_DATE|SQL_C_TYPE_DATE|SQL_DATETIME|SQL_CODE_DATE|  
|SQL_TYPE_TIME|SQL_C_TYPE_TIME|SQL_DATETIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|SQL_DATETIME|SQL_CODE_TIMESTAMP|  
|SQL_INTERVAL_MONTH|SQL_C_INTERVAL_MONTH|SQL_INTERVAL|SQL_CODE_MONTH|  
|SQL_INTERVAL_YEAR|SQL_C_INTERVAL_YEAR|SQL_INTERVAL|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH|SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_INTERVAL|SQL_CODE_YEAR_TO_MONTH|  
QL_INTERVAL_DAY|SQL_C_INTERVAL_DAY|SQL_INTERVAL|SQL_CODE_DAY|  
|SQL_INTERVAL_HOUR|SQL_C_INTERVAL_HOUR|SQL_INTERVAL|SQL_CODE_HOUR|  
|SQL_INTERVAL_MINUTE|SQL_C_INTERVAL_MINUTE|SQL_INTERVAL|SQL_CODE_MINUTE|  
|SQL_INTERVAL_SECOND|SQL_C_INTERVAL_SECOND|SQL_INTERVAL|SQL_CODE_SECOND|  
|SQL_INTERVAL_DAY_TO_HOUR|SQL_C_INTERVAL_DAY_TO_HOUR|SQL_INTERVAL|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE|SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_INTERVAL|SQL_CODE_DAY_TO_MINUTE|  
QL_INTERVAL_DAY_TO_SECOND|SQL_C_INTERVAL_DAY_TO_SECOND|SQL_INTERVAL|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR_TO_MINUTE|SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_INTERVAL|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND|SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_INTERVAL|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE_TO_SECOND|SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_INTERVAL|SQL_CODE_MINUTE_TO_SECOND|
