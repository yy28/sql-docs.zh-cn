---
title: SQL 一致性级别 （Oracle ODBC 驱动程序） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0bf63b831dace7678f5d3fdf952a9d6d5f60aa6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63313389"
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>SQL 一致性级别（Oracle ODBC 驱动程序）
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 Oracle 的 ODBC 驱动程序支持的最小 SQL 语法和核心 SQL 语法，还支持以下 ODBC 扩展到 SQL:  
  
-   日期、 时间和时间戳数据  
  
-   左和右外部联接  
  
-   数值函数：  
  
    |||||  
    |-|-|-|-|  
    |Abs|日志|round|tan|  
    |上限|log10|second|truncate|  
    |Cos|Mod|登录||  
    |Exp|Pi|sin||  
    |floor|Power|sqrt||  
  
-   日期函数：  
  
    |||||  
    |-|-|-|-|  
    |Curdate|Dayofweek|monthname|second|  
    |Curtime|Dayofyear|minute|week|  
    |Dayname|Hour|现在|year|  
    |Dayofmonth|Month|每个季度||  
  
-   字符串函数：  
  
    |||||  
    |-|-|-|-|  
    |Ascii|Left|右侧|Ucase|  
    |Char|长度|rtrim||  
    |Concat|Ltrim|Soundex||  
    |Lcase|替换|substring||  
  
-   类型转换函数：  
  
    ||  
    |-|  
    |转换|  
  
-   系统函数：  
  
    ||  
    |-|  
    |Ifnull|  
    |“用户”|
