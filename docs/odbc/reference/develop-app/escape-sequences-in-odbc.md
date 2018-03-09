---
title: "转义序列中 ODBC |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- escape sequences [ODBC]
- SQL statements [ODBC], escape sequences
- escape sequences [ODBC], about escape sequences
ms.assetid: cf229f21-6c38-4b5b-aca8-f1be0dfeb3d0
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 72884da8498b5e0ccb3533c353e676dee2517795
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="escape-sequences-in-odbc"></a>ODBC 中的转义序列
大量的语言功能，如外部联接和标量函数调用，通常被实现的 Dbms。 但是，为这些功能语法往往是特定于 DBMS 的即使标准语法定义的各种标准正文。 因此，ODBC 定义包含以下语言功能的标准语法的转义序列：  
  
-   日期、 时间、 时间戳，和日期时间间隔文本  
  
-   标量函数，例如数字、 字符串和数据类型转换函数  
  
-   如谓词转义字符  
  
-   外部联接  
  
-   过程调用  
  
 使用 ODBC 的转义序列如下所示：  
  
```  
  
(extension)  
  
```  
  
## <a name="remarks"></a>Remarks  
 转义序列是识别，并且由驱动程序，将替换为特定于 DBMS 的语法的转义序列进行分析。 有关转义序列语法的详细信息，请参阅[ODBC 转义序列](../../../odbc/reference/appendixes/odbc-escape-sequences.md)附录 c: SQL 语法中。  
  
> [!NOTE]  
>  在 ODBC 2。*x*，这是标准语法的转义序列： **-(\*供应商 (***供应商名称***)，产品 (** *产品名称***)***扩展*  **\*)-**  
>   
>  此语法中，除了速记形式语法已定义的窗体： **{***扩展***}**  
>   
>  在 ODBC 3。*x*，已弃用此转义序列的长格式，且以独占方式使用速记形式。  
  
 因为转义序列被映射到特定于 DBMS 的语法驱动程序，应用程序可以使用转义序列或特定于 DBMS 的语法。 但是，应用程序使用特定于 DBMS 的语法将不是可互操作。 在使用转义序列时，应用程序应确保，SQL_ATTR_NOSCAN 语句关闭属性，它本来就是默认情况下。 否则，此转义序列将直接发送至数据源，其中它将通常导致语法错误。  
  
 驱动程序支持仅这些转义序列，它们可以将映射到基础语言功能。 例如，如果数据源不支持外部联接，两者将驱动程序。 若要确定支持哪些转义序列，应用程序调用**SQLGetTypeInfo**和**SQLGetInfo**。 有关详细信息，请参阅下一部分中，[日期、 时间和时间戳文本](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)。  
  
 本部分包含以下主题。  
  
-   [日期、时间和时间戳文本](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)  
  
-   [标量函数调用](../../../odbc/reference/develop-app/scalar-function-calls.md)  
  
-   [LIKE 谓词转义字符](../../../odbc/reference/develop-app/like-predicate-escape-character.md)  
  
-   [外部联接](../../../odbc/reference/develop-app/outer-joins.md)  
  
-   [过程调用](../../../odbc/reference/develop-app/procedure-calls.md)
