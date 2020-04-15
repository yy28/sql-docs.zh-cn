---
title: 显式数据类型转换功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- explicit data type conversion functions [ODBC]
- data type conversion functions [ODBC]
- functions [ODBC], explicit data type conversion functions
ms.assetid: d5789450-b668-4753-96c8-6789e955e7ed
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2de8a8cb6177e9210e8d48c0ce097d13c9a276fd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306988"
---
# <a name="explicit-data-type-conversion-function"></a>显式数据类型转换函数
显式数据类型转换根据 SQL 数据类型定义指定。  
  
 显式数据类型转换函数的 ODBC 语法不限制转换。 一种数据类型到另一种数据类型的特定转换的有效性将由每个特定于驱动程序的实现确定。 驱动程序将由于它将 ODBC 语法转换为本机语法，因此将拒绝数据源不支持的转换（尽管在 ODBC 语法中是合法的）。 ODBC 函数**SQLGetInfo**具有转换选项（如SQL_CONVERT_BIGINT、SQL_CONVERT_BINARY、SQL_CONVERT_INTERVAL_YEAR_MONTH等），提供了一种查询数据源支持的转换的方法。  
  
 **CONVERT**函数的格式为：  
  
 **转换**_value_exp__（value_exp，data_type）_**)**  
  
 该函数返回*value_exp*转换为指定*data_type*指定的值，其中*data_type*是以下关键字之一：  
  
|||  
|-|-|  
|SQL_BIGINT|SQL_INTERVAL_HOUR_TO_MINUTE|  
|SQL_BINARY|SQL_INTERVAL_HOUR_TO_SECOND|  
|SQL_BIT|SQL_INTERVAL_MINUTE_TO_SECOND|  
|SQL_CHAR|SQL_LONGVARBINARY|  
|SQL_DECIMAL|SQL_LONGVARCHAR|  
|SQL_DOUBLE|SQL_NUMERIC|  
|SQL_FLOAT|SQL_REAL|  
|SQL_GUID|SQL_SMALLINT|  
|SQL_INTEGER|SQL_DATE|  
|SQL_INTERVAL_MONTH|SQL_TIME|  
|SQL_INTERVAL_YEAR|SQL_TIMESTAMP|  
|SQL_INTERVAL_YEAR_TO_MONTH|SQL_TINYINT|  
|SQL_INTERVAL_DAY|SQL_VARBINARY|  
|SQL_INTERVAL_HOUR|SQL_VARCHAR|  
|SQL_INTERVAL_MINUTE|SQL_WCHAR|  
|SQL_INTERVAL_SECOND|SQL_WLONGVARCHAR|  
|SQL_INTERVAL_DAY_TO_HOUR|SQL_WVARCHAR|  
|SQL_INTERVAL_DAY_TO_MINUTE||  
|SQL_INTERVAL_DAY_TO_SECOND||  
  
 显式数据类型转换函数的 ODBC 语法不支持转换格式的规范。 如果基础数据源支持显式格式的规范，则驱动程序必须指定默认值或实现格式规范。  
  
 *参数value_exp*可以是列名、另一个标量函数的结果或数字或字符串文本。 例如：  
  
```  
{ fn CONVERT( { fn CURDATE() }, SQL_CHAR ) }  
```  
  
 将 CURDATE 标量函数的输出转换为字符串。  
  
 由于 ODBC 不强制使用标量函数返回值的数据类型（因为这些函数通常是特定于数据源的），因此应用程序应尽可能使用 CONVERT 标量函数来强制转换数据类型。  
  
 以下两个示例说明了**CONVERT**函数的使用。 这些示例假定存在名为"员工"的表，该表的类型为SQL_SMALLINT的 EMPNO 列，类型SQL_CHAR EMPNAME 列。  
  
 如果应用程序指定以下 SQL 语句：  
  
```  
SELECT EMPNO FROM EMPLOYEES WHERE {fn CONVERT(EMPNO,SQL_CHAR)} LIKE '1%'  
```  
  
-   ORACLE 的驱动程序将 SQL 语句转换为：  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE to_char(EMPNO) LIKE '1%'  
    ```  
  
-   SQL Server 的驱动程序将 SQL 语句转换为：  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE convert(char,EMPNO) LIKE '1%'  
    ```  
  
 如果应用程序指定以下 SQL 语句：  
  
```  
SELECT {fn ABS(EMPNO)}, {fn CONVERT(EMPNAME,SQL_SMALLINT)}  
   FROM EMPLOYEES WHERE EMPNO <> 0  
```  
  
-   ORACLE 的驱动程序将 SQL 语句转换为：  
  
    ```  
    SELECT abs(EMPNO), to_number(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```  
  
-   SQL Server 的驱动程序将 SQL 语句转换为：  
  
    ```  
    SELECT abs(EMPNO), convert(smallint, EMPNAME) FROM EMPLOYEES  
       WHERE EMPNO <> 0  
    ```  
  
-   Ingres 的驱动程序将 SQL 语句转换为：  
  
    ```  
    SELECT abs(EMPNO), int2(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```
