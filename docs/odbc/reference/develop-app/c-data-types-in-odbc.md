---
title: ODBC 中的 C 数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], C data types
- C data types [ODBC], about C data types
- C data types [ODBC]
ms.assetid: c91bef31-3794-4736-966a-d50997b2233c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5e1efba2187e2c1f2d813d43640fc9259ad4f2b3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306292"
---
# <a name="c-data-types-in-odbc"></a>ODBC 中的 C 数据类型
ODBC 定义应用程序变量使用的 C 数据类型及其对应的类型标识符。 它们由绑定到结果集列和语句参数的缓冲区使用。 例如，假设某个应用程序想要以字符格式从结果集列中检索数据。 它声明了 SQLCHAR * 数据类型的变量，并将该变量绑定到结果集列，该结果集列的类型标识符为 SQL_C_CHAR。 有关 C 数据类型和类型标识符的完整列表，请参阅[附录 D：数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 ODBC 还定义了从每个 SQL 数据类型到 C 数据类型的默认映射。 例如，数据源中的2字节整数映射到应用程序中的2字节整数。 若要使用默认映射，应用程序需要指定 SQL_C_DEFAULT 类型标识符。 但出于互操作性原因，不建议使用此标识符。  
  
 ODBC 1.x 中定义的所有整数 C 数据类型*均已签名*。 ODBC 2.0 中添加了未签名的 C 数据类型及其对应的类型标识符。 因此，*在处理1.x 版本时*，应用程序和驱动程序需要特别小心。  
  
## <a name="c-data-type-extensibility"></a>C 数据类型扩展性  
 在 ODBC 3.8 中，可以指定特定于驱动程序的 C 数据类型。 这使您可以在调用[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)、 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)或[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)时，将 SQL 类型绑定为 ODBC 应用程序中的特定于驱动程序的 C 类型。 这对于支持新服务器类型可能很有用，因为现有 C 数据类型可能无法正确表示新的服务器数据类型。 使用驱动程序特定的 C 类型可以增加驱动程序可执行的转换数。  
  
 例如，假设某个数据库管理系统（DBMS）引入了新的 SQL 类型**DATETIMEOFFSET**，用来表示时区信息的日期和时间。 ODBC 中没有对应到**DATETIMEOFFSET**的特定 C 类型。 应用程序必须将**DATETIMEOFFSET**绑定为 SQL_C_BINARY，并将其转换为用户定义的数据类型。 从具有 C 数据类型扩展性的 ODBC 3.8 开始，驱动程序可定义新的相应 C 类型。 例如，对于新的 SQL 类型 DATETIMEOFFSET，驱动程序可定义新的相应 C 类型，如 SQL_C_DATETIMEOFFSET。 然后，应用程序可以将新的 SQL 类型绑定为驱动程序特定的 C 类型。  
  
 C 数据类型在驱动程序中定义，如下所示：  
  
-   应用程序、ODBC 驱动程序和驱动程序管理器的 ODBC 符合性级别为3.8 （或更高版本）。  
  
-   驱动程序特定的 C 类型的数据范围介于0x4000 和0x7FFF 之间。  
  
-   驱动程序定义对应于 C 类型的数据的结构。  这可以在特定于驱动程序的 SDK 中完成。  
  
 驱动程序管理器不会验证在0x4000 和0x7FFF 范围内定义的 C 类型。驱动程序将执行验证和任何数据类型转换。 但如果传递到驱动程序管理器的 C 类型的数据范围介于0x0000 和0x3FFF 之间，或者介于0x8000 和0xFFFF 之间，驱动程序管理器将验证 C 数据类型。  
  
> [!NOTE]  
>  驱动程序特定的 C 数据类型应在驱动程序文档中介绍。  
  
 若要指定 ODBC 符合性级别3.8，应用程序将调用[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md) ，并将 SQL_ATTR_ODBC_VERSION 特性设置为**SQL_OV_ODBC3_80**。 若要确定驱动程序的版本，应用程序需要使用 SQL_DRIVER_ODBC_VER 调用**SQLGetInfo** 。  
  
 有关 ODBC 3.8 的详细信息，请参阅[odbc 3.8 中的新增功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)。  
  
## <a name="see-also"></a>另请参阅  
 [C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)
