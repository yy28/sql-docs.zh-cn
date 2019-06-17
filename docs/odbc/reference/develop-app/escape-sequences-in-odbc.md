---
title: ODBC 中的转义序列 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3866a45a2b55a5372769eacc0bb6b0eb1e5c088f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62942970"
---
# <a name="escape-sequences-in-odbc"></a>ODBC 中的转义序列
通常的 Dbms 实现的语言功能，例如外部联接和标量函数调用数。 但是，这些功能的语法往往是特定于 DBMS 的即使标准语法定义各种标准团体。 因此，ODBC 定义包含以下语言功能的标准语法的转义序列：  
  
-   日期、 时间、 时间戳和日期时间间隔文本  
  
-   标量函数，例如数字、 字符串和数据类型转换函数  
  
-   喜欢谓词转义字符  
  
-   外部联接  
  
-   过程调用  
  
 使用 ODBC 的转义序列是按如下所示：  
  
```  
  
(extension)  
  
```  
  
## <a name="remarks"></a>备注  
 转义序列进行识别和分析由驱动程序，它的转义序列替换为特定于 DBMS 的语法。 有关转义序列语法的详细信息，请参阅[ODBC 转义序列](../../../odbc/reference/appendixes/odbc-escape-sequences.md)附录 c： 驱动器中SQL 语法。  
  
> [!NOTE]  
>  在 ODBC 2。*x*，这是标准的转义序列语法： **-(\*供应商 (** _供应商名称_ **)，产品 (** _产品名称_ **)** _扩展_  **\*)-**  
>   
>  此语法中，除了速记形式语法定义的窗体： **{** _扩展_ **}**  
>   
>  在 ODBC 3。*x*、 转义序列的长格式已被弃用，并以独占方式使用的简写形式。  
  
 转义序列映射到特定于 DBMS 的语法的驱动程序，因为应用程序可以使用的转义序列或特定于 DBMS 的语法。 但是，应用程序使用特定于 DBMS 的语法不是可互操作。 当使用转义序列时，应用程序应确保，SQL_ATTR_NOSCAN 语句属性处于关闭状态，它是默认情况下。 否则，转义序列将直接发送到数据源，其中它通常会导致语法错误。  
  
 驱动程序支持仅这些转义序列，它们可以映射到基础语言功能。 例如，如果数据源不支持外部联接，既不将驱动程序。 若要确定支持的转义序列，应用程序调用**SQLGetTypeInfo**并**SQLGetInfo**。 有关详细信息，请参阅下一部分中，[日期、 时间和时间戳文本](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)。  
  
 本部分包含以下主题。  
  
-   [日期、时间和时间戳文本](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)  
  
-   [标量函数调用](../../../odbc/reference/develop-app/scalar-function-calls.md)  
  
-   [LIKE 谓词转义字符](../../../odbc/reference/develop-app/like-predicate-escape-character.md)  
  
-   [外部联接](../../../odbc/reference/develop-app/outer-joins.md)  
  
-   [过程调用](../../../odbc/reference/develop-app/procedure-calls.md)
