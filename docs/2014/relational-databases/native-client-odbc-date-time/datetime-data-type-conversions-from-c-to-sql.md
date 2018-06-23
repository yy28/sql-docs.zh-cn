---
title: 从 C 到 SQL 转换 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- conversions [ODBC], C to SQL
ms.assetid: 7ac098db-9147-4883-8da9-a58ab24a0d31
caps.latest.revision: 35
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2941f9d95c8513762e8f77f8a84fcd34f682eafe
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129881"
---
# <a name="conversions-from-c-to-sql"></a>由 C 转换为 SQL
  本主题列出了需要考虑在 C 类型间转换的问题[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]日期/时间类型。  
  
 下表中介绍的转换适用于在客户端上所进行的转换。 如果客户端指定的参数的秒小数部分精度不同于服务器上定义的精度，客户端转换可能成功，但是当调用 `SQLExecute` 或 `SQLExecuteDirect` 时，服务器将返回错误。 特别是，ODBC 将对秒的小数部分的任何截断视为错误，而 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 则会进行舍入；例如，当从 `datetime2(6)` 转换到 `datetime2(2)` 时发生舍入。 Datetime 列值舍入为 1/300 秒，服务器将 smalldatetime 列的秒数设置为零。  
  
|||||||||  
|-|-|-|-|-|-|-|-|  
||SQL_TYPE_DATE|SQL_TYPE_TIME|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_SS_TIMSTAMPOFFSET|SQL_CHAR|SQL_WCHAR|  
|SQL_C_DATE|@shouldalert|-|-|1,6|1,5,6|1,13|1,13|  
|SQL_C_TIME|-|@shouldalert|@shouldalert|1,7|1,5,7|1,13|1,13|  
|SQL_C_SS_TIME2|-|1,3|1,10|1,7|1,5,7|1,13|1,13|  
|SQL_C_BINARY(SQL_SS_TIME2_STRUCT)|N/A|N/A|1,10,11|N/A|N/A|N/A|N/A|  
|SQL_C_TYPE_TIMESTAMP|1,2|1,3,4|1,4,10|1,10|1,5,10|1,13|1,13|  
|SQL_C_SS_TIMESTAMPOFFSET|1,2,8|1,3,4,8|1,4,8,10|1,8,10|1,10|1,13|1,13|  
|SQL_C_BINARY(SQL_SS_TIMESTAMPOFFSET_STRUCT)|N/A|N/A|N/A|N/A|1,10,11|N/A|N/A|  
|SQL_C_CHAR/SQL_WCHAR (date)|9|9|9|9,6|9,5,6|N/A|N/A|  
|SQL_C_CHAR/SQL_WCHAR (time2)|9|9,3|9,10|9,7,10|9,5,7,10|N/A|N/A|  
|SQL_C_CHAR/SQL_WCHAR (datetime)|9,2|9,3,4|9,4,10|9,10|9,5,10|N/A|N/A|  
|SQL_C_CHAR/SQL_WCHAR (datetimeoffset)|9,2,8|9,3,4,8|9,4,8,10|9,8,10|9,10|N/A|N/A|  
|SQL_C_BINARY(SQL_DATE_STRUCT)|1,11|N/A|N/A|N/A|N/A|N/A|N/A|  
|SQL_C_BINARY(SQL_TIME_STRUCT)|N/A|N/A|N/A|N/A|N/A|N/A|N/A|  
|SQL_C_BINARY(SQL_TIMESTAMP_STRUCT)|N/A|N/A|N/A|N/A|N/A|N/A|N/A|  
  
## <a name="key-to-symbols"></a>符号含义  
  
