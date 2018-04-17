---
title: Datetime 数据类型更改 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- time data type [ODBC]
- datetime data types [ODBC]
- date data type [ODBC]
- backward compatibility [ODBC], datetime data types
- timestamp data type [ODBC]
- compatibility [ODBC], datetime data types
ms.assetid: c38c79f9-8bb0-4633-ac86-542366c09a95
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a2033cd5931278c9a05c62d907d7da73473902e8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="datetime-data-type-changes"></a>Datetime 数据类型更改
在 ODBC 3。*x*、 标识符的日期、 时间和时间戳 SQL 数据类型已更改从 SQL_DATE、 SQL_TIME 和 SQL_TIMESTAMP (的实例，并用**#define** 9、 10 和 11 的标头文件中) 到 SQL_TYPE_DATE，SQL_TYPE_TIME 和 SQL_TYPE_TIMESTAMP (的实例，并用**#define** 91、 92 和 93 的标头文件中)，分别。 相应的 C 类型标识符已更改从 SQL_C_DATE、 SQL_C_TIME 和 SQL_C_TIMESTAMP 为 SQL_C_TYPE_DATE、 SQL_C_TYPE_TIME 和 SQL_C_TYPE_TIMESTAMP，分别。  
  
 列大小和 ODBC 3 中的 SQL datetime 数据类型为返回的十进制数字。*x*是否精度和小数位数相同在 ODBC 2 中为其返回。*x*。 这些值是不同于 SQL_DESC_PRECISION 和 SQL_DESC_SCALE 描述符字段中的值。 (有关详细信息，请参阅[列大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。)  
  
 这些更改会影响**SQLDescribeCol**， **SQLDescribeParam**，和**SQLColAttribute**;**SQLBindCol**， **SQLBindParameter**，和**SQLGetData**; 和**SQLColumns**， **SQLGetTypeInfo**， **SQLProcedureColumns**， **SQLStatistics**，和**SQLSpecialColumns**。  
  
 下表显示如何 ODBC 3*.x*驱动程序管理器执行的输入中的日期、 时间和时间戳 C 数据类型映射*TargetType*的自变量**SQLBindCol**和**SQLGetData**或*ValueType*参数**SQLBindParameter**。  
  
|数据类型<br /><br /> 输入代码|2.*x*应用<br /><br /> 2.*x*驱动程序|2.*x*应用<br /><br /> 3.*x*驱动程序|3.*x*应用<br /><br /> 2.*x*驱动程序|3.*x*应用<br /><br /> 3.*x*驱动程序|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_C_DATE (9)|没有映射|SQL_C_TYPE_DATE (91)|没有映射 [1]|SQL_C_TYPE_DATE (91)|  
|SQL_C_TYPE_DATE (91)|错误 （从数据挖掘）|错误 （从数据挖掘）|SQL_C_DATE (9)|[2] 没有映射|  
|SQL_C_TIME (10)|没有映射|SQL_C_TYPE_TIME (92)|没有映射 [1]|SQL_C_TYPE_TIME (92)|  
|SQL_C_TYPE_TIME (92)|错误 （从数据挖掘）|错误 （从数据挖掘）|SQL_C_TIME (10)|[2] 没有映射|  
|SQL_C_TIMESTAMP (11)|没有映射|SQL_C_TYPE_TIMESTAMP (93)|没有映射 [1]|SQL_C_TYPE_TIMESTAMP (93)|  
|SQL_C_TYPE_TIMESTAMP (93)|错误 （从数据挖掘）|错误 （从数据挖掘）|SQL_C_TIMESTAMP (11)|[2] 没有映射|  
  
 [1] 为此，ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序可以使用目录函数返回的结果集中返回的日期、 时间戳代码。  
  
 [2] 为此，ODBC 3。*x*应用程序使用 ODBC 3。*x*驱动程序可以使用目录函数返回的结果集中返回的日期、 时间戳代码。  
  
 下表显示如何 ODBC 3*.x*驱动程序管理器执行的输入中的日期、 时间和时间戳 SQL 数据类型映射*ParameterType*参数**SQLBindParameter**或*DataType*参数**SQLGetTypeInfo**。  
  
|数据类型<br /><br /> 输入代码|2.*x*应用<br /><br /> 2.*x*驱动程序|2.*x*应用<br /><br /> 3.*x*驱动程序|3.*x*应用<br /><br /> 2.*x*驱动程序|3.*x*应用<br /><br /> 3.*x*驱动程序|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_DATE (9)|没有映射|SQL_TYPE_DATE (91)|没有映射 [1]|SQL_TYPE_DATE (91)|  
|SQL_TYPE_DATE (91)|错误 （从数据挖掘）|错误 （从数据挖掘）|SQL_DATE (9)|[2] 没有映射|  
|SQL_TIME (10)|没有映射|SQL_TYPE_TIME (92)|没有映射 [1]|SQL_TYPE_TIME (92)|  
|SQL_TYPE_TIME (92)|错误 （从数据挖掘）|错误 （从数据挖掘）|SQL_TIME (10)|[2] 没有映射|  
|SQL_TIMESTAMP (11)|没有映射|SQL_TYPE_TIMESTAMP (93)|没有映射 [1]|SQL_TYPE_TIMESTAMP (93)|  
|SQL_TYPE_TIMESTAMP (93)|错误 （从数据挖掘）|错误 （从数据挖掘）|SQL_TIMESTAMP (11)|[2] 没有映射|  
  
 [1] 为此，ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序可以使用目录函数返回的结果集中返回的日期、 时间戳代码。  
  
 [2] 为此，ODBC 3。*x*应用程序使用 ODBC 3。*x*驱动程序可以使用目录函数返回的结果集中返回的日期、 时间戳代码。
