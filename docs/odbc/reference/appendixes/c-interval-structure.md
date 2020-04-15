---
title: C 间隔结构 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- interval data type [ODBC], structure
- C data types [ODBC], interval
ms.assetid: 52b42b56-50aa-4ce6-8d79-0963c7a71437
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 02c86ebe24a0e12531e355f95185b01f3089a31b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292149"
---
# <a name="c-interval-structure"></a>C 间隔结构
[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)部分中列出的每个 C 间隔数据类型都使用相同的结构来包含间隔数据。 当调用**SQLFetch、SQLFetch**或**SQLGetData**时，驱动程序将数据返回到SQL_INTERVAL_STRUCT结构中，使用应用程序为 C 数据类型指定的值（在调用**SQLFetchScroll** **SQLBindCol、SQLGetData**或**SQLGetData****SQLBind参数**）来解释SQL_INTERVAL_STRUCT的内容，并使用与 C 类型的枚*举*值填充结构*interval_type*字段。 请注意，驱动程序不读取*interval_type*字段以确定间隔的类型;因此，驱动程序不会读取该字段。它们检索SQL_DESC_CONCISE_TYPE描述符字段的值。 当结构用于参数数据时，驱动程序使用应用程序在 APD SQL_DESC_CONCISE_TYPE 字段中指定的值来解释SQL_INTERVAL_STRUCT的内容，即使应用程序将*interval_type*字段的值设置为不同的值也是如此。  
  
 此结构的定义如下：  
  
```  
typedef struct tagSQL_INTERVAL_STRUCT  
{  
   SQLINTERVAL interval_type;   
   SQLSMALLINT interval_sign;  
   union {  
         SQL_YEAR_MONTH_STRUCT   year_month;  
         SQL_DAY_SECOND_STRUCT   day_second;  
         } intval;  
} SQL_INTERVAL_STRUCT;  
typedef enum   
{  
   SQL_IS_YEAR = 1,  
   SQL_IS_MONTH = 2,  
   SQL_IS_DAY = 3,  
   SQL_IS_HOUR = 4,  
   SQL_IS_MINUTE = 5,  
   SQL_IS_SECOND = 6,  
   SQL_IS_YEAR_TO_MONTH = 7,  
   SQL_IS_DAY_TO_HOUR = 8,  
   SQL_IS_DAY_TO_MINUTE = 9,  
   SQL_IS_DAY_TO_SECOND = 10,  
   SQL_IS_HOUR_TO_MINUTE = 11,  
   SQL_IS_HOUR_TO_SECOND = 12,  
   SQL_IS_MINUTE_TO_SECOND = 13  
} SQLINTERVAL;  
  
typedef struct tagSQL_YEAR_MONTH  
{  
   SQLUINTEGER year;  
   SQLUINTEGER month;   
} SQL_YEAR_MONTH_STRUCT;  
  
typedef struct tagSQL_DAY_SECOND  
{  
   SQLUINTEGER day;  
   SQLUINTEGER hour;  
   SQLUINTEGER minute;  
   SQLUINTEGER second;  
   SQLUINTEGER fraction;  
} SQL_DAY_SECOND_STRUCT;  
```  
  
 SQL_INTERVAL_STRUCT*的interval_type*字段向应用程序指示在联合中持有哪些结构，以及结构中哪些成员是相关的。 如果间隔前导字段未签名，*则interval_sign*字段具有值SQL_FALSE;如果SQL_TRUE，则前导字段为负。 无论*interval_sign*的值如何，前导字段本身的值始终没有符号。 *interval_sign*字段充当符号位。
