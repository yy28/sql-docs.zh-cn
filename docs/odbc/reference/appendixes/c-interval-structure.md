---
title: "C 间隔结构 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], interval data types
- interval data type [ODBC], structure
- C data types [ODBC], interval
ms.assetid: 52b42b56-50aa-4ce6-8d79-0963c7a71437
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 00ec992c87cce93eb95cd85314743a109183c51f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="c-interval-structure"></a>C 间隔结构
每个 C interval 数据类型中列出[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)部分使用相同的结构来包含该间隔数据。 当**SQLFetch**， **SQLFetchScroll**，或**SQLGetData**是调用，该驱动程序到 SQL_INTERVAL_STRUCT 结构返回的数据，使用指定的值应用程序，C 数据类型 (在调用**SQLBindCol**， **SQLGetData**，或**SQLBindParameter**) 来解释 SQL_INTERVAL_STRUCT 的内容并填充*interval_type*字段具有结构*枚举*与 C 类型相对应的值。 请注意，不读取驱动程序*interval_type*字段以确定间隔的类型; 它们检索 SQL_DESC_CONCISE_TYPE 描述符字段的值。 当结构用于参数数据时，该驱动程序使用 APD SQL_DESC_CONCISE_TYPE 字段中的应用程序指定的值来解释的内容 SQL_INTERVAL_STRUCT，即使应用程序设置的值*interval_type*字段为不同的值。  
  
 此结构定义，如下所示：  
  
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
  
 *Interval_type* SQL_INTERVAL_STRUCT 字段指示应用程序在联合持有何种结构，还结构的哪些成员都是相关。 *Interval_sign*字段具有值 SQL_FALSE，如果前导字段的时间间隔是无符号; 如果它是 SQL_TRUE，前导字段为负。 前导字段自身中的值始终是无符号整数，而不考虑的值*interval_sign*。 *Interval_sign*域可用作符号位。
