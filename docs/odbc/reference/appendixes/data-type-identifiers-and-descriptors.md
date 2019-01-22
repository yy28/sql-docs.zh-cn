---
title: 数据类型标识符和描述符 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d50d0bdfe31db1ad002c4915d7afa2c2decb79bb
ms.sourcegitcommit: 480961f14405dc0b096aa8009855dc5a2964f177
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2019
ms.locfileid: "54419942"
---
# <a name="data-type-identifiers-and-descriptors"></a>数据类型标识符和描述符
中列出的数据类型[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)并[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)本附录前面的部分是"简洁"数据类型：每个标识符是指一种数据类型。 没有标识符和数据类型之间的一一对应关系。 描述符，但是，此不能在所有情况下使用单个值来标识数据类型。 在某些情况下，它们可以使用"详细"的数据类型和类型子代码。 对于除日期时间和间隔数据类型的所有数据类型，详细的类型标识符的简洁类型标识符相同，SQL_DESC_DATETIME_INTERVAL_CODE 中的值等于 0。 对于日期时间和间隔数据类型，但是，详细的类型 （SQL_DATETIME 或 SQL_INTERVAL） 存储中的 SQL_DESC_TYPE、 简洁类型存储在 SQL_DESC_CONCISE_TYPE，并且为每种简洁类型子代码存储在 SQL_DESC_DATETIME_INTERVAL_CODE。 设置这些字段之一会影响其他。 有关这些字段的详细信息，请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)函数说明。  
  
 为某些数据类型设置的 SQL_DESC_TYPE 或 SQL_DESC_CONCISE_TYPE 字段后，SQL_DESC_DATETIME_INTERVAL_PRECISION、 SQL_DESC_LENGTH、 SQL_DESC_PRECISION 和 SQL_DESC_SCALE 字段将自动设置为默认值，根据数据类型。 有关详细信息，请参阅中的 SQL_DESC_TYPE 字段的说明[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。 如果默认值设置的任何不适当，应用程序应显式设置描述符字段通过调用**SQLSetDescField**。  
  
 下表显示了简单的类型标识符、 详细的类型标识符和类型为每个日期时间和间隔 SQL 和 C 类型标识符的子代码。 此表所示，对于日期时间和间隔数据类型的 SQL_DESC_TYPE 和 SQL_DESC_DATETIME_INTERVAL_CODE 字段具有 SQL 数据类型 （在实现描述符） 和 （在应用程序的 C 数据类型都相同的清单常量描述符）。  
  
|简单的 SQL 类型|简单的 C 类型|详细的类型|DATETIME_INTERVAL_CODE|  
|----------------------|--------------------|------------------|------------------------------|  
|SQL_TYPE_DATE|SQL_C_TYPE_DATE|SQL_DATETIME|SQL_CODE_DATE|  
|SQL_TYPE_TIME|SQL_C_TYPE_TIME|SQL_DATETIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|SQL_DATETIME|SQL_CODE_TIMESTAMP|  
|SQL_INTERVAL_MONTH|SQL_C_INTERVAL_MONTH|SQL_INTERVAL|SQL_CODE_MONTH|  
|SQL_INTERVAL_YEAR|SQL_C_INTERVAL_YEAR|SQL_INTERVAL|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH|SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_INTERVAL|SQL_CODE_YEAR_TO_MONTH|  
|S|SQL_INTERVAL_DAY|SQL_C_INTERVAL_DAY|SQL_INTERVAL|SQL_CODE_DAY|  
|SQL_INTERVAL_HOUR|SQL_C_INTERVAL_HOUR|SQL_INTERVAL|SQL_CODE_HOUR|  
|SQL_INTERVAL_MINUTE|SQL_C_INTERVAL_MINUTE|SQL_INTERVAL|SQL_CODE_MINUTE|  
|SQL_INTERVAL_SECOND|SQL_C_INTERVAL_SECOND|SQL_INTERVAL|SQL_CODE_SECOND|  
|SQL_INTERVAL_DAY_TO_HOUR|SQL_C_INTERVAL_DAY_TO_HOUR|SQL_INTERVAL|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE|SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_INTERVAL|SQL_CODE_DAY_TO_MINUTE|  
|SQL_INTERVAL_DAY_TO_SECOND|SQL_C_INTERVAL_DAY_TO_SECOND|SQL_INTERVAL|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR_TO_MINUTE|SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_INTERVAL|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND|SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_INTERVAL|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE_TO_SECOND|SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_INTERVAL|SQL_CODE_MINUTE_TO_SECOND|
