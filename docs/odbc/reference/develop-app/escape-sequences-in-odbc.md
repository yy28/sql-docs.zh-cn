---
title: ODBC 中的转义序列 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC]
- SQL statements [ODBC], escape sequences
- escape sequences [ODBC], about escape sequences
ms.assetid: cf229f21-6c38-4b5b-aca8-f1be0dfeb3d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4d41b0c03ecbe6de63cba1a28a1f39f12a42dc86
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300417"
---
# <a name="escape-sequences-in-odbc"></a>ODBC 中的转义序列
许多语言功能（如外部联接和标量函数调用）通常由 DBMS 实现。 但是，这些功能的语法往往特定于 DBMS，即使标准语法由各种标准机构定义也是如此。 因此，ODBC 定义了包含以下语言功能的标准语法的转义序列：  
  
-   日期、时间、时间戳和日期时间间隔文本  
  
-   标量函数，如数字、字符串和数据类型转换函数  
  
-   喜欢谓词转义字符  
  
-   外部联接  
  
-   过程调用  
  
 ODBC 使用的转义序列如下所示：  
  
```  
  
(extension)  
  
```  
  
## <a name="remarks"></a>备注  
 转义序列由驱动程序识别和解析，这些驱动程序将转义序列替换为特定于 DBMS 的语法。 有关转义序列语法的详细信息，请参阅附录 C 中的[ODBC 转义序列](../../../odbc/reference/appendixes/odbc-escape-sequences.md)：SQL 语法。  
  
> [!NOTE]  
>  在 ODBC 2 中。*x*，这是转义序列的标准语法： **-- （\*供应商（供应商**_名称_**），产品（**_产品名称_**）**_扩展_**\*） --**  
>   
>  除了此语法之外，还定义了窗体的速记语法： {**扩展**_extension_**}**  
>   
>  在 ODBC 3 中。*x*，转义序列的长形式已被弃用，速记形式被专门使用。  
  
 由于转义序列由驱动程序映射到特定于 DBMS 的语法，因此应用程序可以使用转义序列或特定于 DBMS 的语法。 但是，使用特定于 DBMS 的语法的应用程序将不可互操作。 使用转义序列时，应用程序应确保SQL_ATTR_NOSCAN语句属性已关闭，默认情况下，该属性是关闭的。 否则，转义序列将直接发送到数据源，它通常会导致语法错误。  
  
 驱动程序仅支持可以映射到基础语言要素的转义序列。 例如，如果数据源不支持外部联接，则驱动程序也不会。 要确定哪些转义序列受支持，应用程序调用**SQLGetTypeInfo**和**SQLGetInfo**。 有关详细信息，请参阅下一节"[日期、时间和时间戳文本](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)"。  
  
 本部分包含以下主题。  
  
-   [日期、时间和时间戳文本](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)  
  
-   [标量函数调用](../../../odbc/reference/develop-app/scalar-function-calls.md)  
  
-   [LIKE 谓词转义字符](../../../odbc/reference/develop-app/like-predicate-escape-character.md)  
  
-   [外部联接](../../../odbc/reference/develop-app/outer-joins.md)  
  
-   [过程调用](../../../odbc/reference/develop-app/procedure-calls.md)
