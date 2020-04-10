---
title: 使用 SQL 转义序列 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 00f9e25a-088e-4ac6-aa75-43eacace8f03
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2b2bacdc6eb65824c34f6bb2e6dec86f5abe9efd
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924016"
---
# <a name="using-sql-escape-sequences"></a>使用 SQL 转义序列

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

按照 JDBC API 的定义，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 支持使用 SQL 转义序列。 转义序列用于 SQL 语句内，以告诉驱动程序应以不同的方式处理 SQL 字符串的转义部分。 当 JDBC 驱动程序处理 SQL 字符串的转义部分时，它会将字符串的这一部分转换为 SQL Server 可以理解的 SQL 代码。  
  
 JDBC API 需要五种类型的转义序列，JDBC 驱动程序支持所有这些转义序列：  
  
- LIKE 通配符文本
- 函数处理
- 日期和时间文本
- 存储过程调用
- 外部联接
- 限制转义语法

JDBC 驱动程序使用的转义序列语法如下所示：  
  
`{keyword ...parameters...}`  
  
> [!NOTE]  
> SQL 转义处理对于 JDBC 驱动程序始终是打开的。  
  
以下各部分介绍五种类型的转义序列以及 JDBC 驱动程序如何支持它们。  
  
## <a name="like-wildcard-literals"></a>LIKE 通配符文本

JDBC 驱动程序支持 `{escape 'escape character'}` 语法，以便将 LIKE 子句通配符用作文本。 例如，以下代码将返回 col3 的值，其中 col2 的值实际上以下划线开始（而不是对其使用通配符）。  

```java
ResultSet rst = stmt.executeQuery("SELECT col3 FROM test1 WHERE col2   
LIKE '\\_%' {escape '\\'}");  
```

> [!NOTE]  
> 转义序列必须位于 SQL 语句的结尾。 如果一个命令字符串中有多个 SQL 语句，则转义序列需要位于每个相关 SQL 语句的结尾。  

## <a name="function-handling"></a>函数处理

JDBC 驱动程序使用以下语法在 SQL 语句中支持函数转义序列：  

```sql
{fn functionName}  
```

其中，`functionName` 是由 JDBC 驱动程序支持的函数。 例如： 

```sql
SELECT {fn UCASE(Name)} FROM Employee  
```

下表列出当使用函数转义序列时，JDBC 驱动程序支持的各种函数：  
  
| 字符串函数                                                                                                                                                                                                                                                                                                                        | 数值函数                                                                                                                                                                                                                                                                                                                                                                                                   | 日期时间函数                                                                                                                                                                                                                                                                                                                                             | 系统函数                             |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------- |
| ASCII<br /><br /> CHAR<br /><br /> CONCAT<br /><br /> DIFFERENCE<br /><br /> INSERT<br /><br /> LCASE<br /><br /> LEFT<br /><br /> LENGTH<br /><br /> LOCATE<br /><br /> LTRIM<br /><br /> REPEAT<br /><br /> REPLACE<br /><br /> RIGHT<br /><br /> RTRIM<br /><br /> SOUNDEX<br /><br /> SPACE<br /><br /> SUBSTRING<br /><br /> UCASE | ABS<br /><br /> ACOS<br /><br /> ASIN<br /><br /> ATAN<br /><br /> ATAN2<br /><br /> CEILING<br /><br /> COS<br /><br /> COT<br /><br /> DEGREES<br /><br /> EXP<br /><br /> FLOOR<br /><br /> 日志<br /><br /> LOG10<br /><br /> MOD<br /><br /> PI<br /><br /> POWER<br /><br /> RADIANS<br /><br /> RAND<br /><br /> ROUND<br /><br /> SIGN<br /><br /> SIN<br /><br /> SQRT<br /><br /> TAN<br /><br /> TRUNCATE | CURDATE<br /><br /> CURTIME<br /><br /> DAYNAME<br /><br /> DAYOFMONTH<br /><br /> DAYOFWEEK<br /><br /> DAYOFYEAR<br /><br /> EXTRACT<br /><br /> HOUR<br /><br /> MINUTE<br /><br /> 月<br /><br /> MONTHNAME<br /><br /> NOW<br /><br /> QUARTER<br /><br /> SECOND<br /><br /> TIMESTAMPADD<br /><br /> TIMESTAMPDIFF<br /><br /> {1}WEEK{2}<br /><br /> 年 | DATABASE<br /><br /> IFNULL<br /><br /> USER |

