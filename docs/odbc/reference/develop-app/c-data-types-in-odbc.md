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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5472595383c7e4fcf448374c1fd85587246328f7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654285"
---
# <a name="c-data-types-in-odbc"></a>ODBC 中的 C 数据类型
ODBC 定义应用程序变量和其对应的类型标识符所使用的 C 数据类型。 这些使用绑定到结果集列和语句参数的缓冲区。 例如，假设应用程序想要从以字符格式的结果集列中检索数据。 它声明的变量 SQLCHAR * 数据类型，并将此变量绑定到结果集列具有其类型标识符为 SQL_C_CHAR。 C 数据类型和类型标识符的完整列表，请参阅[附录 d： 数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 ODBC 还定义从每个 SQL 数据类型为 C 数据类型的默认映射。 例如，数据源中的 2 字节整数映射到应用程序中的 2 字节整数。 若要使用的默认映射，应用程序，请指定 SQL_C_DEFAULT 类型标识符。 但是，建议不要使用此标识符的互操作性的原因。  
  
 在 ODBC 1 中定义的所有整数 C 数据类型 *.x*是否已进行签名。 ODBC 2.0 添加了无符号的 C 数据类型和其对应的类型标识符。 正因为如此，应用程序和驱动程序需要特别注意处理 1 时 *.x*版本。  
  
## <a name="c-data-type-extensibility"></a>C 数据类型扩展能力  
 在 ODBC 3.8，可以指定特定于驱动程序的 C 数据类型。 这使您可以将 SQL 类型绑定为 ODBC 应用程序中的特定于驱动程序的 C 类型，当您调用[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)， [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)，或[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)。 这可用于支持新的服务器类型，因为现有的 C 数据类型不能正确表示新的服务器数据类型。 使用特定于驱动程序的 C 类型可以提高驱动程序可以执行的转换数。  
  
 例如，假设数据库管理系统 (DBMS) 引入了新的 SQL 类型， **DATETIMEOFFSET**，用于表示的日期和时间与时区信息。 对应于 ODBC 中会有任何特定的 C 类型**DATETIMEOFFSET**。 应用程序必须将绑定**DATETIMEOFFSET** SQL_C_BINARY 和强制转换为其用户定义数据类型。 开始在 ODBC 3.8 中 C 数据类型扩展能力，驱动程序可以定义新的相应 C 类型。 例如，对于新的 SQL 类型 DATETIMEOFFSET，驱动程序可以定义如 SQL_C_DATETIMEOFFSET 对应的新 C 类型。 然后，应用程序可以将新的 SQL 类型绑定为特定于驱动程序的 C 类型。  
  
 C 数据类型定义驱动程序中，如下所示：  
  
-   应用程序、 ODBC 驱动程序和驱动程序管理器的 ODBC 符合性级别是 3.8 （或更高版本）。  
  
-   0x4000 和 0x7FFF 之间是特定于驱动程序的 C 类型的数据范围。  
  
-   该驱动程序定义的 C 类型相对应的数据的结构。  进行这种特定于驱动程序的 SDK。  
  
 驱动程序管理器将不会验证 0x4000 和 0x7FFF; 的范围中定义的 C 类型该驱动程序将执行验证和任何数据类型转换。 但如果传递给驱动程序管理器的 C 类型的数据范围之间 0x8000 和 0xFFFF 或 0x0000 和 0x3FFF 之间，驱动程序管理器将验证的 C 数据类型。  
  
> [!NOTE]  
>  特定于驱动程序的 C 数据类型应驱动程序文档中所述。  
  
 若要指定 ODBC 3.8 的符合性级别，应用程序调用[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md) SQL_ATTR_ODBC_VERSION 与属性设置为**SQL_OV_ODBC3_80**。 若要确定版本的驱动程序，应用程序调用**SQLGetInfo** SQL_DRIVER_ODBC_VER 使用。  
  
 有关 ODBC 3.8 详细信息，请参阅[What's New in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)。  
  
## <a name="see-also"></a>请参阅  
 [C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)
