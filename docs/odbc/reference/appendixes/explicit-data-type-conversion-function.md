---
title: 显式数据类型转换函数的 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77cb69877324b36120b3a277688bb1ad737f5c4d
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54129817"
---
# <a name="explicit-data-type-conversion-function"></a>显式数据类型转换函数
根据 SQL 数据类型定义指定显式数据类型转换。  
  
 显式数据类型转换函数的 ODBC 语法不限制转换。 一种数据类型到另一种数据类型的特定转换的有效性取决于每个特定于驱动程序的实现。 该驱动程序将它将 ODBC 语法转换为本机语法，如拒绝，尽管法律在 ODBC 语法中，不支持数据源的这些转换。 ODBC 函数**SQLGetInfo**，进行转换选项 （如 SQL_CONVERT_BIGINT、 SQL_CONVERT_BINARY、 SQL_CONVERT_INTERVAL_YEAR_MONTH，等等），提供了一种方法来查询有关所支持的数据源转换.  
  
 格式**转换**函数是：  
  
 **转换 (** _value_exp_， _data_type_**)**  
  
 该函数返回指定的值*value_exp*转换为指定*data_type*，其中*data_type*是以下关键字之一：  
  
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
  
 显式数据类型转换函数的 ODBC 语法不支持转换格式规范。 如果基础数据源支持的显式格式规范，则驱动程序必须指定默认值或实现格式规范。  
  
 自变量*value_exp*可以是列名称、 另一个标量函数或数值的结果或字符串文字。 例如：  
  
```  
{ fn CONVERT( { fn CURDATE() }, SQL_CHAR ) }  
```  
  
 将 CURDATE 标量函数的输出转换为字符字符串。  
  
 由于 ODBC 不强制要求来自的返回值的数据类型标量函数 （因为函数通常是数据源特定），应用程序应使用 CONVERT 标量函数，只要有可能以强制数据类型转换。  
  
 以下两个示例说明如何使用**转换**函数。 这些示例假定名员工，为与类型 SQL_SMALLINT EMPNO 列和类型 SQL_CHAR EMPNAME 列的表存在。  
  
 如果应用程序指定以下 SQL 语句：  
  
```  
SELECT EMPNO FROM EMPLOYEES WHERE {fn CONVERT(EMPNO,SQL_CHAR)} LIKE '1%'  
```  
  
-   用于 ORACLE 的驱动程序将转换到的 SQL 语句：  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE to_char(EMPNO) LIKE '1%'  
    ```  
  
-   适用于 SQL Server 驱动程序将转换到的 SQL 语句：  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE convert(char,EMPNO) LIKE '1%'  
    ```  
  
 如果应用程序指定以下 SQL 语句：  
  
```  
SELECT {fn ABS(EMPNO)}, {fn CONVERT(EMPNAME,SQL_SMALLINT)}  
   FROM EMPLOYEES WHERE EMPNO <> 0  
```  
  
-   用于 ORACLE 的驱动程序将转换到的 SQL 语句：  
  
    ```  
    SELECT abs(EMPNO), to_number(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```  
  
-   适用于 SQL Server 驱动程序将转换到的 SQL 语句：  
  
    ```  
    SELECT abs(EMPNO), convert(smallint, EMPNAME) FROM EMPLOYEES  
       WHERE EMPNO <> 0  
    ```  
  
-   Ingres 的驱动程序将转换到的 SQL 语句：  
  
    ```  
    SELECT abs(EMPNO), int2(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```
