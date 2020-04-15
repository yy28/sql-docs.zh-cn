---
title: 日期时间数据类型更改 |微软文档
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
- backward compatibility [ODBC], datetime data types
- timestamp data type [ODBC]
- compatibility [ODBC], datetime data types
ms.assetid: c38c79f9-8bb0-4633-ac86-542366c09a95
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4f186047dd31aa2c4b66ec1ce73c8cb9fae31c04
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304640"
---
# <a name="datetime-data-type-changes"></a>Datetime 数据类型更改
在 ODBC *3.x*中，日期、时间和时间戳 SQL 数据类型的标识符分别从 SQL_DATE、SQL_TIME和SQL_TIMESTAMP（标头文件中的 **#define**实例为 9、10 和 11），更改为SQL_TYPE_DATE、SQL_TYPE_TIME和SQL_TYPE_TIMESTAMP（标头文件中的 **#define**实例为 91、92 和 93）。 相应的 C 类型标识符分别从SQL_C_DATE、SQL_C_TIME 和SQL_C_TIMESTAMP更改为SQL_C_TYPE_DATE、SQL_C_TYPE_TIME 和SQL_C_TYPE_TIMESTAMP。  
  
 为 ODBC *3.x*中为 SQL 约会时间数据类型返回的列大小和十进制数字与在 ODBC *2.x*中为其返回的精度和比例相同。 这些值与SQL_DESC_PRECISION和SQL_DESC_SCALE描述符字段中的值不同。 （有关详细信息，请参阅[列大小、十进制数字、传输八点长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
 这些更改会影响**SQL 描述科尔****、SQL 描述Param**和**SQLColattribute;****SQLBindCol、SQLBind****参数**和**SQLGetData;** 和**SQL 列****、SQLGetTypeInfo、SQL****程序列****、SQL统计**和**SQL 特殊列**。  
  
 下表显示了 ODBC *3.x*驱动程序管理器如何对**SQLBindCol**和**SQLGetData** *的 TargetType*参数或**SQLBind参数***的值类型*参数中输入的日期、时间和时间戳 C 数据类型进行映射。  
  
|数据类型<br /><br /> 输入的代码|*2.x*应用程序到<br /><br /> *2.x*驱动程序|*2.x*应用程序到<br /><br /> *3.x*驱动程序|*3.x*应用程序到<br /><br /> *2.x*驱动程序|*3.x*应用程序到<br /><br /> *3.x*驱动程序|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_C_DATE （9）|无映射|SQL_C_TYPE_DATE （91）|无映射[1]|SQL_C_TYPE_DATE （91）|  
|SQL_C_TYPE_DATE （91）|错误（来自 DM）|错误（来自 DM）|SQL_C_DATE （9）|无映射[2]|  
|SQL_C_TIME （10）|无映射|SQL_C_TYPE_TIME （92）|无映射[1]|SQL_C_TYPE_TIME （92）|  
|SQL_C_TYPE_TIME （92）|错误（来自 DM）|错误（来自 DM）|SQL_C_TIME （10）|无映射[2]|  
|SQL_C_TIMESTAMP （11）|无映射|SQL_C_TYPE_TIMESTAMP （93）|无映射[1]|SQL_C_TYPE_TIMESTAMP （93）|  
|SQL_C_TYPE_TIMESTAMP （93）|错误（来自 DM）|错误（来自 DM）|SQL_C_TIMESTAMP （11）|无映射[2]|  
  
 [1] 因此，使用 ODBC *2.x*驱动程序的 ODBC *3.x*应用程序可以使用目录函数返回的结果集中返回的日期、时间或时间戳代码。  
  
 [2] 因此，使用 ODBC *3.x*驱动程序的 ODBC *3.x*应用程序可以使用目录函数返回的结果集中返回的日期、时间或时间戳代码。  
  
 下表显示了 ODBC *3.x*驱动程序管理器如何对**SQLBind 参数**的*参数类型*参数或**SQLGetTypeInfo**的*数据类型*参数中输入的日期、时间和时间戳 SQL 数据类型进行映射。  
  
|数据类型<br /><br /> 输入的代码|*2.x*应用程序到<br /><br /> *2.x*驱动程序|*2.x*应用程序到<br /><br /> *3.x*驱动程序|*3.x*应用程序到<br /><br /> *2.x*驱动程序|*3.x*应用程序到<br /><br /> *3.x*驱动程序|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_DATE （9）|无映射|SQL_TYPE_DATE (91)|无映射[1]|SQL_TYPE_DATE (91)|  
|SQL_TYPE_DATE (91)|错误（来自 DM）|错误（来自 DM）|SQL_DATE （9）|无映射[2]|  
|SQL_TIME （10）|无映射|SQL_TYPE_TIME （92）|无映射[1]|SQL_TYPE_TIME （92）|  
|SQL_TYPE_TIME （92）|错误（来自 DM）|错误（来自 DM）|SQL_TIME （10）|无映射[2]|  
|SQL_TIMESTAMP （11）|无映射|SQL_TYPE_TIMESTAMP (93)|无映射[1]|SQL_TYPE_TIMESTAMP (93)|  
|SQL_TYPE_TIMESTAMP (93)|错误（来自 DM）|错误（来自 DM）|SQL_TIMESTAMP （11）|无映射[2]|  
  
 [1] 因此，使用 ODBC *2.x*驱动程序的 ODBC *3.x*应用程序可以使用目录函数返回的结果集中返回的日期、时间或时间戳代码。  
  
 [2] 因此，使用 ODBC *3.x*驱动程序的 ODBC *3.x*应用程序可以使用目录函数返回的结果集中返回的日期、时间或时间戳代码。
