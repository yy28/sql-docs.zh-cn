---
title: 数据类型转换 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], conversions
- SQL data types [ODBC], conversions
- converting data [ODBC]
- converting data types [ODBC]
- C data types [ODBC], conversions
ms.assetid: d311fe1c-d882-4136-9fa5-220a4121e04c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 590bd488ae87e8e871837c3055a3225794850d00
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68077007"
---
# <a name="data-type-conversions"></a>数据类型转换
数据可以从一种类型转换为另一种类型，这四次：将数据从一个应用程序变量转换到另一个应用程序变量（C 到 C）时，当在中返回结果集列中的数据时，将应用程序变量中的数据发送到语句参数（C 到 SQL）应用程序变量（SQL 到 C）以及将数据从一个数据源列传输到另一个数据源列（SQL to SQL）的时间。  
  
 当数据从一个应用程序变量传输到另一个应用程序变量时所发生的任何转换都超出了本文档的讨论范围。  
  
 当应用程序将变量绑定到结果集列或语句参数时，应用程序会在其选择应用程序变量的数据类型时隐式指定数据类型转换。 例如，假设某列包含整数数据。 如果应用程序将整数变量绑定到列，则它指定不进行任何转换;如果应用程序将字符变量绑定到列，则它指定将数据从整数转换为字符。  
  
 ODBC 定义了如何在每个 SQL 和 C 数据类型之间转换数据。 实质上，ODBC 支持所有合理的转换，例如字符到整数和整数到浮点的转换，并且不支持错误定义的转换（如浮动到日期）。 驱动程序需要支持其支持的每个 SQL 数据类型的所有转换。 有关 SQL 和 C 数据类型之间的转换的完整列表，请参阅附录 D：数据类型中的将[数据从 SQL 转换为 c 数据类型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)和[将数据从 C 转换为 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
 ODBC 还定义了一个用于将数据从一种 SQL 数据类型转换为另一种数据类型的标量函数。 **CONVERT**标量函数由驱动程序映射到基础标量函数或定义为在数据源中执行转换的函数。 由于此函数映射到 DBMS 特定的函数，ODBC 不会定义这些转换的工作方式或必须支持哪些转换。 应用程序通过**SQLGetInfo**中的 SQL_CONVERT 选项来发现特定驱动程序和数据源支持的转换。 有关**CONVERT**标量函数的详细信息，请参阅[ODBC 中的转义序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)和[显式数据类型转换函数](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)。
