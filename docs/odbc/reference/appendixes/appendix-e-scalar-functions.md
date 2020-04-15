---
title: 附录 E： Scalar 功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL-92 functions [ODBC]
- scalar functions [ODBC]
- functions [ODBC], scalar
ms.assetid: 59c7cd5e-32d6-43ab-bac3-7010322d105a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ea354a7f882bd1a75c5f16fb19350d69ca11d375
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292487"
---
# <a name="appendix-e-scalar-functions"></a>附录 E：标量函数
ODBC 指定以下类型的标量函数，并详细介绍了本附录相应部分中提供的每种函数类型。 函数描述包括关联的语法。  
  
 本附录包含以下主题。  
  
-   [字符串函数](../../../odbc/reference/appendixes/string-functions.md)  
  
-   [数字函数](../../../odbc/reference/appendixes/numeric-functions.md)  
  
-   [时间、日期和时间间隔函数](../../../odbc/reference/appendixes/time-date-and-interval-functions.md)  
  
-   [系统功能](../../../odbc/reference/appendixes/system-functions.md)  
  
-   [显式数据类型转换函数](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)  
  
-   [SQL-92 CAST 函数](../../../odbc/reference/appendixes/sql-92-cast-function.md)  
  
 ODBC 不强制使用类型来获取标量函数的返回值，因为这些函数通常是特定于数据源的。 应用程序应尽可能使用 CONVERT 标量函数来强制转换数据类型。  
  
## <a name="odbc-and-sql-92-scalar-functions"></a>ODBC 和 SQL-92 Scalar 函数  
 本附录中的表包括已在 ODBC 3.0 中添加的函数，以便与 SQL-92 对齐。 为特定类型的标量函数添加的函数（如 ODBC 中定义）在每个部分都表示。  
  
 ODBC 和 SQL-92 对其标量函数分类不同。 ODBC 按参数类型对标量函数进行分类;SQL-92 按返回值对其进行分类。 例如，EXTRACT 函数被 ODBC 分类为时间日期函数，因为提取字段参数是日期时间关键字，并且提取源参数是日期时间或间隔表达式。 另一方面，SQL-92 将 EXTRACT 分类为数字标量函数，因为返回值是一个数字。  
  
 应用程序可以通过调用**SQLGetInfo**来确定驱动程序支持哪些标量函数。 对于 ODBC 和标量函数的 SQL-92 分类，都包含信息类型。 由于这些分类不同，因此某些标量函数的支持可能以与 ODBC 和 SQL-92 不对应的信息类型指示。 例如，ODBC 中对 EXTRACT 的支持由SQL_TIMEDATE_FUNCTIONS信息类型指示;另一方面，SQL-92 中对 EXTRACT 的支持由SQL_SQL92_NUMERIC_VALUE_FUNCTIONS信息类型指示。
