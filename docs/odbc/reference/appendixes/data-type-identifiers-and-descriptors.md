---
title: 数据类型标识符和描述符 |Microsoft Docs
ms.custom: ''
ms.date: 02/02/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- identifiers [ODBC], data types
- descriptors [ODBC], data types
- verbose data types [ODBC]
- data types [ODBC], descriptors
- concise data types [ODBC]
ms.assetid: f0077c9b-8eb2-4b5f-8c4c-7436fdef37ab
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f65bc86213f99112daf17c67a4ca522490d32149
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284480"
---
# <a name="data-type-identifiers-and-descriptors"></a>数据类型标识符和描述符
本附录前面的 " [SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)" 和 " [C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)" 部分中列出的数据类型为 "简洁" 数据类型：每个标识符引用一种数据类型。 标识符和数据类型之间存在一对一的对应关系。 但是，说明符并非在所有情况下都使用单个值来标识数据类型。 在某些情况下，它们使用 "verbose" 数据类型和类型子代码。 对于除 datetime 和 interval 数据类型之外的所有数据类型，详细类型标识符与简明类型标识符相同，SQL_DESC_DATETIME_INTERVAL_CODE 中的值等于0。 但对于 datetime 和 interval 数据类型，详细类型（SQL_DATETIME 或 SQL_INTERVAL）存储在 SQL_DESC_TYPE 中，一个简洁的类型存储在 SQL_DESC_CONCISE_TYPE 中，每个简明类型的子代码存储在 SQL_DESC_DATETIME_INTERVAL_CODE 中。 设置其中一个字段会影响其他字段。 有关这些字段的详细信息，请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)函数说明。  
  
 为某些数据类型设置 SQL_DESC_TYPE 或 SQL_DESC_CONCISE_TYPE 字段时，SQL_DESC_DATETIME_INTERVAL_PRECISION、SQL_DESC_LENGTH、SQL_DESC_PRECISION 和 SQL_DESC_SCALE 字段将自动设置为适用于数据类型的默认值。 有关详细信息，请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中的 SQL_DESC_TYPE 字段的说明。 如果设置的任何默认值不合适，则应用程序应通过调用**SQLSetDescField**显式设置描述符字段。  
  
 下表显示了每个 datetime 和 interval SQL 和 C 类型标识符的简明类型标识符、详细类型标识符和类型子代码。 正如表中所示，对于 datetime 和 interval 数据类型，SQL_DESC_TYPE 和 SQL_DESC_DATETIME_INTERVAL_CODE 字段对 SQL 数据类型（在实现描述符中）和 C 数据类型（在应用程序描述符中）具有相同的清单常量。  
  
|简洁的 SQL 类型|简洁 C 类型|详细类型|DATETIME_INTERVAL_CODE|  
|----------------------|--------------------|------------------|------------------------------|  
|SQL_TYPE_DATE|SQL_C_TYPE_DATE|SQL_DATETIME|SQL_CODE_DATE|  
|SQL_TYPE_TIME|SQL_C_TYPE_TIME|SQL_DATETIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|SQL_DATETIME|SQL_CODE_TIMESTAMP|  
|SQL_INTERVAL_MONTH|SQL_C_INTERVAL_MONTH|SQL_INTERVAL|SQL_CODE_MONTH|  
|SQL_INTERVAL_YEAR|SQL_C_INTERVAL_YEAR|SQL_INTERVAL|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH|SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_INTERVAL|SQL_CODE_YEAR_TO_MONTH|  
|SQL_INTERVAL_DAY|SQL_C_INTERVAL_DAY|SQL_INTERVAL|SQL_CODE_DAY|  
|SQL_INTERVAL_HOUR|SQL_C_INTERVAL_HOUR|SQL_INTERVAL|SQL_CODE_HOUR|  
|SQL_INTERVAL_MINUTE|SQL_C_INTERVAL_MINUTE|SQL_INTERVAL|SQL_CODE_MINUTE|  
|SQL_INTERVAL_SECOND|SQL_C_INTERVAL_SECOND|SQL_INTERVAL|SQL_CODE_SECOND|  
|SQL_INTERVAL_DAY_TO_HOUR|SQL_C_INTERVAL_DAY_TO_HOUR|SQL_INTERVAL|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE|SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_INTERVAL|SQL_CODE_DAY_TO_MINUTE|  
|SQL_INTERVAL_DAY_TO_SECOND|SQL_C_INTERVAL_DAY_TO_SECOND|SQL_INTERVAL|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR_TO_MINUTE|SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_INTERVAL|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND|SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_INTERVAL|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE_TO_SECOND|SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_INTERVAL|SQL_CODE_MINUTE_TO_SECOND|
