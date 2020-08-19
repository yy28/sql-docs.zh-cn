---
description: SQL 一致性级别（Oracle ODBC 驱动程序）
title: " (用于 Oracle) 的 ODBC 驱动程序的 SQL 一致性级别 |Microsoft Docs"
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
ms.openlocfilehash: 78e98aed952ef8b15a4654be9f82e355d1b4177b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483420"
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>SQL 一致性级别（Oracle ODBC 驱动程序）
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 适用于 Oracle 的 ODBC 驱动程序支持最低 SQL 语法和核心 SQL 语法，还支持以下 SQL ODBC 扩展：  
  
-   日期、时间和时间戳数据  
  
-   左外部联接和右外部联接  
  
-   数值函数：  

    :::row:::
        :::column:::
            Abs  
            Ceiling  
            Cos  
            Exp  
            Floor  
        :::column-end:::
        :::column:::
            日志  
            Log10  
            Mod  
            Pi  
            电源  
        :::column-end:::
        :::column:::
            round  
            第 2 个  
            签名  
            sin  
            sqrt  
        :::column-end:::
        :::column:::
            tan  
            truncate  
        :::column-end:::
    :::row-end:::
    
-   日期函数：  

    :::row:::
        :::column:::
            Curdate  
            Curtime  
            Dayname  
            Dayofmonth  
        :::column-end:::
        :::column:::
            Dayofweek  
            Dayofyear  
            Hour  
            Month  
        :::column-end:::
        :::column:::
            monthname  
            minute  
            now  
            quarter  
        :::column-end:::
        :::column:::
            第 2 个  
            week  
            year  
        :::column-end:::
    :::row-end:::

-   字符串函数：  

    :::row:::
        :::column:::
            Ascii  
            Char  
            Concat  
            Lcase  
        :::column-end:::
        :::column:::
            Left  
            长度  
            Ltrim  
            Replace  
        :::column-end:::
        :::column:::
            右  
            rtrim  
            soundex  
            substring  
        :::column-end:::
        :::column:::
            ucase  
        :::column-end:::
    :::row-end:::

-   类型转换函数：  

    转换  

-   系统函数：  
  
    Ifnull  
    用户
