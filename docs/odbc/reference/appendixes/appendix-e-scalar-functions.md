---
title: 附录 E：标量函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bb5f16485312979e9fb2ad6b3a95dacb79b695d6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67996178"
---
# <a name="appendix-e-scalar-functions"></a>附录 E：标量函数
ODBC 指定以下类型的标量函数，有关每个相应部分的本附录中提供这些函数类型的详细信息。 函数说明包含关联的语法。  
  
 本附录包含的以下主题。  
  
-   [字符串函数](../../../odbc/reference/appendixes/string-functions.md)  
  
-   [数字函数](../../../odbc/reference/appendixes/numeric-functions.md)  
  
-   [时间、日期和时间间隔函数](../../../odbc/reference/appendixes/time-date-and-interval-functions.md)  
  
-   [系统函数](../../../odbc/reference/appendixes/system-functions.md)  
  
-   [显式数据类型转换函数](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)  
  
-   [SQL-92 CAST 函数](../../../odbc/reference/appendixes/sql-92-cast-function.md)  
  
 因为这些函数通常是数据源特定于 ODBC 不强制返回值的数据类型要求从标量函数。 应用程序应使用 CONVERT 标量函数，只要有可能以强制数据类型转换。  
  
## <a name="odbc-and-sql-92-scalar-functions"></a>ODBC 和 SQL-92 的标量函数  
 本附录中的表包含在 ODBC 3.0 以符合 SQL-92 中已添加的函数。 定义在 ODBC 中，添加特定类型的标量函数，这些函数是每个节中所述。  
  
 ODBC 和 SQL-92 分类及其标量函数以不同的方式。 ODBC 将分为两类标量函数的参数类型;SQL-92 进行分类的返回值。 例如，提取函数归类为 timedate 函数通过 ODBC，因为提取字段参数是 datetime 关键字并且提取源参数为 datetime 或间隔的表达式。 SQL-92，但是，将提取分类为数值的标量函数，因为返回值是数字。  
  
 应用程序可以确定驱动程序支持通过调用的标量函数**SQLGetInfo**。 ODBC 和 SQL-92 的标量函数的分类中包含的信息类型。 因为这些分类不同，可能会在不对应于 ODBC 和 SQL-92 的信息类型中指示某些标量函数的支持。 SQL_TIMEDATE_FUNCTIONS 信息类型; 例如，指示 ODBC 中提取的支持但是，支持 SQL-92 中提取 SQL_SQL92_NUMERIC_VALUE_FUNCTIONS 信息类型的指示。
