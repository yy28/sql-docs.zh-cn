---
title: "附录 e： 标量函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL-92 functions [ODBC]
- scalar functions [ODBC]
- functions [ODBC], scalar
ms.assetid: 59c7cd5e-32d6-43ab-bac3-7010322d105a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: aaa110a6a62ca91535e790a267ef714675719bf4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="appendix-e-scalar-functions"></a>附录 e： 标量函数
ODBC 指定以下类型的标量函数，有关上述每种函数类型，在此附录的相应章节中提供的详细信息。 函数说明中包含相关联的语法。  
  
 本附录包含以下主题。  
  
-   [字符串函数](../../../odbc/reference/appendixes/string-functions.md)  
  
-   [数值函数](../../../odbc/reference/appendixes/numeric-functions.md)  
  
-   [时间、 日期和时间间隔函数](../../../odbc/reference/appendixes/time-date-and-interval-functions.md)  
  
-   [系统函数](../../../odbc/reference/appendixes/system-functions.md)  
  
-   [显式数据类型转换函数](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)  
  
-   [SQL 92 CAST 函数](../../../odbc/reference/appendixes/sql-92-cast-function.md)  
  
 因为函数通常是数据源 – 特定 ODBC 不强制返回值的数据类型要求从标量函数。 应用程序应使用 CONVERT 标量函数，只要有可能，以强制数据类型转换。  
  
## <a name="odbc-and-sql-92-scalar-functions"></a>ODBC 和 SQL 92 标量函数  
 本附录中的表包含 ODBC 3.0 为了符合 SQL 92 已添加的函数。 ODBC 中定义为特定类型的标量函数，添加这些函数会显示在每个部分。  
  
 ODBC 和 SQL 92 分类其标量函数以不同的方式。 ODBC 将分类自变量类型; 标量的函数SQL 92 对它们进行分类的返回值。 例如，EXTRACT 函数归类为 timedate 函数通过 ODBC，因为提取字段自变量是一个 datetime 关键字，提取源参数是日期时间或间隔的表达式。 Sql-92，另一方面，将提取分类为数值的标量函数，因为返回值是一个数字。  
  
 应用程序可以确定驱动程序还支持通过调用哪些标量函数**SQLGetInfo**。 信息类型是包含对于 ODBC 和标量函数的 SQL 92 分类。 因为这些分类不同，对于某些标量函数的支持可能会指出与 ODBC 和 SQL 92 并不对应的信息类型中。 SQL_TIMEDATE_FUNCTIONS 信息类型; 例如，指示用于 ODBC 中提取的支持另一方面，用于提取在 sql-92，支持由 SQL_SQL92_NUMERIC_VALUE_FUNCTIONS 信息类型表示。