> [!NOTE]  
> 如果您试图使用数据库不支持的函数，则将发生错误。  

## <a name="date-and-time-literals"></a>日期和时间文本

用于日期、时间和时间戳文本的转义语法如下所示：  

```sql
{literal-type 'value'}  
```

其中，`literal-type` 为以下值之一：  
  
| 文本类型 | 说明 | 值格式               |
| ------------ | ----------- | -------------------------- |
| d            | Date        | yyyy-mm-dd                 |
| t            | 时间        | hh:mm:ss [1]               |
| ts           | TimeStamp   | yyyy-mm-dd hh:mm:ss[.f...] |
  
例如：  

```sql
UPDATE Orders SET OpenDate={d '2005-01-31'}
WHERE OrderID=1025  
```

## <a name="stored-procedure-calls"></a>存储过程调用

JDBC 驱动程序对于存储过程调用支持 `{? = call proc_name(?,...)}` 和 `{call proc_name(?,...)}` 转义语法，具体取决于是否需要处理返回参数。  
  
过程是存储在数据库中的可执行对象。 通常，它是一个或更多的已经预编译的 SQL 语句。 调用存储过程的转义序列语法如下所示：  

```sql
{[?=]call procedure-name[([parameter][,[parameter]]...)]}  
```

其中，`procedure-name` 指定存储过程的名称，`parameter` 指定存储过程参数。  
  
有关将 `call` 转义序列用于存储过程的详细信息，请参阅[结合使用语句和存储过程](../../connect/jdbc/using-statements-with-stored-procedures.md)。  

## <a name="outer-joins"></a>外部联接

JDBC 驱动程序支持 SQL92 左联接、右联接和完全外部联接语法。 外部联接的转义序列如下所示：  

```sql
{oj outer-join}  
```

其中，外部联接为：  

```sql
table-reference {LEFT | RIGHT | FULL} OUTER JOIN
{table-reference | outer-join} ON search-condition  
```

其中，`table-reference` 为表名，`search-condition` 为要用于这些表的联接条件。  
  
例如：  

```sql
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status
   FROM {oj Customers LEFT OUTER JOIN
      Orders ON Customers.CustID=Orders.CustID}
   WHERE Orders.Status='OPEN'  
```

JDBC 驱动程序支持以下外部联接转义序列：  

- 左外部联接
- 右外部联接
- 完全外部联接
- 嵌套外部联接

## <a name="limit-escape-syntax"></a>限制转义语法  

> [!NOTE]  
> 在使用 JDBC 4.1 或更高版本时，LIMIT 转义语法仅受 Microsoft JDBC Driver 4.2 for SQL Server（或更高版本）支持。  
  
 LIMIT 的转义语法如下所示：  

```sql
LIMIT <rows> [OFFSET <row offset>]  
```

转义语法有两个部分：\<行> 是必需部分，用于指定要返回的行数  。 OFFSET 和 \<行偏移> 都是可选部分，用于指定在开始返回行之前要跳过的行数  。 JDBC 驱动程序通过将查询转换为使用 TOP 而不是 LIMIT，仅支持必需部分。 SQL Server 不支持 LIMIT 子句。 JDBC 驱动程序不支持可选的 **行偏移>；如果使用它，驱动程序将引发异常\<** 。  
  
## <a name="see-also"></a>另请参阅

[通过 JDBC 驱动程序使用语句](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
