---
title: ODBC 中的 C 数据类型 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306292"
---
# <a name="c-data-types-in-odbc"></a>ODBC 中的 C 数据类型
ODBC 定义应用程序变量及其相应的类型标识符使用的 C 数据类型。 这些由绑定到结果集列和语句参数的缓冲区使用。 例如，假设应用程序希望以字符格式从结果集列检索数据。 它声明具有 SQLCHAR + 数据类型的变量，并将此变量绑定到具有SQL_C_CHAR类型标识符的结果集列。 有关 C 数据类型和类型标识符的完整列表，请参阅附录[D：数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 ODBC 还定义从每个 SQL 数据类型到 C 数据类型的默认映射。 例如，数据源中的 2 字节整数映射到应用程序中的 2 字节整数。 要使用默认映射，应用程序指定SQL_C_DEFAULT类型标识符。 但是，出于互操作性的原因，不鼓励使用此标识符。  
  
 在 ODBC *1.x*中定义的所有整数 C 数据类型都进行了签名。 在 ODBC 2.0 中添加了未签名的 C 数据类型及其相应的类型标识符。 因此，在处理*1.x*版本时，应用程序和驱动程序需要特别小心。  
  
## <a name="c-data-type-extensibility"></a>C 数据类型扩展性  
 在 ODBC 3.8 中，您可以指定特定于驱动程序的 C 数据类型。 这使您能够在调用[SQLBindCol、SQLGetData](../../../odbc/reference/syntax/sqlbindcol-function.md)或[SQLBind参数](../../../odbc/reference/syntax/sqlbindparameter-function.md)时，在 ODBC[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)应用程序中将 SQL 类型绑定为特定于驱动程序的 C 类型。 这对于支持新的服务器类型非常有用，因为现有的 C 数据类型可能无法正确表示新的服务器数据类型。 使用特定于驱动程序的 C 类型可以增加驱动程序可以执行的转换次数。  
  
 例如，假设数据库管理系统 （DBMS） 引入了新的 SQL 类型**DATETIMEOFFSET，** 以表示具有时区信息的日期和时间。 ODBC 中没有与**DATETIMEOFFSET**相对应的特定 C 类型。 应用程序必须将**DATETIMEOFFSET**绑定为SQL_C_BINARY并将其转换为用户定义的数据类型。 从具有 C 数据类型扩展性的 ODBC 3.8 开始，驱动程序可以定义新的对应 C 类型。 例如，对于新的 SQL 类型 DATETIMEOFFSET，驱动程序可以定义新的对应 C 类型，如SQL_C_DATETIMEOFFSET。 然后，应用程序可以将新的 SQL 类型绑定为特定于驱动程序的 C 类型。  
  
 在驱动程序中定义 C 数据类型，如下所示：  
  
-   应用程序、ODBC 驱动程序和驱动程序管理器的 ODBC 合规性级别为 3.8（或更高）。  
  
-   特定于驱动程序的 C 类型的数据范围介于 0x4000 和 0x7FFF 之间。  
  
-   驱动程序定义与 C 类型对应的数据的结构。  这可以在特定于驱动程序的 SDK 中完成。  
  
 驱动程序管理器不会验证在 0x4000 和 0x7FFF 范围内定义的 C 类型;因此，驱动程序管理器将验证在 0x4000 和 0x7FFF 范围内定义的 C 类型。驱动程序将执行验证和任何数据类型转换。 但是，如果传递给驱动程序管理器的 C 类型的数据范围介于 0x0000 和 0x3FFF 之间或介于 0x8000 和 0xFFFF 之间，则驱动程序管理器将验证 C 数据类型。  
  
> [!NOTE]  
>  驱动程序文档中应描述特定于驱动程序的 C 数据类型。  
  
 要指定 ODBC 合规性级别 3.8，应用程序调用[SQLSetEnvAttr，SQL_ATTR_ODBC_VERSION](../../../odbc/reference/syntax/sqlsetenvattr-function.md)属性设置为**SQL_OV_ODBC3_80**。 要确定驱动程序的版本，应用程序使用SQL_DRIVER_ODBC_VER调用**SQLGetInfo。**  
  
 有关 ODBC 3.8 的详细信息，请参阅[ODBC 3.8 中的新增功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)。  
  
## <a name="see-also"></a>另请参阅  
 [C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)
