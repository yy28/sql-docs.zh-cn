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
manager: craigg
ms.openlocfilehash: 84710ffd69ea377c979adf94af1394d8436ef10b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62640465"
---
# <a name="data-type-conversions"></a>数据类型转换
数据可以从一种类型到另一个在转换一个四次： 时数据从一个应用程序变量时转移到另一个 (C 到 C)，应用程序变量中的数据发送到语句参数 (C 到 SQL) 中返回结果集列中的数据时应用程序变量 (SQL 到 C)，并当数据从一个数据源列的传输另一个 (从 SQL 到 SQL)。  
  
 超出了本文档的范围是从一个应用程序变量到另一个传输数据时，会发生任何转换。  
  
 当应用程序将变量绑定到结果集列或语句参数时，应用程序其选择的任何应用程序变量的数据类型隐式指定数据类型转换。 例如，假设某个列包含整数数据。 如果应用程序将整数变量绑定到列，它指定不完成任何转换;如果应用程序将字符变量绑定到列，它指定数据将从整数转换为字符。  
  
 ODBC 定义每个 SQL 和 C 数据类型之间转换数据的方式。 基本上，ODBC 支持所有的合理转换，例如字符到整数和浮点数的整数，不支持未正确定义的转换，例如日期浮点型。 它们支持每个 SQL 数据类型支持的所有转换所需的驱动程序。 有关 SQL 和 C 数据类型之间的转换的完整列表，请参阅[转换将数据从 SQL 到 C 数据类型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)并[转换将数据从 C 到 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)中附录 d:数据类型。  
  
 ODBC 还定义用于将数据从一个 SQL 数据类型转换为另一种标量函数。 **转换**标量函数映射到基础标量函数或函数定义为数据源中执行的转换驱动程序。 因为此函数映射到特定于 DBMS 的函数时，ODBC 不定义这些转换的工作原理或必须支持哪些转换。 应用程序发现哪些转换支持的特定驱动程序和数据源中的 SQL_CONVERT 选项通过**SQLGetInfo**。 有关详细信息**转换**标量函数，请参阅[ODBC 中的转义序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)并[显式数据类型转换函数](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)。
