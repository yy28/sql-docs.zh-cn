---
title: 显示大小 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- display size of data types [ODBC]
- size of data types [ODBC]
- data types [ODBC], display size
- SQL data types [ODBC], column characteristics
ms.assetid: 9f7f766f-2492-463c-aab7-f2476e222042
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c7d4a14a6afc2d716e85e687cbae1a202a596d7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63241243"
---
# <a name="display-size"></a>显示大小
列的显示大小是最大字符窗体中显示数据所需的字符数。 下表定义每个 ODBC SQL 数据类型的显示大小。  
  
|SQL 类型标识符|显示大小|  
|-------------------------|------------------|  
|所有字符类型 [a]|定义 （适用于固定类型） 或 （对于变量类型） 最大字符窗体中显示数据所需的字符数。|  
|SQL_DECIMAL SQL_NUMERIC|列加上 2 的精度 (a 的登录，*精度*数字和小数点)。 例如，定义为 NUMERIC(10,3) 的列的显示大小为 12。|  
|SQL_BIT|1 （1 个数字）。|  
|SQL_TINYINT|如果签名 （以符号和 3 位数字） 4 或 3 无符号 （3 位数字）。|  
|SQL_SMALLINT|如果签名 （以符号和 5 位数字） 的 6 或 5 无符号 （5 位数）。|  
|SQL_INTEGER|如果签名 （以符号和数字） 的 11 或 10 无符号 （10 个数字）。|  
|SQL_BIGINT|20 （以符号和 19 个数字，如果签名或 20 位数字，如果无符号）。|  
|SQL_REAL|14 (登录、 7 位、 小数点、 以字母*E*，号和 2 位数)。|  
|SQL_FLOAT SQL_DOUBLE|24 (一个符号，15 位、 小数点、 字母*E*，一个符号和 3 位数字)。|  
|所有二进制类型 [a]|定义或最大 （适用于变量类型） 的列的长度乘以 2。 （每个二进制字节表示的 2 位十六进制数中）。|  
|SQL_TYPE_DATE|10 (日期格式的日期*年-月-日*)。|  
|SQL_TYPE_TIME|8 (格式的时间*hh: mm:* )<br /><br /> - 或 -<br /><br /> 9 + *s* (格式的时间*hh: mm:* [....fff]，其中*s*秒的小数部分精度)。|  
|SQL_TYPE_TIMESTAMP|19 (对于中的时间戳*年-月-日 hh: mm:* 格式)<br /><br /> - 或 -<br /><br /> 20 + *s* (对于中的时间戳*年-月-日： 分： 秒*[.fff...] 格式，其中*s*秒的小数部分精度)。|  
|所有时间间隔数据类型|请参阅[间隔数据类型长度](../../../odbc/reference/appendixes/interval-data-type-length.md)。|  
|SQL_GUID|36 (中的字符数*aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee*格式|  
  
 [a] 如果驱动程序无法确定变量类型的列或参数的长度，它将返回 SQL_NO_TOTAL。
