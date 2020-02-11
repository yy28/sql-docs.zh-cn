---
title: Datetime 数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1cb92afa9467717b8a589ddbcaee4ab8a5a529f6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68130094"
---
# <a name="datetime-data-types"></a>日期时间数据类型
在 ODBC *2.x 中，* 日期、时间和时间戳 SQL 数据类型的标识符已从 SQL_DATE、SQL_TIME 和 SQL_TIMESTAMP （将头文件中的 **#define**实例9、10和11）更改为 SQL_TYPE_DATE、SQL_TYPE_TIME 和 SQL_TYPE_TIMESTAMP （在91、92和93的标头文件中 **#define**的实例）。 对应的 C 类型标识符已从 SQL_C_DATE、SQL_C_TIME 和 SQL_C_TIMESTAMP 更改为 SQL_C_TYPE_DATE、SQL_C_TYPE_TIME 和 SQL_C_TYPE_TIMESTAMP，并对 **#define**的实例进行了相应的更改。  
  
 ODBC 2.x 中 SQL datetime 数据类型返回的列大小和小数位数与*odbc 2.x*中为其返回的精度和小数位数*相同。* 这些值与 "SQL_DESC_PRECISION" 和 "SQL_DESC_SCALE 描述符" 字段中的值不同。 （有关详细信息，请参阅附录 D：数据类型中的[列大小、十进制数字、传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。）  
  
 这些更改会影响**SQLDescribeCol**、 **SQLDescribeParam**和**SQLColAttributes**;**SQLBindCol**、 **SQLBindParameter**和**SQLGetData**;和**SQLColumns**、 **SQLGetTypeInfo**、 **SQLProcedureColumns**、 **SQLStatistics**和**SQLSpecialColumns**。  
  
 *ODBC 2.x*驱动程序根据 SQL_ATTR_ODBC_VERSION 环境属性的设置来处理上一段落中列出的函数调用。 对于**SQLColumns**、 **SQLGetTypeInfo**、 **SQLProcedureColumns**、 **SQLSpecialColumns**和**SQLStatistics**，如果 SQL_ATTR_ODBC_VERSION 设置为 SQL_OV_ODBC3，则这些函数将在 SQL_TYPE_TIMESTAMP 字段中返回 SQL_TYPE_DATE、SQL_TYPE_TIME 和 DATA_TYPE。 在**SQLColumns**、 **SQLGetTypeInfo**、 **SQLProcedureColumns**和**SQLSpecialColumns**返回的结果集中，COLUMN_SIZE 列包含近似数值类型的二进制精度。 在**SQLColumns**、 **SQLGetTypeInfo**和**SQLProcedureColumns**返回的结果集中，NUM_PREC_RADIX 列的值为2。 如果 SQL_ATTR_ODBC_VERSION 设置为 SQL_OV_ODBC2，则这些函数将在 SQL_TIMESTAMP 字段中返回 SQL_DATE、SQL_TIME 和 DATA_TYPE，COLUMN_SIZE 列包含近似数值类型的小数精度和 NUM_PREC_RADIX 列的值为10。  
  
 当在对**SQLGetTypeInfo**的调用中请求所有数据类型时，函数返回的结果集将*包含 odbc 2.x 中定义的 SQL_TYPE_DATE*、SQL_TYPE_TIME 和 SQL_TYPE_TIMESTAMP，以及 odbc 2.x 中定义的 SQL_DATE、SQL_TIME 和*SQL_TIMESTAMP。*  
  
 由于*ODBC 2.X*驱动程序管理器如何执行日期映射，时间和时间戳数据类型 *，ODBC 2.x*驱动程序只需识别在**SQLBindCol**和**SQLGetData**的*TargetType*参数或**SQLBindParameter**的*ValueType*参数中输入的日期、时间和时间戳 C 数据类型 **#defines** 91、92和93），并且只需识别在中输入的日期、时间和时间戳 SQL 数据类型的91、92和 93 **#defines****SQLBindParameter**的*ParameterType*参数或**SQLGetTypeInfo**的*DataType*参数。 有关详细信息，请参阅[Datetime 数据类型更改](../../../odbc/reference/develop-app/datetime-data-type-changes.md)。
