---
description: ODBC 中的转义序列
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 62745b749870fa33151fc1a5f6bd3a1bfc344ad7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429309"
---
# <a name="escape-sequences-in-odbc"></a>ODBC 中的转义序列
许多语言功能（例如外部联接和标量函数调用）通常由 Dbms 实现。 不过，这些功能的语法通常是特定于 DBMS 的，即使标准语法由各种标准主体定义也是如此。 因此，ODBC 定义了包含以下语言功能标准语法的转义序列：  
  
-   日期、时间、时间戳和日期时间间隔文本  
  
-   标量函数，例如数字、字符串和数据类型转换函数  
  
-   LIKE 谓词转义符  
  
-   外部联接  
  
-   过程调用  
  
 ODBC 使用的转义序列如下所示：  
  
```  
  
(extension)  
  
```  
  
## <a name="remarks"></a>备注  
 驱动程序会识别和分析转义序列，驱动程序将使用特定于 DBMS 的语法替换转义序列。 有关转义序列语法的详细信息，请参阅附录 C： SQL 语法中的 [ODBC 转义序列](../../../odbc/reference/appendixes/odbc-escape-sequences.md) 。  
  
> [!NOTE]  
>  在 ODBC 2 中。*x*，这是转义序列的标准语法： **-- (\* 供应商 (**_供应商名称_**) 、产品 (**_产品名称_**) **_扩展_ ** \*) **  
>   
>  除了此语法以外，还定义了简写语法，格式为：            **{**_extension_**}**  
>   
>  ODBC 3 中的。*x*，转义序列的长格式已被弃用，并且简写形式仅用于。  
  
 由于转义序列由驱动程序映射到 DBMS 特定的语法，因此应用程序可以使用转义序列或 DBMS 特定的语法。 但是，使用特定于 DBMS 的语法的应用程序将无法互操作。 使用转义序列时，应用程序应确保已关闭 SQL_ATTR_NOSCAN 语句特性，默认情况下它是如此。 否则，转义序列将直接发送到数据源，这通常会导致语法错误。  
  
 驱动程序仅支持可映射到基础语言功能的转义序列。 例如，如果数据源不支持外部联接，则这两个驱动程序都不会。 若要确定支持的转义序列，应用程序将调用 **SQLGetTypeInfo** 和 **SQLGetInfo**。 有关详细信息，请参阅下一节、 [日期、时间和时间戳文本](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)。  
  
 本部分包含以下主题。  
  
-   [日期、时间和时间戳文本](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)  
  
-   [标量函数调用](../../../odbc/reference/develop-app/scalar-function-calls.md)  
  
-   [LIKE 谓词转义字符](../../../odbc/reference/develop-app/like-predicate-escape-character.md)  
  
-   [外部联接](../../../odbc/reference/develop-app/outer-joins.md)  
  
-   [过程调用](../../../odbc/reference/develop-app/procedure-calls.md)
