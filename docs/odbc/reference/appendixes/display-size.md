---
title: "显示大小 |Microsoft 文档"
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
- display size of data types [ODBC]
- size of data types [ODBC]
- data types [ODBC], display size
- SQL data types [ODBC], column characteristics
ms.assetid: 9f7f766f-2492-463c-aab7-f2476e222042
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 222150f200720a9213bc8f04cf7900771c2e0619
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="display-size"></a>显示大小
列的显示大小是最大字符窗体中显示数据所需的字符数。 下表定义每个 ODBC SQL 数据类型的显示大小。  
  
|SQL 类型标识符|显示大小|  
|-------------------------|------------------|  
|所有字符类型 [a]|（对于固定类型） 定义或最大值 （为变量的类型） 显示字符窗体中的数据所需的字符数。|  
|SQL_DECIMAL SQL_NUMERIC|列加上 2 精度 (的登录，*精度*数字和小数)。 例如，定义为 NUMERIC(10,3) 的列的显示大小为 12。|  
|SQL_BIT|1 （1 个数字）。|  
|SQL_TINYINT|如果签名 （一个符号和 3 个数字） 4 或 3 如果无符号 （3 位）。|  
|SQL_SMALLINT|如果签名 （一个符号和 5 位数字） 6 或 5 如果无符号 （5 位数字）。|  
|SQL_INTEGER|如果签名 （一个符号和 10 位数字） 的 11 或 10 如果无符号 （10 个数字）。|  
|SQL_BIGINT|20 （登录和 19 位数如果签名或如果未签名的 20 位数字）。|  
|SQL_REAL|14 (登录、 7 位，小数点、 字母*E*，一个符号和 2 位数)。|  
|SQL_FLOAT SQL_DOUBLE|24 (登录、 15 位，小数点、 字母*E*，一个符号和 3 个数字)。|  
|所有二进制类型 [a]|定义或 （对于变量类型） 最大列长度的时间 2。 （每个二进制字节表示的 2 位十六进制数字的中）。|  
|SQL_TYPE_DATE|10 (日期的日期格式*yyyy-月-日*)。|  
|SQL_TYPE_TIME|8 (格式的时间*hh: mm:*)<br /><br /> - 或 -<br /><br /> 9 + *s* (格式的时间*hh: mm:*[.fff...] 其中*s*是秒的小数部分精度)。|  
|SQL_TYPE_TIMESTAMP|19 (时间戳为*yyyy mm dd hh: mm:*格式)<br /><br /> - 或 -<br /><br /> 20 + *s* (时间戳为*yyyy mm dd hh: mm:*[.fff...] 格式，其中*s*是秒的小数部分精度)。|  
|所有 interval 数据类型|请参阅[间隔数据类型长度](../../../odbc/reference/appendixes/interval-data-type-length.md)。|  
|SQL_GUID|36 (中的字符数*aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee*格式|  
  
 [a] 如果驱动程序无法确定变量类型的列或参数长度，它将返回 SQL_NO_TOTAL。
