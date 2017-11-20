---
title: "附录 d： 数据类型 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- C data types [ODBC], defined
- SQL data types [ODBC], defined
- data types [ODBC]
- data types [ODBC], about data types
ms.assetid: 981d49c3-3531-4543-aa75-5bd9e4f67000
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a543430479a33953e087fd50c91f7f2a307fc204
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="appendix-d-data-types"></a>附录 d： 数据类型
ODBC 定义了两个集的数据类型： SQL 数据类型和 C 数据类型。 SQL 数据类型表示存储在数据源的数据的数据类型。 C 数据类型表示存储在应用程序缓冲区中数据的数据类型。  
  
 SQL 数据类型由 sql-92 标准根据每个 DBMS 定义。 对于 sql-92 标准中指定的每个 SQL 数据类型，ODBC 定义类型标识符，它是**#define**值，该值是作为 ODBC 函数中的自变量传递或返回的结果集的元数据中。 唯一的 SQL 92 不支持 ODBC 的数据类型是的位 （ODBC SQL_BIT 类型具有不同的特征）、 BIT_VARYING、 TIME_WITH_TIMEZONE、 TIMESTAMP_WITH_TIMEZONE 和 NATIONAL_CHARACTER。 驱动程序负责将数据源 – 特定 SQL 数据类型映射到 ODBC SQL 数据类型标识符和特定于驱动程序的 SQL 数据类型的标识符。 在实现描述符的 SQL_DESC_CONCISE_TYPE 字段中指定的 SQL 数据类型。  
  
 ODBC 定义的 C 数据类型和其相应的 ODBC 类型标识符。 应用程序指定将通过传递中的相应 C 类型标识符接收结果集数据的缓冲区的 C 数据类型*TargetType*对的调用中的自变量**SQLBindCol**或**SQLGetData**。 它指定通过传递相应的 C 类型标识符中包含的语句参数的缓冲区的 C 类型*ValueType*对的调用中的自变量**SQLBindParameter**。 在应用程序描述符的 SQL_DESC_CONCISE_TYPE 字段中指定的 C 数据类型。  
  
> [!NOTE]  
>  没有特定于驱动程序的 C 数据类型。  
  
 每个 SQL 数据类型对应于 ODBC C 数据类型。 再从数据源中返回数据，该驱动程序将其转换为指定的 C 数据类型。 在将数据发送到数据源之前, 驱动程序将其转换从指定的 C 数据类型。  
  
 本附录包含以下主题。  
  
-   [使用数据类型标识符](../../../odbc/reference/appendixes/using-data-type-identifiers.md)  
  
-   [SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)  
  
-   [C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)  
  
-   [数据类型标识符和描述符](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)  
  
-   [伪类型标识符](../../../odbc/reference/appendixes/pseudo-type-identifiers.md)  
  
-   [以二进制格式传输数据](../../../odbc/reference/appendixes/transferring-data-in-its-binary-form.md)  
  
-   [间隔和数值数据类型的准则](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md)  
  
-   [公历的约束](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)  
  
-   [列大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)  
  
-   [将数据从 SQL 转换为 C 数据类型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)  
  
-   [将 C 中的数据转换为 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)  
  
 ODBC 数据类型的说明，请参阅[ODBC 中的数据类型](../../../odbc/reference/develop-app/data-types-in-odbc.md)。 有关特定于驱动程序的 SQL 数据类型的信息，请参阅驱动程序的文档。

