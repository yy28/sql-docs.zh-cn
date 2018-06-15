---
title: 数据类型转换 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], conversions
- SQL data types [ODBC], conversions
- converting data [ODBC]
- converting data types [ODBC]
- C data types [ODBC], conversions
ms.assetid: d311fe1c-d882-4136-9fa5-220a4121e04c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0501e4bf627d8dafddfbf5020345d43135af9d6d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32911932"
---
# <a name="data-type-conversions"></a>数据类型转换
数据可以转换从一种类型到另一个在四次之一： 时数据从一个应用程序变量时转移到另一个 (C 到 C)，应用程序变量中的数据发送到语句参数 (C to SQL) 中，在返回结果集列中的数据时在应用程序变量 (SQL 到 C)，并且当数据已转让从一个数据源列给另一个 (SQL to SQL)。  
  
 当数据从一个应用程序变量传输到另一个时发生的任何转换都超出了本文档的范围。  
  
 当应用程序绑定到结果集列或语句参数的变量时，应用程序将其选择的任何应用程序变量的数据类型隐式指定的数据类型转换。 例如，假设某一列包含整数数据。 如果应用程序将一个整数变量绑定到列，它指定，进行任何转换;如果应用程序将字符变量绑定到列，它指定数据将从整数转换为字符。  
  
 ODBC 定义每个 SQL 和 C 数据类型之间转换数据的方式。 基本上，ODBC 支持所有的合理转换，例如到整数和浮点数的整数的字符，不支持未正确定义的转换，如到日期的浮点数。 它们支持每个 SQL 数据类型支持所有转换所需驱动程序。 SQL 和 C 数据类型之间的转换的完整列表，请参阅[转换数据从 SQL C 数据类型到](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)和[C 中为 SQL 数据类型的转换的数据](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)附录 d： 数据类型中。  
  
 ODBC 还定义了用于将数据从一种 SQL 数据类型转换为另一个标量函数。 **转换**标量函数映射的驱动程序添加到该基础标量函数或函数定义为数据源中执行转换。 因为此函数映射到特定于 DBMS 的功能，ODBC 不定义这些转换的工作方式，或必须支持哪些转换。 应用程序发现哪些转换支持的特定驱动程序和数据源中的 SQL_CONVERT 选项通过**SQLGetInfo**。 有关详细信息**转换**标量函数，请参阅[ODBC 中的转义序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)和[显式数据类型转换函数](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)。
