---
title: SQL 一致性级别（Oracle ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- ODBC driver for Oracle [ODBC], conformance levels
ms.assetid: 077a6c6a-2c57-42c9-a4fd-4cf0e65cf7e2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e283bbc13f0d0dda055b047b027f7b9816502df5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300677"
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>SQL 一致性级别（Oracle ODBC 驱动程序）
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 适用于 Oracle 的 ODBC 驱动程序支持最低 SQL 语法和核心 SQL 语法，还支持以下 SQL ODBC 扩展：  
  
-   日期、时间和时间戳数据  
  
-   左外部联接和右外部联接  
  
-   数值函数：  
  
    |||||  
    |-|-|-|-|  
    |Abs|日志|round|tan|  
    |Ceiling|Log10|second|truncate|  
    |Cos|Mod|签名||  
    |Exp|Pi|sin||  
    |层|强力|sqrt||  
  
-   日期函数：  
  
    |||||  
    |-|-|-|-|  
    |Curdate|Dayofweek|monthname|second|  
    |Curtime|Dayofyear|minute|week|  
    |Dayname|Hour|now|year|  
    |Dayofmonth|月份|quarter||  
  
-   字符串函数：  
  
    |||||  
    |-|-|-|-|  
    |Ascii|Left|右|ucase|  
    |Char|长度|rtrim||  
    |Concat|Ltrim|soundex||  
    |Lcase|将|substring||  
  
-   类型转换函数：  
  
    ||  
    |-|  
    |转换|  
  
-   系统函数：  
  
    ||  
    |-|  
    |Ifnull|  
    |User|
