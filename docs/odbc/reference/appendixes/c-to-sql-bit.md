---
title: C 到 SQL：位 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], bit
- bit data type [ODBC]
- data conversions from C to SQL types [ODBC], bit
ms.assetid: 267c9fa9-599e-4ee6-b51b-0cae43f09183
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a96982573d83cf01947f82dc2014ee2c470931e3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292040"
---
# <a name="c-to-sql-bit"></a>从 C 到 SQL：位
位 ODBC C 数据类型的标识符是：  
  
 SQL_C_BIT  
  
 下表显示了可转换为位 C 数据的 ODBC SQL 数据类型。 有关表中列和术语的说明，请参阅[将数据从 C 转换为 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 类型标识符|测试|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHARSQL_VARCHAR<br /><br /> SQL_LONGVARCHAR<br /><br /> SQL_WCHARSQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|None|不适用|  
|SQL_DECIMALSQL_NUMERIC<br /><br /> SQL_TINYINTSQL_SMALLINT<br /><br /> SQL_INTEGERSQL_BIGINT<br /><br /> SQL_REALSQL_FLOAT<br /><br /> SQL_DOUBLE|None|不适用|  
|SQL_BIT|None|不适用|  
  
 驱动程序在从位 C 数据类型转换数据时忽略长度/指示器值，并假定数据缓冲区的大小是位 C 数据类型的大小。 长度/指标值在**SQLPutData**中的*StrLen_or_Ind*参数中传递，在**SQLBind 参数**中用*StrLen_or_IndPtr*参数指定的缓冲区中传递。 数据缓冲区使用**SQLPutData**中的*DataPtr*参数和**SQLBind 参数**中的*参数ValuePtr*参数指定。
