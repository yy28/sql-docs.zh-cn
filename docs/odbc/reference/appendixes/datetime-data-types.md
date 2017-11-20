---
title: "Datetime 数据类型 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- time data type [ODBC]
- datetime data types [ODBC]
- date data type [ODBC]
- data types [ODBC], date
- backward compatibility [ODBC], datetime data types
- timestamp data type [ODBC]
- data types [ODBC], timestamp
- data types [ODBC], backward compatibility
- compatibility [ODBC], datetime data types
- data types [ODBC], time
ms.assetid: 6b9363c9-04bf-4492-a210-7aa15dea4af8
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 92ab5f52282fddf89c48bef73fa7817684ae3496
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="datetime-data-types"></a>Datetime 数据类型
ODBC 3 中*.x*、 标识符的日期、 时间和时间戳 SQL 数据类型已更改从 SQL_DATE、 SQL_TIME 和 SQL_TIMESTAMP (的实例，并用**#define** 9、 10 和 11 的标头文件中) 到 SQL_TYPE_DATE、 SQL_TYPE_TIME 和 SQL_TYPE_TIMESTAMP (的实例，并用**#define** 91、 92 和 93 的标头文件中)，分别。 标识符已更改从 SQL_C_DATE、 SQL_C_TIME 和 SQL_C_TIMESTAMP SQL_C_TYPE_DATE、 SQL_C_TYPE_TIME，和 SQL_C_TYPE_TIMESTAMP，分别对应 C 类型和实例的**#define**已更改相应地。  
  
 ODBC 3 中的 SQL datetime 数据类型返回的列大小和十进制数字*.x*是否精度和小数位数相同在 ODBC 2 中为其返回。*x*。 这些值是不同于 SQL_DESC_PRECISION 和 SQL_DESC_SCALE 描述符字段中的值。 (有关详细信息，请参阅[列大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附录 d： 数据类型中。)  
  
 这些更改会影响**SQLDescribeCol**， **SQLDescribeParam**，和**SQLColAttributes**;**SQLBindCol**， **SQLBindParameter**，和**SQLGetData**; 和**SQLColumns**， **SQLGetTypeInfo**， **SQLProcedureColumns**， **SQLStatistics**，和**SQLSpecialColumns**。  
  
 ODBC 3*.x*驱动程序处理根据 SQL_ATTR_ODBC_VERSION 环境属性的设置的上一个段落中列出的函数调用。 有关**SQLColumns**， **SQLGetTypeInfo**， **SQLProcedureColumns**， **SQLSpecialColumns**，和**SQLStatistics**，如果 SQL_ATTR_ODBC_VERSION 设置为 SQL_OV_ODBC3，函数将返回 SQL_TYPE_DATE、 SQL_TYPE_TIME 和 SQL_TYPE_TIMESTAMP DATA_TYPE 字段中。 COLUMN_SIZE 列 (在返回的结果集**SQLColumns**， **SQLGetTypeInfo**， **SQLProcedureColumns**，和**SQLSpecialColumns**)包含近似数值类型的二进制精度。 NUM_PREC_RADIX 列 (在返回的结果集**SQLColumns**， **SQLGetTypeInfo**，和**SQLProcedureColumns**) 包含值为 2。 如果 SQL_ATTR_ODBC_VERSION 设置为 SQL_OV_ODBC2，则函数返回 SQL_DATE、 SQL_TIME 和 SQL_TIMESTAMP DATA_TYPE 字段中，则 COLUMN_SIZE 该列包含的近似数值类型和 NUM_PREC_RADIX 列的小数精度包含值为 10。  
  
 所有数据类型对的调用中的都请求时**SQLGetTypeInfo**，由该函数返回的结果集将包含 SQL_TYPE_DATE、 SQL_TYPE_TIME 和 SQL_TYPE_TIMESTAMP ODBC 3 中定义*.x*，和 SQL_DATE、 SQL_TIME 和 SQL_TIMESTAMP ODBC 2 中定义。*x*。  
  
 由于如何 ODBC 3*.x*驱动程序管理器执行日期、 时间和时间戳数据类型映射，ODBC 3*.x*只能识别驱动程序，需要**#defines**的 91、 92，和有关日期、 时间和时间戳 C 数据类型的 93 进入*TargetType*的自变量**SQLBindCol**和**SQLGetData**或*ValueType*自变量**SQLBindParameter**，并仅需要识别**#defines**的 91，92 和 93、 日期时间、 和时间戳 SQL 数据类型进入*ParameterType*参数**SQLBindParameter**或*DataType*参数**SQLGetTypeInfo**。 有关详细信息，请参阅[Datetime 数据类型更改](../../../odbc/reference/develop-app/datetime-data-type-changes.md)。