|符号|含义|  
|------------|-------------|  
|-|不支持任何转换。 生成具有 SQLSTATE 07006 和消息“受限制的数据类型属性冲突”的诊断记录。|  
|@shouldalert|如果提供的数据无效，则生成具有 SQLSTATE 22007 和消息“日期时间格式无效”的诊断记录。|  
|2|时间字段必须为零，否则，将生成具有 SQLSTATE 22008 和消息“小数部分截断”的诊断记录。|  
|3|秒的小数部分必须为零，否则将生成具有 SQLSTATE 22008 和消息“小数部分截断”的诊断记录。|  
|4|忽略日期部分。|  
|5|根据客户端的时区设置设置时区。|  
|6|时间设置为零。|  
|7|日期设置为当前日期。|  
|8|将时间从客户端时区转换为 UTC。 如果在此转换过程中发生错误，则生成具有 SQLSTATE 22008 和消息“日期时间字段溢出”的诊断记录。|  
|9|根据遇到的第一个标点符号以及存在的剩余部分分析该字符串，并将其转换为 date、datetime、datetimeoffset 或 time 值。 然后，根据上表中针对此过程发现的源类型的规则，此字符串将转换为目标类型。 如果在分析数据时检测到错误，则生成具有 SQLSTATE 22018 和消息“为转换指定的字符值无效”的诊断记录。 对于 datetime 和 smalldatetime 参数，如果年份超出这些类型支持的范围，则生成具有 SQLSTATE 22007 和消息“日期时间格式无效”的诊断记录。<br /><br /> 对于 datetimeoffset，在转换为 UTC 后该值必须处于规定范围内，即使不要求转换为 UTC。 这是因为 TDS 和服务器始终规范化 UTC 的 datetimeoffset 值中的时间，因此在转换为 UTC 后，客户端必须确认时间部分处于支持的范围内。 如果值不在支持的 UTC 范围内，则生成具有 SQLSTATE 22007 和消息“日期时间格式无效”的诊断记录。|  
|10|如果发生截断且丢失数据，将生成一条具有 SQLSTATE 22008 和消息“时间格式无效”的诊断记录。 如果值处于服务器使用的 UTC 范围可表示的范围外，也会发生此错误。|  
|11|如果数据的字节长度不等于 SQL 类型所需的结构的大小，则生成具有 SQLSTATE 22003 和消息“数值超出了范围”的诊断记录。|  
|12|如果数据的字节长度为 4 或 8，则采用原始 TDS smalldatetime 或 datetime 格式将数据发送到服务器。 如果数据的字节长度与 SQL_TIMESTAMP_STRUCT 大小完全匹配，则将该数据转换为 datetime2 的 TDS 格式。|  
|13|如果发生截断且丢失数据，则生成具有 SQLSTATE 22001 和消息“字符串数据，右端被截断”的诊断记录。<br /><br /> 秒的小数部分位数 （缩放） 由根据以下目标列的大小：<br /><br /> **类型：** SQL_C_TYPE_TIMESTAMP<br /><br /> 暗指的小数位数<br /><br /> 0<br /><br /> 19<br /><br /> 暗指的小数位数<br /><br /> 1..9<br /><br /> 21..29<br /><br /> 但是，对于 SQL_C_TYPE_TIMESTAMP，如果秒的小数部分可以在不丢失数据的情况下由三位数表示，并且列大小为 23 或更大，则生成确切的三位数的秒小数部分。 此行为确保使用早期 ODBC 驱动程序开发的应用程序的向后兼容性。<br /><br /> 对于大于表中范围的列大小，则暗指小数位数为 9。 此转换应允许的秒的小数部分位数多达 9 位，这是 ODBC 允许的最大位数。<br /><br /> 列大小为零则暗指 ODBC 中可变长度字符类型的大小无限制（即 9 位，除非应用 SQL_C_TYPE_TIMESTAMP 的三位数规则）。 指定列大小为零且具有固定长度的字符类型是错误的。|  
|N/A|现有 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更早版本的行为将保持。|  
  
## <a name="see-also"></a>请参阅  
 [日期和时间改进&#40;ODBC&#41;](date-and-time-improvements-odbc.md)  
  
  