---
title: 附录 d： 数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- C data types [ODBC], defined
- SQL data types [ODBC], defined
- data types [ODBC]
- data types [ODBC], about data types
ms.assetid: 981d49c3-3531-4543-aa75-5bd9e4f67000
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cfaecb5b3705e2c5affe8c2cda3e42eeaddf4156
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47669375"
---
# <a name="appendix-d-data-types"></a>附录 D：数据类型
ODBC 定义的数据类型的两个集： SQL 数据类型和 C 数据类型。 SQL 数据类型表示存储在数据源的数据的数据类型。 C 数据类型表示应用程序缓冲区中存储的数据的数据类型。  
  
 SQL 数据类型由每个 DBMS 根据 SQL-92 标准定义。 对于 SQL-92 标准中指定的每个 SQL 数据类型，ODBC 定义的类型标识符，即 **#define**值，该值是作为中的 ODBC 函数的参数传递或返回结果集的元数据中。 只有 SQL-92 不支持 ODBC 的数据类型是的位 （ODBC SQL_BIT 类型具有不同的特征）、 BIT_VARYING、 TIME_WITH_TIMEZONE、 TIMESTAMP_WITH_TIMEZONE 和 NATIONAL_CHARACTER。 驱动程序负责将数据源特定于 SQL 数据类型映射到 ODBC SQL 数据类型标识符和特定于驱动程序的 SQL 数据类型标识符。 SQL 数据类型的实现描述符 SQL_DESC_CONCISE_TYPE 字段中指定。  
  
 ODBC 定义的 C 数据类型和其相应的 ODBC 类型标识符。 应用程序指定将通过传递相应的 C 类型标识符中接收结果集数据的缓冲区的 C 数据类型*TargetType*调用中的参数**SQLBindCol**或**SQLGetData**。 它指定通过传递相应的 C 类型标识符中包含语句参数的缓冲区的 C 类型*ValueType*调用中的参数**SQLBindParameter**。 在应用程序描述符的 SQL_DESC_CONCISE_TYPE 字段中指定的 C 数据类型。  
  
> [!NOTE]  
>  没有特定于驱动程序的 C 数据类型。  
  
 每个 SQL 数据类型对应于 ODBC C 数据类型。 从数据源返回数据之前, 驱动程序将其转换为指定的 C 数据类型。 将数据发送到数据源之前, 驱动程序将其转换从指定的 C 数据类型。  
  
 本附录包含的以下主题。  
  
-   [使用数据类型标识符](../../../odbc/reference/appendixes/using-data-type-identifiers.md)  
  
-   [SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)  
  
-   [C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)  
  
-   [数据类型标识符和描述符](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)  
  
-   [伪类型标识符](../../../odbc/reference/appendixes/pseudo-type-identifiers.md)  
  
-   [以二进制格式传输数据](../../../odbc/reference/appendixes/transferring-data-in-its-binary-form.md)  
  
-   [间隔和数字数据类型的准则](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md)  
  
-   [公历的约束](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)  
  
-   [列大小、十进制数字、传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)  
  
-   [将数据从 SQL 转换为 C 数据类型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)  
  
-   [将数据从 C 转换为 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)  
  
 有关 ODBC 数据类型的说明，请参阅[ODBC 中的数据类型](../../../odbc/reference/develop-app/data-types-in-odbc.md)。 有关特定于驱动程序的 SQL 数据类型的信息，请参阅驱动程序的文档。
