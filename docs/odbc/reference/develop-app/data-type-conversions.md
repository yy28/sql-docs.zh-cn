---
title: 数据类型转换 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cd888fe32692494e2b0ceadc1ed872dd96e244a9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305209"
---
# <a name="data-type-conversions"></a>数据类型转换
数据可以在四次之一时从一种类型转换为另一种类型：当数据从一个应用程序变量传输到另一个应用程序变量（C 到 C）、将应用程序变量中的数据发送到语句参数 （C 到 SQL）时、在应用程序变量（SQL 到 C）中返回结果集列中的数据时，以及数据从一个数据源列传输到另一个数据源列时（SQL 到 SQL）。  
  
 当数据从一个应用程序变量传输到另一个应用程序变量时发生的任何转换都不在本文档的范围之内。  
  
 当应用程序将变量绑定到结果集列或语句参数时，应用程序隐式指定数据类型转换，以选择应用程序变量的数据类型。 例如，假设列包含整数数据。 如果应用程序将整数变量绑定到列，则指定不执行任何转换;如果应用程序将整数变量绑定到列，则不执行任何转换。如果应用程序将字符变量绑定到列，则指定将数据从整数转换为字符。  
  
 ODBC 定义如何在每种 SQL 和 C 数据类型之间转换数据。 基本上，ODBC 支持所有合理的转换，例如字符到整数和整数到浮点，并且不支持定义不当的转换，如浮动至今。 需要驱动程序来支持他们支持的每个 SQL 数据类型的所有转换。 有关 SQL 和 C 数据类型之间的转换的完整列表，请参阅在附录 D：数据类型中[将数据从 SQL 转换为 C 数据类型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)以及[将数据从 C 转换为 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
 ODBC 还定义了用于将数据从一种 SQL 数据类型转换为另一种 SQL 数据类型的标量函数。 **CONVERT**标量函数由驱动程序映射到为在数据源中执行转换而定义的基础标量函数或函数。 由于此函数映射到特定于 DBMS 的函数，因此 ODBC 不定义这些转换的工作原理或必须支持哪些转换。 应用程序通过**SQLGetInfo**中的SQL_CONVERT选项发现特定驱动程序和数据源支持哪些转换。 有关**CONVERT**标量函数的详细信息，请参阅[ODBC 中的转义序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)和[显式数据类型转换函数](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)。
