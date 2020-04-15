---
title: SQL 一致性级别（Oracle 的 ODBC 驱动程序） |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300677"
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>SQL 一致性级别（Oracle ODBC 驱动程序）
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 而是使用 Oracle 提供的 ODBC 驱动程序。  
  
 Oracle 的 ODBC 驱动程序支持最小 SQL 语法和核心 SQL 语法，还支持以下对 SQL 的 ODBC 扩展：  
  
-   日期、时间和时间戳数据  
  
-   左和右外部联接  
  
-   数字函数：  
  
    |||||  
    |-|-|-|-|  
    |Abs|日志|round|tan|  
    |Ceiling|Log10|second|truncate|  
    |Cos|Mod|签名||  
    |Exp|Pi|sin||  
    |层|电源|sqrt||  
  
-   日期函数：  
  
    |||||  
    |-|-|-|-|  
    |库达|周日|月名|second|  
    |诅咒|Dayofyear|minute|week|  
    |日名|Hour|now|year|  
    |每月的一天|月份|quarter||  
  
-   字符串函数：  
  
    |||||  
    |-|-|-|-|  
    |Ascii|Left|右|乌瓦凯斯|  
    |Char|长度|里特里姆||  
    |Concat|Ltrim|声音||  
    |Lcase|将|substring||  
  
-   类型转换功能：  
  
    ||  
    |-|  
    |转换|  
  
-   系统功能：  
  
    ||  
    |-|  
    |Ifnull|  
    |用户|
