---
title: 附录 D：数据类型 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c1abadb962e3a1ee9327bbb8d84e52d180b4a7e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292457"
---
# <a name="appendix-d-data-types"></a>附录 D：数据类型
ODBC 定义了两组数据类型：SQL 数据类型和 C 数据类型。 SQL 数据类型指示存储在数据源中的数据的数据类型。 C 数据类型指示存储在应用程序缓冲区中的数据的数据类型。  
  
 SQL 数据类型由每个 DBMS 根据 SQL-92 标准定义。 对于 SQL-92 标准中指定的每个 SQL 数据类型，ODBC 定义类型标识符，该标识符是**一个#define**值，在 ODBC 函数中作为参数传递或在结果集的元数据中返回。 ODBC 不支持的唯一 SQL-92 数据类型是 BIT（ODBC SQL_BIT类型具有不同的特征）、BIT_VARYING、TIME_WITH_TIMEZONE、TIMESTAMP_WITH_TIMEZONE和NATIONAL_CHARACTER。 驱动程序负责将特定于数据源的 SQL 数据类型映射到 ODBC SQL 数据类型标识符和特定于驱动程序的 SQL 数据类型标识符。 SQL 数据类型在实现描述符SQL_DESC_CONCISE_TYPE字段中指定。  
  
 ODBC 定义 C 数据类型及其相应的 ODBC 类型标识符。 应用程序指定缓冲区的 C 数据类型，该类型将通过在调用**SQLBindCol**或**SQLGetData**中在*TargetType*参数中传递相应的 C 类型标识符来接收结果集数据。 它通过在调用**SQLBind参数**中的*ValueType*参数中传递相应的 C 类型标识符来指定包含语句参数的缓冲区的 C 类型。 C 数据类型在应用程序描述符的SQL_DESC_CONCISE_TYPE字段中指定。  
  
> [!NOTE]  
>  没有特定于驱动程序的 C 数据类型。  
  
 每个 SQL 数据类型对应于 ODBC C 数据类型。 在从数据源返回数据之前，驱动程序会将其转换为指定的 C 数据类型。 在将数据发送到数据源之前，驱动程序会将其从指定的 C 数据类型转换。  
  
 本附录包含以下主题。  
  
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
