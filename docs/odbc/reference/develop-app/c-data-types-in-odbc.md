---
title: ODBC 中的 C 数据类型 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], C data types
- C data types [ODBC], about C data types
- C data types [ODBC]
ms.assetid: c91bef31-3794-4736-966a-d50997b2233c
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 815dcb47a34d2e0729111b2a34693f1e6f4de557
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="c-data-types-in-odbc"></a>ODBC 中的 C 数据类型
ODBC 定义由应用程序变量和其相应的类型标识符的 C 数据类型。 绑定到结果集中的列和语句参数的缓冲区使用这些名称。 例如，假设应用程序想要从字符格式的结果集列中检索数据。 它声明的变量 SQLCHAR * 数据类型，并将此变量绑定到结果集列与 SQL_C_CHAR 类型标识符。 C 数据类型和类型标识符的完整列表，请参阅[附录 d： 数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 ODBC 还定义了从每个 SQL 数据类型为 C 数据类型的默认映射。 例如，数据源中的 2 字节整数被映射到应用程序中的 2 字节整数。 若要使用的默认映射，应用程序，请指定 SQL_C_DEFAULT 类型标识符。 但是，建议不要使用此标识符互操作性的原因。  
  
 在 ODBC 1 中定义的所有整数 C 数据类型 *.x*是否已进行签名。 无符号的 C 数据类型和其相应的类型标识符被添加在 ODBC 2.0。 因此，应用程序和驱动程序需要特别注意 1 在处理时 *.x*版本。  
  
## <a name="c-data-type-extensibility"></a>C 数据类型扩展性  
 在 ODBC 3.8，你可以指定特定驱动程序的 C 数据类型。 这使你可以将 SQL 类型 ODBC 应用程序中的特定于驱动程序的 C 类型作为绑定，当您调用[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)， [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)，或[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)。 这可能有助于支持新的服务器类型，因为现有的 C 数据类型可能无法正确反映新的服务器数据类型。 使用特定于驱动程序的 C 类型会增加驱动程序可以执行的转换的数。  
  
 例如，假设数据库管理系统 (DBMS) 引入了新的 SQL 类型， **DATETIMEOFFSET**，用于表示的日期和时间与时区信息。 对应于的 ODBC 中将有任何特定的 C 类型**DATETIMEOFFSET**。 应用程序将需要将绑定**DATETIMEOFFSET** SQL_C_BINARY 以及强制转换到用户定义数据类型。 从开始在 ODBC 3.8 C 数据类型可扩展性，驱动程序可以定义新的相应 C 类型。 例如，对于新的 SQL 类型 DATETIMEOFFSET 中，该驱动程序可以定义如 SQL_C_DATETIMEOFFSET 对应的新 C 类型。 然后，应用程序可以将新的 SQL 类型绑定为特定于驱动程序的 C 类型。  
  
 C 数据类型定义驱动程序中，如下所示：  
  
-   应用程序、 ODBC 驱动程序和驱动程序管理器的 ODBC 符合性级别是 3.8 （或更高版本）。  
  
-   特定于驱动程序的 C 类型的数据范围是 0x4000 和 0x7FFF 之间。  
  
-   该驱动程序定义的 C 类型与对应的数据的结构。  进行这种特定于驱动程序的 SDK。  
  
 驱动程序管理器将不会验证中 0x4000 和 0x7FFF; 范围内定义的 C 类型该驱动程序将执行验证和任何数据类型转换。 但是，如果传递给驱动程序管理器的 C 类型的数据范围之间 0x8000 到 0xFFFF 或 0x0000 和 0x3FFF 之间，驱动程序管理器将验证 C 数据类型。  
  
> [!NOTE]  
>  特定于驱动程序的 C 数据类型应驱动程序文档中所述。  
  
 若要指定的 3.8 ODBC 符合性级别，应用程序调用[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)并且 SQL_ATTR_ODBC_VERSION 属性设置为**SQL_OV_ODBC3_80**。 若要确定版本的驱动程序，应用程序调用**SQLGetInfo**与 SQL_DRIVER_ODBC_VER。  
  
 有关 ODBC 3.8 的详细信息，请参阅[What's New in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)。  
  
## <a name="see-also"></a>另请参阅  
 [C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)
