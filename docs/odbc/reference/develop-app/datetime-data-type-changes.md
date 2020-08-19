---
description: Datetime 数据类型更改
title: Datetime 数据类型更改 |Microsoft Docs
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
ms.openlocfilehash: a36339f275ff03584a3682f9f57eeeb8445faf3b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424749"
---
# <a name="datetime-data-type-changes"></a>Datetime 数据类型更改
在 ODBC *3.x 中，* 日期、时间和时间戳 SQL 数据类型的标识符已从 SQL_DATE、SQL_TIME 和 SQL_TIMESTAMP (分别更改为9、10和 11 #define 的标头文件中的 **) ** SQL_TYPE_DATE、SQL_TYPE_TIME 和 91 SQL_TYPE_TIMESTAMP (#define) 、92和 93 **#define** 对应的 C 类型标识符已分别 SQL_C_DATE、SQL_C_TIME 和 SQL_C_TIMESTAMP 更改为 SQL_C_TYPE_DATE、SQL_C_TYPE_TIME 和 SQL_C_TYPE_TIMESTAMP。  
  
 ODBC 2.x 中 SQL datetime 数据类型返回的列大小和小数位数与*odbc 2.x*中为其返回的精度和小数位数*相同。* 这些值与 "SQL_DESC_PRECISION" 和 "SQL_DESC_SCALE 描述符" 字段中的值不同。  (有关详细信息，请参阅 [列大小、十进制数字、传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。 )   
  
 这些更改会影响 **SQLDescribeCol**、 **SQLDescribeParam**和 **SQLColAttribute**; **SQLBindCol**、 **SQLBindParameter**和 **SQLGetData**;和 **SQLColumns**、 **SQLGetTypeInfo**、 **SQLProcedureColumns**、 **SQLStatistics**和 **SQLSpecialColumns**。  
  
 下表显示*了 ODBC 2.X*驱动程序管理器如何执行**SQLBindCol**和**SQLGetData**的*TargetType*参数或**SQLBindParameter**的*ValueType*参数中输入的日期、时间和时间戳 C 数据类型的映射。  
  
|数据类型<br /><br /> 已输入代码|*2. x* 应用程序到<br /><br /> 2.x*驱动程序*|*2. x* 应用程序到<br /><br /> 3.x*驱动程序*|*3. x* 应用程序到<br /><br /> 2.x*驱动程序*|*3. x* 应用程序到<br /><br /> 3.x*驱动程序*|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_C_DATE (9) |无映射|SQL_C_TYPE_DATE (91) |无映射 [1]|SQL_C_TYPE_DATE (91) |  
|SQL_C_TYPE_DATE (91) |DM)  (错误|DM)  (错误|SQL_C_DATE (9) |无映射 [2]|  
|SQL_C_TIME (10) |无映射|SQL_C_TYPE_TIME (92) |无映射 [1]|SQL_C_TYPE_TIME (92) |  
|SQL_C_TYPE_TIME (92) |DM)  (错误|DM)  (错误|SQL_C_TIME (10) |无映射 [2]|  
|SQL_C_TIMESTAMP (11) |无映射|SQL_C_TYPE_TIMESTAMP (93) |无映射 [1]|SQL_C_TYPE_TIMESTAMP (93) |  
|SQL_C_TYPE_TIMESTAMP (93) |DM)  (错误|DM)  (错误|SQL_C_TIMESTAMP (11) |无映射 [2]|  
  
 [1] 这样做的结果是，*使用 odbc 2.x* *驱动程序的 odbc 1.x 应用程序*可以使用目录函数返回的结果集中返回的日期、时间或时间戳代码。  
  
 [2] 因此，*使用 odbc 1.x* *驱动程序的 odbc 1.x 应用程序*可以使用目录函数返回的结果集中返回的日期、时间或时间戳代码。  
  
 下表显示*了 ODBC 2.X*驱动程序管理器如何执行在**SQLBindParameter**的*ParameterType*参数中或在**SQLGetTypeInfo**的*DataType*参数中输入的日期、时间和时间戳 SQL 数据类型的映射。  
  
|数据类型<br /><br /> 已输入代码|*2. x* 应用程序到<br /><br /> 2.x*驱动程序*|*2. x* 应用程序到<br /><br /> 3.x*驱动程序*|*3. x* 应用程序到<br /><br /> 2.x*驱动程序*|*3. x* 应用程序到<br /><br /> 3.x*驱动程序*|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_DATE (9) |无映射|SQL_TYPE_DATE (91)|无映射 [1]|SQL_TYPE_DATE (91)|  
|SQL_TYPE_DATE (91)|DM)  (错误|DM)  (错误|SQL_DATE (9) |无映射 [2]|  
|SQL_TIME (10) |无映射|SQL_TYPE_TIME (92) |无映射 [1]|SQL_TYPE_TIME (92) |  
|SQL_TYPE_TIME (92) |DM)  (错误|DM)  (错误|SQL_TIME (10) |无映射 [2]|  
|SQL_TIMESTAMP (11) |无映射|SQL_TYPE_TIMESTAMP (93)|无映射 [1]|SQL_TYPE_TIMESTAMP (93)|  
|SQL_TYPE_TIMESTAMP (93)|DM)  (错误|DM)  (错误|SQL_TIMESTAMP (11) |无映射 [2]|  
  
 [1] 这样做的结果是，*使用 odbc 2.x* *驱动程序的 odbc 1.x 应用程序*可以使用目录函数返回的结果集中返回的日期、时间或时间戳代码。  
  
 [2] 因此，*使用 odbc 1.x* *驱动程序的 odbc 1.x 应用程序*可以使用目录函数返回的结果集中返回的日期、时间或时间戳代码。
