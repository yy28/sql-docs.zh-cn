---
title: 日期时间数据类型 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 10626c4f0bf2e33c70322a0eb49af6c3e01e4303
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307058"
---
# <a name="datetime-data-types"></a>日期时间数据类型
在 ODBC *3.x*中，日期、时间和时间戳 SQL 数据类型的标识符分别从 SQL_DATE、SQL_TIME和SQL_TIMESTAMP（标头文件中的 **#define**实例为 9、10 和 11），更改为SQL_TYPE_DATE、SQL_TYPE_TIME和SQL_TYPE_TIMESTAMP（标头文件中的 **#define**实例为 91、92 和 93）。 相应的 C 类型标识符分别从SQL_C_DATE、SQL_C_TIME和SQL_C_TIMESTAMP更改为SQL_C_TYPE_DATE、SQL_C_TYPE_TIME 和**SQL_C_TYPE_TIMESTAMP，#define**实例也相应更改。  
  
 为 ODBC *3.x*中为 SQL 约会时间数据类型返回的列大小和十进制数字与在 ODBC *2.x*中为其返回的精度和比例相同。 这些值与SQL_DESC_PRECISION和SQL_DESC_SCALE描述符字段中的值不同。 （有关详细信息，请参阅附录 D 中的[列大小、十进制数字、传输八字长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)：数据类型。  
  
 这些更改会影响**SQL 描述科尔****、SQL 描述参数**和**SQLColattributes;****SQLBindCol、SQLBind****参数**和**SQLGetData;** 和**SQL 列****、SQLGetTypeInfo、SQL****程序列****、SQL统计**和**SQL 特殊列**。  
  
 ODBC *3.x*驱动程序根据SQL_ATTR_ODBC_VERSION环境属性的设置处理上一段中列出的函数调用。 对于**SQLColumns、SQLGetTypeInfo、SQL****程序列****、SQL特别列**和**SQLStatistics，** 如果SQL_ATTR_ODBC_VERSION设置为SQL_OV_ODBC3，则函数返回DATA_TYPE字段中SQL_TYPE_DATE、SQL_TYPE_TIME和SQL_TYPE_TIMESTAMP。 **SQLColumns** COLUMN_SIZE列（在**SQLColumn、SQLGetTypeInfo、SQL****程序列**和**SQL 特别列**返回的结果集中）包含近似数值类型的二进制精度。 **SQLColumns** NUM_PREC_RADIX列（在**SQLColumn、SQLGetTypeInfo**和**SQLColumns****SQL过程列**返回的结果集中）包含值 2。 如果SQL_ATTR_ODBC_VERSION设置为SQL_OV_ODBC2，则函数返回DATA_TYPE字段中的SQL_DATE、SQL_TIME和SQL_TIMESTAMP，则COLUMN_SIZE列包含近似数值类型的十进制精度，NUM_PREC_RADIX列包含值 10。  
  
 当在调用**SQLGetTypeInfo**时请求所有数据类型时，函数返回的结果集将包含 ODBC *3.x*中定义的SQL_TYPE_DATE、SQL_TYPE_TIME和SQL_TYPE_TIMESTAMP，以及 ODBC *2.x*中定义的SQL_DATE、SQL_TIME和SQL_TIMESTAMP。  
  
 由于 ODBC *3.x*驱动程序管理器如何对日期、时间和时间戳数据类型进行映射， ODBC *3.x*驱动程序只需要识别**SQLBindCol**和**SQLGetData** *的 TargetType*参数或**SQLBind参数***的值类型*参数中输入的日期、时间和时间戳 C 数据类型 **#defines** 91、92 和 93，并且只需识别**在 SQLBind 参数***参数*或数据*类型*参数中输入的日期、时间和时间戳**SQL**数据类型 **#defines** 91、92 和 93。 有关详细信息，请参阅[日期时间数据类型更改](../../../odbc/reference/develop-app/datetime-data-type-changes.md)。
